# Android 12 (31) : S

## android:exported

**它主要是设置 `Activity` 是否可由其他应用的组件启动**， “`true`” 则表示可以，而“`false`”表示不可以。

当然不止是 `Activity`， `Service` 和 `Receiver` 也会有 `exported` 的场景。

**一般情况下如果使用了 `intent-filter`，则不能将  `exported` 设置为“`false`”**，不然在 `Activity` 被调用时系统会抛出 `ActivityNotFoundException` 异常。



## SplashScreen

Android 12 新增加了 [`SplashScreen`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.android.com%2Freference%2Fandroid%2Fwindow%2FSplashScreen) 的 API，它包括启动时的进入应用的动作、显示应用的图标画面，以及展示应用本身的过渡效果

它大概由如下 4 个部分组成，这里需要注意：

 1. 最好是矢量的可绘制对象，当然它可以是静态或动画形式。
 1. 是可选的，也就是图标的背景。
 1. 与自适应图标一样，前景的三分之一被遮盖 (3)。
 1. 就是窗口背景。

启动画面动画机制由进入动画和退出动画组成。
	1. 进入动画由系统视图到启动画面组成，这由系统控制且不可自定义。
	1. 退出动画由隐藏启动画面的动画运行组成。如果要[对其进行自定义](https://developer.android.com/guide/topics/ui/splash-screen#customize-animation)，可以通过 [`SplashScreenView`](https://developer.android.com/reference/android/window/SplashScreenView) 自定义。

[参考](https://juejin.cn/post/7037105000480243748/)



1. 后台服务不能启动前台服务(加了限制 比如activity处于可见状态、应用相关页面元素执行操作与通知、气泡、微件 或activity有互动、用户已授权添加为白名单权限并且导向用户停止该应用的电池优化界面、广播接收器接收了ACTION_BOOT_COMPLETED intent 操作之后等等

1. 以android12为目标平台的含使用intent过滤器的activity与服务、广播 需要加android:exported声明 为false就好（否则android12不能安装）

1. 应用以不安全的方式启动嵌套intent

1. 比如intent的extra中解封嵌套了intent

1. 应用使用了嵌套intent的组件
    调用detectUnsafeIntentLaunch()即可解决

1. 通知中心

1. ndroid App Links 验证

1. 安全和隐私设置

1. SameSite Cookie

1. 应用休眠

1. PendingIntent

1. 麦克风和摄像头切换开关

1. **待处理 intent 可变性**

1. **前台服务启动限制**

1. **精确的闹钟权限**

1. **应用休眠**

1. **自定义通知**

1.  

     [适配参考](https://mp.weixin.qq.com/s/rA-1f8aa4PzjFuD6EIA7jw)

     
