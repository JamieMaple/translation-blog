# Understanding REST(Representational State Transfer)

![](https://cdn-images-1.medium.com/max/1200/1*EbBD6IXvf3o-YegUvRB_IA.jpeg)

### REST 是什么

REST 是 Representational State Transfer 的缩写。

一个简单的 REST 定义可能下面这样：

> Examination of the Internet as a stateless service of near-limitless expansion model with a simple but effective information delivery system.

#### 使用 REST 架构的网站

Amazon, Yahoo, Google (Search), Flickr, Facebook, Myspace, LinkedIn, Microsoft, Ebay 等等。。。

### 定义

> REST is intended to evoke an image of how a well-designed Web application behaves: a network of web pages (a virtual state-machine), where the user progresses through an application by selecting links (state transitions), resulting in the next page (representing the next state of the application) being transferred to the user and rendered for their use.
>
> [- Roy Fielding in his Ph.D. dissertation in the year 2000](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

### REST 风格是什么样子的

REST 经常被描述成一种架构风格。

它能够被描述成一套用来创建体系结构的正式以及非正式的指导的集合——“约束”：

- 客户端-服务器
- 无状态
- 可缓存
- 统一接口
- 分层系统
- 按需编码（可选）

当我们使用 REST 风时，应用只需与资源交互的时候做两件事：

- 资源标识符
- 对资源执行的操作
- ….

理解 REST 风架构的限制

##### 1. 客户端服务端

分离最要关心的是客户端-服务端背后限制的原则。通过分离用户接口与数据存储，我们可以提高使用多种多样平台的用户接口以及提高扩展性以简化服务端功能的可能性。

![](https://cdn-images-1.medium.com/max/1600/1*_Bc3-FKtaV--gfh2QftNrg.png)

​						Client Server Model

##### 2. 无状态

无状态意味着(客户端与服务端之间的)对话必须是无状态的，如 `client stateless server style`。每一个从客户端到服务端请求都必须包含所有对(服务端)理解请求必要的信息，同时也不能利用在服务端上任何存储的上下文信息。 **因此会话的状态必须完整的保留在客户端上**。

![](https://cdn-images-1.medium.com/max/1600/1*Ztyoi5oUwujgoRpBqP3KDw.png)

​						Client Stateless Server

##### 3.可缓存

为了提高网络的利用效率，REST 风添加了缓存的限制。

缓存限制要求任何对请求做出响应的数据都必须显式或隐式标明 cacheable 还是 non-cacheable。如果一个响应式可缓存的，那么当客户端之后发起等效请求时，其缓存就有了重用之前请求数据的权利。

##### 4. 统一接口

区分 REST 风格与其他网络的风格的核心特征就是它强调组件间的统一接口。

资源仅仅只是通过 URI 定位的概念。URI 能够告诉客户端它在哪。然后客户端从服务器端找到它的表现形式。

E.g. 网页就是一种资源的表现形式。

##### 5. 分层系统

为了进一步适应互联网快速发展的需求，我们添加了分层系统约束。

分层系统风格允许通过约束组件行为的不同等级层组合成的系统架构，使得与每个组件的直接交互层都是"透明的"。

##### 6. 按需编码

最后要添加进我们 REST 集合中的约束来自按需编码的风格。

REST 允许客户端通过下载和执行 applets 或 script 代码来进行功能性扩展。

这通过减少预先需要实现的特性来简化了客户端。允许开发后通过下载的方式扩展的特性提高了系统的可扩展性。

### 创建 RESTful 服务

##### 步骤

1. 定义域名和数据
2. 组织数据进行分组
3. 创建资源映射的 URI
4. 定义客户端的表现形式 （XML, HTML, CSS...）
5. 通过资源链接数据（连通性或超媒体）
6. 创建用例映射到事件/使用方法
7. 对可能出错的事情进行规划















