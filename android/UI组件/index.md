### View绘制原理

主要是分析measure,layout,draw的过程,之前写过一篇比较完整的,如下.

[死磕Android_View工作原理你需要知道的一切](https://link.juejin.cn/?target=https%3A%2F%2Fblog.csdn.net%2Fxfhy_%2Farticle%2Fdetails%2F90270630)



### View,SurfaceView

- View是Android中所有控件的基类
- View适用于主动更新的情况，而SurfaceView则适用于被动更新的情况，比如频繁刷新界面。
- View在主线程中对页面进行刷新，而SurfaceView则开启一个子线程来对页面进行刷新。
- View在绘图时没有实现双缓冲机制，SurfaceView在底层机制中就实现了双缓冲机制。

