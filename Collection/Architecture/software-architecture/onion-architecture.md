# Onion Architecture (洋葱架构)

原文: https://www.jianshu.com/p/d87d5389c92a

这篇文章是[软件架构编年史](https://herbertograca.com/2017/07/03/the-software-architecture-chronicles/)([译](https://www.jianshu.com/p/b477b2cc6cfa))的一部分，这部编年史由[一系列关于软件架构的文章](https://herbertograca.com/category/development/series/software-architecture/)组成。在这一系列文章中，我将写下我对软件架构的学习和思考，以及我是如何运用这些知识的。如果你阅读了这个系列中之前的文章，本篇文章的的内容将更有意义。

`2008` 年 `Jeffrey Palermo` 提出了 [`洋葱架构`](http://jeffreypalermo.com/blog/the-onion-architecture-part-1/)。在我看来，它在端口和适配器架构的基础上贯彻了将领域放在应用中心，将传达机制(UI)和系统使用的基础设施(ORM、搜索引擎、第三方 API...)放在外围的思路。但是它前进了一步，在其中加入了内部层次。

我们从通常拥有四个层次(表现层、应用层、领域层、持久化层)的分层架构发展到了端口和适配器架构，它只是含蓄地提到了两个同心圆层次：

1. 代表传达机制和基础设施的外层；

2. 代表业务逻辑的内层。

端口和适配器架构与洋葱架构有着相同的思路，它们都通过编写适配器代码将应用核心从对基础设施的关注中解放出来，避免基础设施代码渗透到应用核心之中。这样应用使用的工具和传达机制都可以轻松地替换，可以一定程度地避免技术、工具或者供应商锁定。

另外，它还有着脱离真实基础设施和传达机制应用仍然可以运行的便利，这样可以使用 mock 代替它们方便测试。

然而，洋葱架构还告诉我们，企业应用中存在着不止两个层次，它在业务逻辑中加入了一些在领域驱动设计的过程中被识别出来的层次：

![](../../../Assets/Collection/Architecture/software-architecture/onion-architecture/001.png)

此外，它明确了端口和适配器架构中关于依赖方向的暗示：

- 外层依赖内层；

- 内层对外层无感知。

也就是说耦合的方向是从外层指向中心，它提供了一个完全独立的对象模型(领域模型)，该模型位于架构的核心，不依赖其它任何层次。我们拥有了在不影响内层的情况下改变外层的灵活性。它在架构层面运用了依赖倒置原则。

> 洋葱架构的关键原则：
> 
> 围绕独立的对象模型构建应用
> 内层定义接口，外层实现接口
> 依赖的方向指向圆心
> 所有的应用代码可以独立于基础设施编译和运行
>
> —— Jeffrey Palermo 2008, [The Onion Architecture: part 3](http://jeffreypalermo.com/blog/the-onion-architecture-part-3/)

还有，任何一个外部层次都可以直接调用任何一个内部层次，这样既不会破坏耦合的方向，也避免了仅仅为了追求分层模式而创建一些没有任何业务逻辑的代理方法甚至代理类。这和 Martin Flowler 表达的偏好一致。

> 上层可以使用它们下面的任意层次，而不仅仅是它们直接的下层。
>
> ——Jeffrey Palermo 2008, [The Onion Architecture: part 3](http://jeffreypalermo.com/blog/the-onion-architecture-part-3/)

总结
洋葱架构在端口和适配器架构的基础之上增加了一些的应用业务逻辑的内部组织，这些组织基于领域驱动设计的概念划分的。

这又是一次职责分离的更深入的演化，带来了高内聚低耦合，反过来也带来了更好的可测试性和可维护性。


## 引用来源

2002 – Martin Fowler – [Patterns of Enterprise Application Architecture](https://www.amazon.com/dp/0321127420/ref=wl_it_dp_o_pC_nS_ttl?_encoding=UTF8&colid=CG11VVP0H8Y8&coliid=I1QPWUPW6G7YF5)

2008 – Jeffrey Palermo – [The Onion Architecture: part 1](http://jeffreypalermo.com/blog/the-onion-architecture-part-1/)

2008 – Jeffrey Palermo – [The Onion Architecture: part 2](http://jeffreypalermo.com/blog/the-onion-architecture-part-2/)

2008 – Jeffrey Palermo – [The Onion Architecture: part 3](http://jeffreypalermo.com/blog/the-onion-architecture-part-3/)

2013 – Jeffrey Palermo – [The Onion Architecture: part 4 – After Four Years](http://jeffreypalermo.com/blog/onion-architecture-part-4-after-four-years/)
