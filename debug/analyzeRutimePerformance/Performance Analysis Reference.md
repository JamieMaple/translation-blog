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

在你 [record runtime performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#record-runtime) 或 [record load performance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference?hl=zh-cn#record-load) 之后，





