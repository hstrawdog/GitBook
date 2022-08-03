MVC，Model-View-Controller，职责分类如下：

- Model，模型层，即数据模型，用于获取和存储数据。
- View，视图层，即xml布局
- Controller，控制层，负责业务逻辑。

View层 接收到用户操作事件，通知到 Controller 进行对应的逻辑处理，然后通知 Model去获取/更新数据，**Model 再把新的数据 通知到 View 更新界面**。这就是一个完整 MVC 的数据流向。

但在Android中，因为xml布局能力很弱，View的很多操作是在Activity/Fragment中的，而**业务逻辑同样也是写在Activity/Fragment中**。

![MVC](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/448de00695bd4fee8aa3e39848123d95~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)

所以，**MVC 的问题点** 如下：

1. Activity/Fragment 责任不明，同时负责View、Controller，就会导致其中代码量大，不满足单一职责。
2. Model耦合View，View 的修改会导致 Controller 和 Model 都进行改动，不满足最少知识原则。


作者：胡飞洋
链接：https://juejin.cn/post/6921321173661777933/
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。