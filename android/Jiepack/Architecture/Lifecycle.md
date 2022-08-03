Lifecycle，顾名思义，是用于帮助开发者管理Activity和Fragment 的生命周期，它是LiveData和ViewModel的基础。

https://juejin.cn/post/6893870636733890574#heading-10







Lifecycle使用非常非常简单。默认你已经使用过Lifecycle。但如果我问你以下几个问题。你能回答出来几个？

- Lifecycle的创建方式有几种？
- 有什么不同？推荐使用哪种？为什么？
- Event事件和State状态是什么关系
- nStop()生命周期，处于什么State状态
- Lifecycle是如何进行生命周期同步
- 如果在onResume() 注册观察者会收到那几个种回调？为什么？
- Activity/Fragment 实现Lifecycle能力的方式一样吗？
- 为什么要这么设计？有什么好处？
- Application能感知Activity生命周期吗?（如何使用Lifecycle监听前后台的能力）
- Lifecycle从源码角度，简述Lifecycle的注册，派发，感知的过程
- 什么嵌套事件？发生的时机？Lifecycle是如何解决的？