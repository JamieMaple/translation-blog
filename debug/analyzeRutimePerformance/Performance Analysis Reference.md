# 性能分析参考

### 内容

1. 记录性能
   - 记录运行时性能
   - 记录加载时性能
   - 记录时捕获快照（screenshots）
   - 记录时强制垃圾收集
   - 显示记录相关设置
   - 禁用 JavaScript 示例
   - 记录时节流网络
   - 记录时节流 CPU
   - 启用高级绘制工具
2. 保存记录
3. 加载记录
4. 清除之前的记录
5. 分析性能记录
   - 选择记录中的某部分
   - 搜寻活动
   - 查看主线程的活动
   - 查看 GPU 的活动
   - 查看 raster 活动
   - 查看交互
   - 分析每秒的帧数（FPS）
   - 查看网络请求
   - 查看内存指标
   - 查看部分记录的运行时间
   - 查看快照
   - 查看图层信息
   - 查看绘制分析器（profiler）
6. 通过 Rendering 选项卡对渲染性能进行分析
   - 通过 FPS 面板查看运行时的每秒帧数
   - 通过 Paint Flashing 查看运行时的绘制事件
   - 通过 Layers Borders 查看图层的叠加层
   - 查找运行时的滑动性能问题

这个页面涵盖了所有与性能分析相关方面 Chrome DevTools 的参考。

参阅 [Get Started With Analyzing Runtime Performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/) 来获取怎样通过 Chrome DevTools 来分析页面性能的指南。

---

### 记录性能

##### 记录运行时性能

记录运行时性能是在当你想要分析页面性能同时正在运行的的时候，这与加载时相反。

1. 前往你想要进行分析的页面

2. 点击在 DevTools 中的 **Performance** 选项卡

3. 点击 **Record**

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/record.svg)

   **Figure 1. Record** 蓝圈圈出来的

4. 与页面进行交互。DevTools 将会记录所有你与页面交互后发生的活动。

5. 再一次点击 **Record** 或者点击 **Stop** 来停止记录。

##### 记录加载时性能

记录加载时性能时在当你想分析页面性能同时正在加载的时候，这与运行时相反。

1. 前往你想要进行分析的页面

2. 打开 DevTools 中的 **Performance** 选项卡

3. 点击 **Reload page**。DevTools 会在页面重新加载记录性能的数据然后会在加载完成几秒后自动停止录制。

   ![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/reload-page.svg)

   **Figure 2. Reload page**，篮圈圈中的。


DevTools 会自动缩放到大多数事件发生的某部分记录上。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/load-recording.png)

**Figure 3.** 一个页面加载时的记录

##### 捕获记录时的快照

勾选 **Screenshots** 选项框来捕获记录时的每一帧。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/screenshots.svg)

**Figure 4**. **Screenshots** 选项框

参阅 [View a screenshot](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#view-screenshot) 学习更多关于怎样与快照进行交互。

##### 强制在记录时垃圾回收

当你在记录一个页面的时候，点击 **Collect garbage** 来强制垃圾回收。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/collect-garbage.svg)

**Figure 5**. 蓝圈圈中了垃圾回收

##### 显示记录相关设置

点击 **Capture settings** 显示更多关于 DevTools 捕获性能记录的选项设置。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/capture-settings.svg)

**Figure 6**. 蓝圈圈中的是 **Capture settings** 

##### 禁用 JavaScript 示例

默认情况下，**Main** 部分的记录展示了记录时 **JavaScript** 函数调用的调用栈详细情况。禁止这些调用栈：

1. 打开 **Capture settings** 菜单。参阅 [Show recording settings](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#settings)
2. 点击 **Disable JavaScript Samples** 的选项框
3. 然后对页面做一次记录

Figure 7 and Figure 8 展示了禁用与启用 JavaScript 示例的区别。在禁用 JavaScript 示例时，因为省略了所有 JavaScript 调用栈，所以 **Main** 部分的记录要短很多。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/js-samples-disabled.png?hl=zh-cn)

**Figure 7**. 一个禁用 JS 示例的记录栗子

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/js-samples-enabled.png)

**Figure 8**.  一个启用 JS 示例的记录栗子

##### 节流记录时的网络

为了节流记录时的网络：

1. 打开 **Capture settings** 菜单。 参阅 [Show recording settings](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#settings)
2. 设置 **Network** 到期望的节流等级

##### 节流记录时的 CPU

为了节流记录时的 CPU

1. 打开 **Capture settings** 菜单。参阅 [Show recording settings](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#settings)
2. 设置 **CPU** 到期望的节流等级

节流性能与你的电脑性能相关。举个栗子， **2x slowdown** 选项会让你的 CPU 以慢于常规情况下的 2 倍进行操作。因为移动设备的架构与桌面端电脑和笔记本千差万别，所以DevTools 无法真正模拟移动设备的 CPU。

##### 启用高级绘制工具

为了查看绘制工具的详情：

1. 打开 **Capture settings** 菜单。参阅 [Show recording settings](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#settings)
2. 选中 **Enable advanced paint instrumentation** 选项框

参阅 [View layers](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#layers) 以及 [View paint profiler](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#paint-profiler) 学习怎样与绘制信息交互。

### 保存记录

右击然后选择 **Save Profile** 来保存记录。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/save-profile.png)

**Figure 9**. **Save Profile**

### 加载记录

右击然后选择 **Load Profile** 来加载记录。

### 清除之前的记录

在做了记录之后，点击 **Clear recording** 来在 **Performance** 选项卡中清除记录。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/clear-recording.svg?hl=zh-cn)

**Figure 11**. 蓝圈全中了清除记录

### 分析性能记录

在你 [record runtime performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#record-runtime) 或 [record load performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#record-load) 之后，**Performance** 选项卡会提供很多刚记录用来分析性能的数据。

##### 选择记录中一部分

在 **Overview** 上向左或向右拖拽你的鼠标来选取一部分的记录。 **Overview** 就是那个有包含了 FPS，CPU 以及 NET 表格的区域。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/zoom.gif)

**Figure 12**. 在 Overview 上拖拽鼠标来放大或缩小

用键盘来选取一部分：

1. 点击 **Main** 区域的背景，或者其他任意靠近它的区域，比如说 **Interactions**，**Network**，或者 **GPU**。键盘的工作流程只会发生在其中某个部分被选中的时候。
2. 使用 W，A，S，D 键位来分别放大，向左移动，缩小以及向右移动。

用触控板来选取一部分：

1. 让你的鼠标悬停在 **Overview** 或者 **Details** 区域。**Overview** 部分就是那个包含有 **FPS**，**CPU** 以及 **NET** 表格的区域。**Details** 部分就是那个包含了 **Main** 部分，**Interactions** 部分以及其他部分的区域。
2. 用两个手指向上滑动来缩小，向左滑动来向左移动，向下滑动来放大，向右滑动来向右移动。

为了在 **Main** 区域上的很长一段表格上滑动或者任意与它相邻的区域，在向上和向下拖动的同时点击并按住。向左或向右拖动来移动到选中记录的任意部分。

##### 搜寻事件

按下 `Command` + `F` (Mac) 或 `Control` + `F` (windows，Linux) 来打开在 **Performance** 选项卡下方的搜索框。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/search.png)

**Figure 13**. 在窗口下方的搜索框中使用正则表达式来查找所有以 `E` 开头的活动。

导航符合你条件的活动：

1. 使用 **Previous** ![Previous](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/previous.png) 以及 **Next** ![Next](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/next.png) 按钮。
2. 按下 `Shift` + `Enter` 来选取之前的或者按下 `Enter` 选择下一个

更改查询设定：

1. 点击 **Case sensitive** ![Case sensitive](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/search-case.png) 让查找对大小敏感
2. 点击 **Regex** ![Regex](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/search-regex.png) 在查询中使用正则表达式

点击 **Cancel** 来隐藏搜索框

##### 查看主线程的活动

使用 **Main** 区域来查看发生在页面主线程上的事件。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/main.svg)

**Figure 14**. 蓝圈圈中的是 **Main** 部分

点击一个事件在 **Summary** 选项卡中查看更多关于它的信息。DevTools 会用蓝圈圈中选中的事件。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/maineventsummary.png)

**Figure 15**. **Summary** 选项卡中更多关于 `Me` 函数调用事件的信息

DevTools 会用表格显示主线程中的事件。x 轴代表了记录的时间。y 轴代表了调用栈。上方的事件会引发下方的事件。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/flamechart.png)

**Figure 16**. **Main** 区域上大量的表格

在图16中，一个 `click` 事件导致了一个在 `script_foot_clousure.js` 中的53行处的函数调用。在 `Function Call` 下方你可以看到有个匿名函数被调用。这个匿名函数然后调用了 `Me()` 然后它又调用了 `Se()`，等等。

DevTools 随机给脚本分配了颜色。在图16中，从某个脚本中调用的函数被涂上了绿色。另一个脚本文件的调用则使用了米色。深黄色代表了脚本的活动，紫色事件代表了渲染活动。这些深黄色以及紫色事件是会贯穿整个记录的。

如果你想要隐藏 JavaScript 详细的调用表格，查阅 [Disable JavaScript samples](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#disable-js-samples)  获取更多。当 JS 示例被禁用时，你只能看到一些像在图16中的 `Event(click)` 以及 `Function Call (script_foot_closure.js:53)` 的高层事件。

##### 在表格中查看活动

当记录完一个页面后，你无需完全依赖 **Main** 部分来分析活动。DevTools 还提供了三个表格式的视图用以分析活动。每一个视图都能给你这些活动不一样的视角：

- 当你想要查看导致了大量工作的 Root activities 时，请使用 [the **Call Tree** tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#call-tree) 。
- 当你想要查看耗时长的事件时，请使用 [the **Bottom-Up** tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#bottom-up) 。
- 当你想要查看记录中的事件怎样排序时，请使用 [the **Event Log** tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#event-log) 。

> 提示：下面三个部分全是用的一个 Demo。你可以用在 [Activity Tabs demo](https://googlechrome.github.io/devtools-samples/perf/activitytabs) 上运行自己的 demo 同时可以查看 [GoogleChrome/devtools-samples/perf/activitytabs.html](https://github.com/GoogleChrome/devtools-samples/blob/master/perf/activitytabs.html) 的源码。

##### Root activities

这里有个关于的在 **Call Tree** 选项卡，**Bottom-Up** 选项卡以及 **Event Log** 区域中曾提到到过得 Root activities 概念的解释。

Root activities 指的就是那些会导致浏览器会做更多事情的活动。举个栗子，当你点击一个页面时，浏览器会发出一个 `Event` 活动作为 root activity。这个 `Event` 可能会导致一个处理函数去执行，等等。

在 **Main** 区域的表格中，root activities 处于表格的顶部。在 **Call Tree** 以及 **Event Log** 选项卡中，root activities 是顶层的东西。

查阅 [The Call Tree tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#call-tree) 中关于 root activities 的栗子。

##### The Call Tree tab

使用 **Call Tree** 来查看哪个 [root activities](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#root-activities) 导致更多的工作。

**Call Tree** 只能显示在记录中选中区域的活动。查阅 [Select a portion of a recording](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#select) 来学习怎样选择区域。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/call-tree.png)

**Figure 17**. **Call Tree** 选项卡

在图 17 中，在  **Activity** 一栏中顶层的事物，比如 `Event`，`Paint` 以及 `Composite Layers` 就是 root activities。嵌套的代表了调用栈。举个栗子，在图 17 中，`Event` 会导致 `Function Call`，这会导致 `button.addEventListener`，这又会导致 `b` ，等等。

**Self Time** 代表了这个活动中直接耗费了多少的时间。 **Total Time** 代表了在这个事件中或者他的孩子共耗费了多少的时间。

点击 **Self Time**，**Total Time** 或者 **Activity** 通过该列对这个表格排序。

使用 **Filter** 文本框来通过活动名称过滤事件。

默认情况下， **Grouping** 菜单栏被设置成 **No Grouping**。使用 **Grouping** 菜单在多样的标准上对活动进行排序。

点击 **Show Heaviest Stack** 来展开另外一个在 **Activity** 表格右边的表格。点击任意一个活动来展开 **Heviest Stack** 表格。 **Heaviest Stack** 表格向你展示了哪个子事件耗费了最多的执行时间。

##### The Bottom-Up tab

使用 **Bottom-Up** 选项卡来查看哪个事件在总数上使用了大量的时间。

**Bottom-Up** 选项卡只显示在记录中选中部分的活动。查阅 [Select a portion of a recording](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#select) 来学习怎样选取部分。

![](/var/folders/7c/w93rl_1d6f57c_2jr5xxxp0w0000gn/T/abnerworks.Typora/image-20180421181641661.png)

**Figure 18**. **Bottom-Up** 选项卡

图18中 **Main** 部分中，你可以看到几乎所有的时间都执行在了三次调用 `wait()` 上。于是，图 18 中的 **Bottom-Up** 选项卡中的顶层活动的 `wait`。在图 18 中，实际上在 `wait` 调用下方黄色部分有几千次的 `Minor GC` 的调用。于是，你可以在 **Bottom-Up** 选项卡中，另一个花费了大量时间的活动是 **Minor GC**。

**Self Time** 栏代表了某个活动在他发生期间花费的总时间。

**Total Time** 栏代表了某个活动或者他的子活动的总时间。

##### Event Log 选项卡

使用 **Event Log** 选项卡来查看在记录时按顺序发生的活动。

**Event Log** 选项卡只会展示记录中选中部分的活动。查阅 [Select a portion of a recording](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#select) 来学习怎样选择部分。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/event-log.png)

**Figure 19.** **Event Log** 选项卡

**Start Time** 选项栏代表了事件开始的时间点，这与记录开始的时间有关。举个栗子，图 19 中选中部分的 `1573.0 ms` 开始时间意味着该活动在记录开始的 1573 ms 之后。

**Self Time** 栏代表了该活动耗费了多长时间。

**Total Time** 栏代表了该事件直接或它的子事件耗费了多长时间。

点击 **Start Time**， **Self Time** 或者 **Total Time** 来通过这些栏目对表格进行排序。

使用 **Filter** 文本框对活动名称进行过滤。

使用 **Duration** 菜单来过滤掉任何耗费了少于 1ms 或者 15 ms 时间的活动。默认情况下， **Duration** 菜单被设置成了 **All**，这意味着所有的活动都会呈现。

禁用 **Loading**， **Scripting**， **Rendering** 或者 **Painting** 选项卡迎来从这些种类中过滤所有活动。

##### 查看 GPU 活动

在 GPU 区域查看 GPU 的活动

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/gpu.svg)

**Figure 20.** 途中蓝圈圈中的是 **GPU** 部分

##### 查看 raster （光栅）活动

在 **Raster** 部分中查看 raster 活动。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/raster.svg)

**Figure 21.** 蓝圈全中了 **Raster** 部分

##### 查看交互事件

使用 **Interactions** 部分来查找以及分析在发生在记录时用户的交互行为。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/interactions.svg)

**Figure 22. 蓝圈全中了 ** **Interactions** 部分

交互事件下方的红线代表了主线程等待所耗费的时间。

点击一个交互事件来在 **Summary** 选项卡中查看详细信息。

##### 分析每秒的帧数（FPS）

DevTools 提供了很多的方式来分析每秒的帧数：

- 使用 [the **FPS** chart](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#fps-chart) 来得到记录时 FPS 的概览
- 使用 [the **Frames** section](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#frames) 来查看一个特定帧耗费了多长时间
- 使用 **FPS meter** 来获取实时页面运行估计的 FPS。查阅 [View frames per second in realtime with the FPS meter](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#fps-meter)

##### FPS 表格

**FPS** 表格提供了记录时帧率的概况。大体上来说，绿条越高，帧率越高。

**FPS** 表格下面的红条时一个帧率非常低的警告，这可能很可能会影响到用户体验。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/fps-chart.svg)

**Figure 20.**  蓝圈全中了 FPS 表格

##### 帧数部分

**Frame** 部分告诉了你某个帧具体耗费了多长的时间。

让鼠标悬停在一个帧上来查看关于它具体信息的提示。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/frames-section.png)

**Figure 21.** 悬停在一个帧上时

点击一个帧来在 **Summary** 选项卡上查看更多关于该帧的信息。DevTools 会用蓝圈框选选中的帧。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/frame-summary.png)

**Figure 22.** 在 **Summary** 选项卡上查看帧

##### 查看网络请求

展开 **Network** 部分来查看记录发生时网络请求瀑布流。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/network-request.svg)

**Figure 23.**  蓝圈选中了 **Network** 部分

请求会用下面的颜色对不同的文件上色：

- HTML: 蓝色
- CSS: 紫色
- JS: 黄色
- Images: 绿色

点击任意一个请求在 **Summary ** 选项卡上查看更多关于它的详情。举个栗子，在图 23 中的 **Summary** 选项卡显示了在 **Network** 中更多关于蓝色选中的请求的详情信息。

在请求左上方的深蓝色正方形意味着他是一个高优先级的请求。淡蓝色正方形则意味着低优先级。举个栗子，在图 23 中蓝色选中的请求比在它下面的绿色请求优先级更高。

在图 24 中，对 `www.google.com` 的请求通过左边的一条线，有深色和浅色区域的中间长条以及一条右边的线来表示。图 25 显示了 **Network** 面板中 **Timing** 选项卡对应请求的信息。下面是这两者之间的对应关系：

- 左边的线代包括了所有 `Connect Start` 的一系列的事件。换句话说，他不包括所有在 `Request Sent` 之前的事情。
- 长条的浅色部分是 `Request Sent` 以及 `Waiting (TTFN)`。
- 长条的深色部分是 `Content Download`。
- 右边的线本质上是等待主线程所耗费的时间。这个不会在 **Timing** 选项卡中显示出来。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/linebar.png)

**Figure 24.** `www.google.com` 请求的长条描述形式。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/timing.png)

**Figure 25.**  **Timing** 选项卡中 `www.google.com` 请求的描述形式。

##### 查看内存指标

选中 **Memory** 选项框来查看最近一次记录的内存指标。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/memory.svg)

**Figure 26.** 蓝圈全中了 **Memory** 选项框

DevTools 展示了一个新的 **Memory** 表格，在 **Summary** 选项卡上方。同时也还有一个新表格在 **NET** 表格之下，它被叫做 **HEAP**。 **HEAP** 表格提供了同样的信息就像在 **Memory** 表格中的 **JS Heap**。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/memory.png)

**Figure 27.** 位于 **Summary** 选项卡上方的内存指标

表格上有颜色的线与表格上方有颜色的选项框一一对应。点击禁用某个选项框来隐藏表格中那个类别的信息。

表格只显示记录中当前选中的区域。举个栗子，在图 27 中， **Memory** 表格只显示了记录开始时的内存使用情况，大约只有 1000ms。

##### 查看部分记录的运行时间

当你在分析像 **Network** 或者 **Main** 部分时，你可能需要更多关于事件会花费具体多长时间的精确预估。按住 `Shift` ，点击然后拖动，向左或向右拖动来选择记录的某部分。在你选择部分的下方，DevTools 会展示这个部分耗费了多长时间。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/duration.png)

**Figure 28.** 选中部分的底部的 `488.53ms` 时间戳表明了这个部分耗费了多长时间

##### 查看快照

查阅 [Capture screenshots while recording](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#screenshots) 来学习怎样启用快照。

让鼠标悬停在 **Overview** 上方来查看当前页面在记录中该时刻的快照。 **Overview** 就是那个包含有 **CPU**， **FPS** 以及 **NET** 表格的部分。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/view-screenshot.png)

**Figure 29.** 查看快照

你也可以通过点击 **Frames** 部分的一个帧来查看快照。DevTools 展示了在 **Summary** 选项卡中快照的一个小版本。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/frame-screenshot-summary.png)

**Figure 30.** 在 **Frames** 部分中点击 `195.5ms` 帧之后，该帧的快照就会显示在 **Summary** 选项卡中。

点击 **Summary** 选项卡中的缩略图来放大快照。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/frame-screenshot-zoom.png)

**Figure 31. ** 在点击 **Summary** 选项卡中点击缩略图之后，DevTools 会放大快照。

##### 查看图层信息

查看关于某个帧图层高级信息：

1. [Enable advanced paint instrumentation](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#paint)
2. 在 **Frames** 部分选择一个帧。DevTools 会在与 **Event Log** 相邻的，一个新的 **Layers** 选项卡中展示关于他的图层信息。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/layers.png)

**Figure 32.** **Layers** 选项卡

在图上，鼠标悬停在一个图层上来高亮它。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/layerhover.png)

**Figure 33.** 高亮图层 **#39**

移动图：

- 点击 **Pan Mode** ![Pan Mode](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/pan-mode.png) 来通过 x ，y 轴来移动。
- 点击 **Rotate Mode** ![Rotate Mode](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/rotate-mode.png) 来通过 z 轴旋转。
- 点击 **Reset Transform** ![Reset  Transform](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/reset-transform.png) 来重置示例图到原来的位置。

**Figure 34.** **Paint Profiler** 选项卡

### 通过 Rendering 选项卡分析渲染性能

使用 **Rendering** 选项卡的特性来帮助你可视化页面渲染性能。

打开 **Rendering** 选项卡：

1. 打开 [Command Menu](https://developers.google.com/web/tools/chrome-devtools/ui#command-menu)
2. 输入 `Rendering` 然后选择 `Show Rendering`。DevTools 会在 DevTools 窗口的下方显示 **Rendering** 选项卡。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/rendering-tab.png)

**Figure 35** **Rendering** 选项卡

##### 通过 FPS 面板来查看实时每秒的帧数

**FPS 面板** 是一个出现在你视野右上角的覆盖层。他会提供实时页面运行的 FPS 估计值。打开 **FPS 面板**：

1. 打开 **Rendering** 选项卡。查阅 [Analyze rendering performance with the Rendering tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#rendering)
2. 启用 **FPS 面板** 选项框

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/fps-meter.png)

**Figure 36.** FPS 面板

##### 通过 Paint Flashing 查看实时绘制事件

使用 Paint Flashing 来获取页面实时所有的绘制事件的视图。每当页面的任意一个部分发生了重绘，DevTools 会用绿圈圈中重绘的区域：

启用 Paint Flashing：

1. 打开 **Rendering** 选项卡。查阅 [Analyze rendering performance with the Rendering tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#rendering)
2. 启用 **Paint Flashing** 选项框

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/paint-flashing.gif)

**Figure 37.** Paint Flashing

#####  通过 Layers Borders 查看图层的叠加层

使用 **Layers Borders** 在页面顶层来查看叠加层的图层边框以及叠加情况。

启用 Layers Borders：

1. 打开 **Rendering** 选项卡。查阅 [Analyze rendering performance with the Rendering tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#rendering)。
2. 启用 **Layers Border** 选项框。

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/layer-borders.png)

**Figure 38.** Layer Borders

查阅 [`debug_colors.cc`](https://cs.chromium.org/chromium/src/cc/debug/debug_colors.cc) 中的注释来得到颜色编码的解释。

##### 查找实时的滑动性能问题

使用 **Scrolling Performance Issues** 来确认页面的元素是否有相关的事件监听会影响到页面的性能。DevTools 会圈出潜在有问题的元素。

查看滑动性能问题：

1. 打开 **Rendering** 选项卡。查阅 [Analyze rendering performance with the Rendering tab](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference#rendering)。
2. 启用 **Scrolling Performance Issues** 选项框

![](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/imgs/scrolling-performance-issues.png)

**Figure 39.** **Scrolling Performance Issues** 表明该页面存在一个 **mousewheel** 事件监听，其中包含了有损整个页面视图滑动性能的监听器。
































