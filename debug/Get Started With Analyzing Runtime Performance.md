# 分析运行时性能

### 内容

1. 开始
   - 模拟手机 CPU
   - 设置 demo
   - 录制运行时性能
2. 分析结果
   - 分析每秒的帧
   - 找出性能瓶颈
   - 福利：分析优化了的版本
3. 进一步学习

---

Runtime Performance 是你的页面运行时的情况，这与加载时相反。这个教程将教会你怎样来用 Chrome DevTools 性能分析面板来对运行时性能进行Fenix。就 RAIL model 而言，你从这个教程中学到的将有助于分析你页面的网络响应，动画以及idle phases。

> 注意：这个教程基于 Chrome 59，如果你用另外版本的 Chrome，DevTools 的 UI 界面和特性将可能有所不同。请检查 `crhome://help` 来查看你的 chrome 版本号

让我们开始吧！你使用过 Performance 面板多少次？

---

### 开始

在这个教程中，你应该在打开一个页面的同时使用性能分析面板来找到当前页面的性能瓶颈。

1. 在匿名模式下打开 Google Chrome。隐身模式确保了 chrome 运行在一个相对干净的环境下。举个栗子，如果你安装了非常多的插件，这些插件将对你页面的性能表现有所影响。

2. 在匿名窗口中加载下面的页面。这是你将要用来分析的 demo。这个页面展示了很多上下移动的蓝色小正方形。

   `https://googlechrome.github.io/devtools-samples/jank/`

3. 按下 `Command` + `option` + `I`（Mac）或者 `Control` + `shift` + `I`（Windows，Linux）来打开 DevTools。

   ![](https://github.com/JamieMaple/translation-blog/raw/master/debug/Get%20Started%20With%20Analyzing%20Runtime%20Performance/1.png)

   **Figure 1. ** demo 在左，DevTools 在右

   > 提示：对于剩下的截图，DevTools 被[分开到了另外的窗口](https://developers.google.com/web/tools/chrome-devtools/ui#placement)这样就能侧重看内容

##### 模拟移动端的 CPU

移动端设备的 CPU 一般比台式和笔记本弱很多。每当你想分析一个页面时，请使用 CPU Throttling 对这个页面进行移动设备性能模拟。

1. 在 DevTools 中，点击 Performance 选项。

2. 确保 Screenshots 已被选中。

3. 点击 Capture Settings. DevTools 有很多设定来模拟各类状况。

4. 对于 CPU ，请选择 2x slowdown。DevTools 将降低 CPU 性能，比原来慢两倍。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/throttling.svg)

   **Figure 2. ** 蓝色圈住的是 CPU throttling

   > Note：当测试其他页面时，如果你想确保他们在低配手机上运行良好，请将 CPU 性能下降到 20x slowdown。这个 demo无法在 20x slowdown 情况下工作良好，所以为了更好的教学，将使用 2x slowdown

##### 设置 demo

创建一个对所有读者来说都表现一样的运行时性能分析的 demo 是困难的。这个部分将让你自定义 demo，以确保然你体验到的 demo 相对稳定统一的，无论你怎样特别的设定。

1. 一直点击 Add 10 直到蓝色小正方形相比以前明显的卡顿。在性能比较好的机器上，大概需要点击 20 下。

2. 点击 Optimize。蓝色小正方形将再次运动流畅起来

   > 如果你没有看到优化和没优化两个版本明显的对比，请尝试点击 Subtract 10 几次进行多次尝试。如果你添加了过多的蓝色小正方形，你将让 CPU 运行满载，同时你将看不到这两者结果主要的区别。

   3. 点击 Un-Optimize。蓝色小正方形将会再次移动卡顿起来。

##### 记录运行时性能

当你运行这个页面优化后的版本，蓝色小正方形将运行流畅起来。为什么会这样？俩个版本都会让每一个正方形在相同的时间内移动相同的距离。在 Performance 面板中做录制，进一步学习怎样在未被优化的版本中检测页面性能瓶颈。

1. 在 DevTools 中，点击 Record。DevTools 将会随着页面运行来获得性能评估。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/profiling.png)

2. 等待几秒钟时间

3. 点击 Stop。DevTools 停止录制，分析数据，然后将在 Performance 面板上展示结果。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/results.png)

   **Figure 4:** profile 的结果

哇塞，这有非常多的数据。别担心，他将会很快证明非常有用。

###分析结果

一旦你得到了该页面的性能录制，你将会发现这个页面的性能有多么的差以及造成这个的原因有哪些。

##### 分析每秒的帧

衡量任何动画性能好坏的主要因素是看每秒多少帧（FPS）。当达到 60 FPS时，用户体验是非常好的。

1. 查看 FPS 图表栏。每当你发现 FPS 上方的红条时，这意味着存在非常严重的问题损害到了用户体验。整体来说，绿条越高，FPS 就越高。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/fps-chart.svg)

   **Figure 5:** 蓝色圈住的是 FPS 图表

2. 在 FPS 表格栏下面是 CPU 图表栏。CPU 栏里的颜色与下方 Summary 栏的颜色息息相关。当你看到 CPU 表格栏满满的颜色时，这意味着你的 CPU 在录制期间满载了。只要当你看到 CPU 满载工作了，你就有了减少 CPU 工作的线索。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/cpu-summary.svg)

   **Figure 6: ** 蓝色圈住的是 CPU 图表以及 Summary 选项卡

3. 鼠标悬停在 FPS，CPU 或者 NET 任意一栏上时。DevTools 将给你展示此页面该时刻的截图，左右移动鼠标将会重放此时间段内的录像。这个被称为 scrubbing，对于我们分析动画的每个细节是非常有用的。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/screenshot.png)

   **Figure 7 :** 页面截图大概在录像 2000ms 处

4. 在有关 Frames （帧）的部分，在任意一个绿色矩形上悬停你的鼠标。DevTools 将向你展示该特定帧的 FPS 的信息。每一帧都可能低于目标的 60FPS。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/frame.png)

   **Figure 8:** 悬停在某个帧

当然，这个 demo 很明显性能并不好。但是在实际的情况中，它可能并没有那么清楚，所以把这些工具都结合起来使用是非常好的。

##### 功能：打开 FPS 面板

另外一个很好用的工具是 FPS 面板，这个将在页面运行时提供实时的 FPS 信息。

1. 按下 `Command` + `Shift` + `P` (mac) 或者 `Control` + `Shift` + `P` (windows, linx) 来打开命令菜单栏。

2. 然后在命令菜单栏中输入 `Rendering`  然后选择 `Show Rendering`

3. 在 Rendering 表中，启用 FPS 面板。它将出现在页面的右上方。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/fps-meter.png)

   **Figure 9:** FPS 面板

4. 禁用 FPS 面板只需按下 `Escape` 来关闭 Rendering 栏。在这个教程中你将不会用到它。

##### 查找性能瓶颈所在

现在你发现了同时确定了页面动画非常不流畅，那么问题来了：是什么原因造成的？

1. 请注意 summary 选项卡。当没有选择任何事件，此面板会显示所有活动的细目。这个页面花费了很多时间在 rendering 上。因为**提升性能是减少工作的艺术**，你的目标就是来减少 rendering 的时间。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/summary.svg)

   **Figure 10: ** 蓝圈选中的是 Summary 选项卡

2. 展开 Man 部分。DevTools 将向你展示主线程在运行期间的各种情况。x 轴代表了录制的时间。每一条矩形都代表了一个事件。一个较宽的长条代表该事件花费了更长的事件。y 轴代表了调用栈。当你看到某些事件在其他事件之上时（栈），这意味着上方的事件调用了下方的事件。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/main.svg)

   **Figure 11:** 篮圈选中的是 Main 部分

3. 录制中有非常多的数据。通过单击、按住以及拖动鼠标到 Overview 来放大单个动画帧事件，这个部分包含了 FPS，CPU 以及 NET 图表。Main 部分和 Summary 选项卡只显示该选中的录像部分信息。

   ![](/var/folders/7c/w93rl_1d6f57c_2jr5xxxp0w0000gn/T/abnerworks.Typora/image-20180415095231783.png)

   **Figure 12:** 放大了的某个帧的 Animation Frame Fired 事件

   > 提示：另一个放大的方法就是通过点击 Main 部分的背景或者选中一个事件来让焦点在 Main 部分上，然后按 W, A, S 以及 D

4. 请注意在 Animation Frame Fired 事件右上方的红色小三角形。只要你看到这样的红色小三角形，你就要知道这是一个警告信息，代表了这个事件很有可能存在问题。

   > 提示：Animation Frame Fired 事件由 requestAnimationFrame() 回调函数调用而发生

5. 点击 Animation Frame Fired 事件。Summary 选项卡此时会向你展示这个事件的有关信息。请注意 reveal 链接。点击它将会让 DevTools 高亮启动该 Animation Frame Fired 事件的事件。同时注意 app.js:94 链接。点击它将跳转到源码中相关的代码位置。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/animation-frame-fired.png)

   **Figure 13:** 更多有关 Animation Frame Fired 事件的信息

   > 提示：在选中一个事件后，用箭头键来切换与其相近的事件

6. 在 app.update 事件下方，有一些颜色为紫色的事件。如果他们都比较长，那么它们每个事件都可能会有一个红三角。现在点击其中一个紫色 Layout 事件。DevTools 将为你在 summary 选项卡中提供更多的信息。实际上有一个关于强行热 reflow(回流) 的警告（layout(布局) 另一个词语）。

7. 在 Summary 选项卡中，点击在 Layout forced 下面的 app.js:70 链接。DevTools 将带你跳转到源码中强制你 layout(布局) 的代码行。

   ![](/var/folders/7c/w93rl_1d6f57c_2jr5xxxp0w0000gn/T/abnerworks.Typora/image-20180415095258297.png)

   **Figure 13:** 这行代码导致了强制 layout（布局）

   > 提示：这个代码中的问题就是：在每一个 Animation frame 中，它改变了每个小正方形的样式，同时还查询了该页面上每一个小长方形的位置信息。因为他们的样式都发生了变化，但是浏览器并不知道每一个小正方形的位置改变了，所以为了获取计算这些位置就必然会 relayout（重排） 这些小正方形。查看[Avoid forced synchronous layouts](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing#avoid_forced_synchronous_layouts) 了解更多

原来如此！虽然经过了这么努力分析，但是你现在已经有了很多关于分析运行时性能的基本工作流程的基础。非常好！

##### 福利：分析优化了的版本

利用刚刚学到的工作流程以及工具，点击 demo 中的 Optimize 来启用优化了的代码，进行又一次的性能录制，然后分析这些结果。从改进版本中 Main 部分的图表能看得到大量事件被缩减，你可以看到这个优化了的版本做了更少的工作却得到了更好性能的结果！

> 提示：尽管 这个 “优化了” 的版本不是那么好，因为他依然操作了每个正放心的 top 属性。一个更好的办法是使用只影响到 compositing 的属性。查看 [Use transform and opacity changes for animations](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count#use_transform_and_opacity_changes_for_animations) 来获取更多的信息。

---

### 进一步学习

理解性能的基础和关键在于 RAIL 模型。这个模型会告诉你影响用户使用体验的最重要的性能指标。查看 [Measure Performance With The RAIL Model](https://developers.google.com/web/fundamentals/performance/rail) 来获取更多信息。

为了更加堆 Performance 栏的使用更加适应，应当多练习。尝试对自己的页面进行 profile 然后分析结果。如果你对你的结果还有更多的问题，[open a Stack Overflow question tagged with `google-chrome-devtools`](http://stackoverflow.com/questions/ask?tags=google-chrome-devtools).尽可能包括这些截图或者链接以重现页面。

为了真正掌握主要的运行时性能，你需要学习浏览器是怎样翻译 HTML，CSS 以及 JS 到屏幕的每个像素中。最好的开始是这个 [Rendering Performance Overview](https://developers.google.com/web/fundamentals/performance/rendering/). [The Anatomy Of A Frame](https://aerotwist.com/blog/the-anatomy-of-a-frame/) ，你将会学到更多。

最后，有非常多的方式来对运行时的性能进行优化。这个教程只是针对一个比较特定的动画瓶颈，来让你重点浏览 Performance 面板，但是这仅仅是许多你应该考虑瓶颈中的一个。剩下还有更多更好关于 Rendering Performance 的文章，让你对其他非常多方面提升运行时性能，比如：

- [Optimizing JS Execution](https://developers.google.com/web/fundamentals/performance/rendering/optimize-javascript-execution)
- [Reduce The Scope And Complexity Of Style Calculations](https://developers.google.com/web/fundamentals/performance/rendering/reduce-the-scope-and-complexity-of-style-calculations)
- [Avoid Large, Complex Layouts And Layout Thrashing](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing)
- [Simplify Paint Complexity And Reduce Paint Areas](https://developers.google.com/web/fundamentals/performance/rendering/simplify-paint-complexity-and-reduce-paint-areas)
- [Stick To Compositor-Only Properties And Manage Layer Count](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)
- [Debounce Your Input Handlers](https://developers.google.com/web/fundamentals/performance/rendering/debounce-your-input-handlers)
