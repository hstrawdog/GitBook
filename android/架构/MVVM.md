MVVM，Model-View-ViewModel，职责分类如下：

- Model，模型层，即数据模型，用于获取和存储数据。
- View，视图，即Activity/Fragment
- ViewModel，视图模型，负责业务逻辑。

> 注意，MVVM这里的ViewModel就是一个名称，可以理解为MVP中的Presenter。不等同于上一篇中的 ViewModel组件 ，Jetpack ViewModel组件是 对 MVVM的ViewModel 的具体实施方案。

MVVM 的本质是 **数据驱动**，把解耦做的更彻底，viewModel不持有view 。

View 产生事件，使用 ViewModel进行逻辑处理后，通知Model更新数据，Model把更新的数据给ViewModel，ViewModel**自动通知View更新界面**，**而不是主动调用View的方法**。

![MVVM](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1ff7967e856646fb8f72044b61e95dff~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)



在应用的各个模块之间设定**明确定义的职责界限**。

**ViewModel 不能持有 View层引用**，包括Context也不能持有。

**将一个数据源指定为单一可信来源**。 每当需要访问数据时，都应一律源于此单一可信来源。 例如 UserRepository会将网络服务响应保存在数据库中。这样一来，对数据库的更改将触发对活跃 LiveData 对象的回调。**数据库会充当单一可信来源**。

保留尽可能多的相关数据和最新数据。 这样，即使用户的设备处于离线模式，他们也可以使用您应用的功能。请注意，并非所有用户都能享受到稳定的高速连接。

显示页面状态。 例如例子中的加载进度条，就是观察 ViewModel中的MutableLiveData loadingLiveData 进行操作的。



# 补充

一、ViewModel 和 View 职责分离，ViewModel中处理业务逻辑，View 仅展示数据及传递事件

二、ViewModel 不引用 View 及 Context

三、View 通过 LiveData 观察数据变化，不是直接向View 推送数据

四、ViewModel中 除了 业务 LiveData 外，还应该提供 LiveData，表示数据 是加载中、加载成功、加载失败。

五、使用SingleLiveEvent  来传递 事件类消息：仅在显式调用setValue()或call()时 才会通知观察者；只有一个观察者会收到更改通知。

六、ViewModel 和 Repository 之间，建议 使用 LiveData 进行通信，就像 View 和 ViewModel 之间那样  使用回调的话，可能会有内存泄漏的风险。 并且在[ViewModel中 使用 Transformations.switchMap](https://juejin.cn/post/6844903509893054471#heading-11) 把 生命周期信息 传递到 Repository 的 LiveData 中。

七、DataBinding中绑定的数据 直接使用 LivaData 即可， 而不是 BaseObservable

八、xml中尽量只定义一个variable，那就是 页面对应的 ViewModel ，控件直接绑定 LivaData 的字段

九、XML 中尽量 不使用逻辑表达式，把逻辑放在 ViewModel 中，控件绑定终态数据


作者：胡飞洋
链接：https://juejin.cn/post/6923859213403979789