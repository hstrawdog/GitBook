MVP，Model-View-Presenter，职责分类如下：

- Model，模型层，即数据模型，用于获取和存储数据。
- View，视图层，即Activity/Fragment
- Presenter，控制层，负责业务逻辑。

MVP解决了MVC的问题：1.View责任明确，逻辑不再写在Activity中，而是在Presenter中；2.Model不再持有View。

View层 接收到用户操作事件，通知到Presenter，Presenter进行逻辑处理，然后通知Model更新数据，Model 把更新的数据给到Presenter，Presenter再通知到 View 更新界面。

![MVP](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8a7b61dbb3454d969777f02e88256ff6~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)

MVP的实现思路：

- UI逻辑抽象成IView接口，由具体的Activity实现类来完成。且调用Presenter进行逻辑操作。
- 业务逻辑抽象成IPresenter接口，由具体的Presenter实现类来完成。逻辑操作完成后调用IView接口方法刷新UI。

MVP 本质是**面向接口编程，实现了依赖倒置**原则。MVP解决了View层责任不明的问题，但并没有解决代码耦合的问题，View和Presenter之间相互持有。

所以 MVP 有**问题点** 如下：

1. 会引入大量的IView、IPresenter接口，增加实现的复杂度。
2. View和Presenter相互持有，形成耦合。


作者：胡飞洋
链接：https://juejin.cn/post/6921321173661777933/
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。