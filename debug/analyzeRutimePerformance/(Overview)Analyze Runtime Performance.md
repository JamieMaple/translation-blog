# Analyze Runtime Performance

### 内容

1. JavaScript
   - 工具
   - 问题
2. Style (样式)
   - 工具
   - 问题
3. Layout (布局)
   - 工具
   - 问题
4. Paint (绘制) and Composite (复合)
   - 工具
   - 问题

用户都希望页面能够交互且流畅。像素管道的任何一个阶段都可能引入问题（jank）。学习一些工具和策略来发现并解决这些让运行时性能变差的常见问题。

TL;DR

- 不要写让浏览器重新计算 layout (布局)的 JS 代码。分离读写的函数，然后让读取的函数先执行。
- 不要让你的 CSS 过于复杂。用尽量少的 CSS 同时让你的 CSS 选择器尽可能简单。
- 尽可能避免 layout。选择那些根本上不会引发布局的 CSS 代码。
- 绘制比其他的渲染活动更耗费时间。注意绘制会有的瓶颈。

### JavaScript

JavaScript 计算，尤其是那些会触发页面大范围可视化的改动，这会严重影响到页面的性能。

##### 工具

做一次 **Timeline** [录制]((https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool#make-a-recording))同时查找可能导致 **Evaluate Script** 的事件。如果你发现任何可能的事件，你可以打开 [JS Profiler](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool#profile-js) 同时重新开始你的录制来获取更多关于哪个 JS 函数被调用以及被每个函数被调用了多长时间的详情。

如果你注意到了 JavaScript 一些的卡顿情况，你可能需要做进一步分析收集你 JavaScript CPU profile（配置信息）。CPU 的 profiles 向你展示了页面上哪些函数耗费了多少时间。学习怎样在 [Speed Up JavaScript Execution](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/js-execution) 中创建 CPU profiles。

##### 问题

下面的表格向你描述了一些常见的 JavaScript 问题以及可行的解决方案：

| Problem                                        | Example                                                      | Solution                                                     |
| ---------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 性能开销很大的输入处理函数会影响到响应以及动画 | 触摸，视差，滑动                                             | 让浏览器尽可能晚的去处理触摸和滑动，或者绑定监听器（参阅 [Expensive Input Handlers in Paul Lewis' runtime performance checklist](http://calendar.perfplanet.com/2013/the-runtime-performance-checklist/)） |
| 时间不当的 JavaScript 会影响到响应，动画，加载 | 在页面加载后用户的滑动，setTimeout/setInterval               | [Optimize JavaScript execution](https://developers.google.com/web/fundamentals/performance/rendering/optimize-javascript-execution)： 使用 **requestAnimationFrame**，在不同的帧里面分离操作，使用 Web Workers |
| 响应后长时间运行 JavaScript                    | 过多的 JS 工作让 [DOMContentLoaded event](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 拖延了很长时间 | 在  [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 中使用纯净的计算、如果你需要访问 DOM，那么请使用 **requestAnimationFrame** （参阅 [Optimize JavaScript Execution](https://developers.google.com/web/fundamentals/performance/rendering/optimize-javascript-execution)） |
| 某些脚本生成垃圾，影响到了响应或动画           | 垃圾收集可能随时发生                                         | 写少量会产生垃圾的脚本代码（参阅  [Garbage Collection in Animation in Paul Lewis' runtime performance checklist](http://calendar.perfplanet.com/2013/the-runtime-performance-checklist/)） |

### Style

样式的改变是非常昂贵的，尤其是那些会影响到不止一个 DOM 元素的改变。你给元素样式的任何改变，浏览器都得查明对相关元素的所有影响，重新计算布局然后再重绘。

相关指南：

- [Reduce the Scope and Complexity of Styles Calculations](https://developers.google.com/web/fundamentals/performance/rendering/reduce-the-scope-and-complexity-of-style-calculations)

##### 工具

做一次 **Timeline** 的记录。查找引起大量 **Recalculate Style** 的事件（显示颜色为紫色的）。

点在 **Details** 窗口中，击任意一个 **recalculate Style** 事件来查看关于它更多的信息。如果这个样式改变确实用了非常多的时间，那么它会非常影响性能了。如果这个样式的计算影响到了非常多的元素，那么这又有很多地方做性能优化。

![](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/imgs/recalculate-style.png)

为了减少 **Recalculate Style** 事件的影响：

- 阅读 [CSS Triggers](https://csstriggers.com/) 来了解哪些 CSS 属性会触发 layout（布局），paint（绘制）以及 composite （复合）
- 取而代之使用另外一些产生更少影响的属性。 参阅 [Stick to compositor-only properties and manage layer count](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count) 来获得更多指南。

##### 问题

下面的表格面描述了一些常见的样式问题以及可行的解决方案：

| Problem                                    | Example                                                      | Solution                                                     |
| ------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 性能开销大的样式计算会影响到页面响应或动画 | 任何会改变一个元素几何形状的 CSS 属性，比如它的宽高或者位置；浏览器必须检查所有其他元素的情况然后重新布局 | [Avoid CSS that triggers layouts.](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing) |
| 复杂的选择器会影响到响应或动画             | 嵌套的选择器强制浏览器去了解更多关于其他元素的所有信息，包括他的父子级 | [Reference an element in your CSS with just a class.](https://developers.google.com/web/fundamentals/performance/rendering/reduce-the-scope-and-complexity-of-style-calculations) |

相关指南：

- [Reduce the Scope and Complexity of Styles Calculations](https://developers.google.com/web/fundamentals/performance/rendering/reduce-the-scope-and-complexity-of-style-calculations)

### Layout

Layout（布局，在火狐中我们称为 reflow）是通过浏览器在一个页面上计算所有元素的位置和大小的过程。网页的布局意味着任意一个元素都会影响到其他元素；举个栗子，`<body>` 元素的宽度一般都会影响到他子元素的宽度，也会影响到树中的任意处节点，等等。这个过程与浏览器息息相关。

从一般经验法则来说，如果你在一个帧完成前，对某个 DOM 查询几何形状相关的具体数值，你就会很快发现你在“强制同步布局”，如果频繁重复这样的行为或者在一个很大的 DOM 树中执行这样的操作，将会出现一个很大的性能瓶颈。

相关指南：

- [Avoid Layout Thrashing](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing)
- [Diagnose Forced Synchronous Layouts](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/forced-synchronous-layouts)

##### 工具

Chrome DevTools **Timeline** 将会确认何时页面产生了强制同步布局的行为。这些**布局**事件会被用红线标记。

![](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/imgs/forced-synchronous-layout.png)



"布局抖动"(layout thrashing) 是一个反复强制同步布局的条件。它当在 JavaScript 从 DOM 中反复读写时出现，这会强制浏览器不断的重新计算布局。为了确认是否出现了布局抖动，查找是否出现了有多次强制同步布局大量警告的图案（就像上面的截图的那样）。

##### 问题

下面的表个人描述一些常见的布局问题以及可行的解决方案：

| Problem                      | Example                                                      | Solution                                                     |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 强制同步布局会影响响应或动画 | 强制浏览器在像素通道中过早的执行布局，会导致在渲染过程中多次反复布局 | 批量一次性读取你的样式，然后再做写入操作（参阅  [Avoid large, complex layouts and layout thrashing](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing)） |
| 布局抖动会影响响应或动画     | 一个让浏览器陷入反复读写的循环将会强制让浏览器反复重新计算布局 | 使用 [FastDom library](https://github.com/wilsonpage/fastdom) 自动管理读写操作 |

### Paint and composite

绘制（Paint）是一个填充像素的过程。它经常是渲染过程中最耗时的部分。如果你已经注意到了你页面的卡顿，你很有可能有绘制方面的问题。

复合（composite）是把绘制出来的页面部分放在一起显示在屏幕上。对于大多数的情况，如果你坚持要使用只会引起页面合成的属性并且同避免使用引起绘制的属性一起，你应该会看到一个在性能方面很大的提升，但是你需要注意过多的图层（layer）的数量（查阅[Stick to compositor-only properties and manage layer count](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)）

##### 工具

你想知道绘制花了多长时间么以及重绘多久会发生一次么？在 **Timeline** 面板启用 [Paint profiler](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool#profile-painting) 然后 [做一次记录](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool#make-a-recording)。如果你渲染大多数时间花费在绘制上，那么此时在绘制方面存在问题。

![](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/imgs/long-paint.png)

请检查 [**rendering settings**](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool#rendering-settings) 菜单来看更多能帮助你诊断绘制问题的配置。

##### 问题

下面的表格描述了一般绘制与复合的问题以及可行的解决方案：

| Problem                                       | Example                                                      | Solution                                                     |
| --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 大量的绘制会影响响应或动画                    | 大范围的绘制或者开销大的绘制会影响到响应或动画               | 避免重绘，让元素移动到他们自己的图层以提升页面元素，使用 transform 以及 opacity （查阅 [Simplify paint complexity and reduce paint areas](https://developers.google.com/web/fundamentals/performance/rendering/simplify-paint-complexity-and-reduce-paint-areas)） |
| 图层爆炸（layers explosions）会影响页面的动画 | 使用`translateZ(0)` 过多地提升了大量的元素会对页面的动画性能有非常大的影响 | 谨慎地添加图层，而且当前仅当这样确实能获得明显的提升（查阅 [Stick to composite-only properties and manage layer count](https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count)） |















