#			Activity

https://www.jianshu.com/p/86c0a4afd28e

https://blog.csdn.net/weixin_44339238/article/details/103977138

##				生命周期

1. 					onCreate 
1. 					onStart 
1. 					onResume 
1. 					onPause 
1. 					onStop 
1. 					onDestroy 
1. 					onRestart 
1. 					onNewIntent
1. 					onSavaInstanceState 
1. 					onRestoreInstanceState  

##	 				四种启动模式

1. 					默认启动模式standard：
1. 					栈顶复用模式singleTop：
1. 					栈内复用模式singleTask：
1. 					全局唯一模式singleInstance：

##	 				用Intent传递数据和Bundle传递数据的区别

两者本质上没有任何区别。
Bundle只是一个信息的载体 将内部的内容以键值对组织 
Intent负责Activity之间的交互 自己是带有一个Bundle的
Intent.putExtras(Bundle bundle)直接将Intent的内部Bundle设置为参数里的bundle
Intent.getExtras()直接可以获取Intent带有的Bundle

##	 				Activity可以设置为对话框的形式吗

可以

[参考](https://cloud.tencent.com/developer/article/1151676)

##	 				Activity与Fragment的关系

1. 					Fragment可作为Activity的界面组成部分，可在Activity运行中动态的实现加入、移除和交换。
1. 					一个Activity可以拥有多个Fragment，一个Fragment也可以依附于多个Activity。
1. 					Activity的FragmentManager负责调用队列中的Fragment的生命周期方法，只要Fragment的状态与Activity的状态保持一致，宿主Activity的FragmentManager就会继续调用其他生命周期方法以保持Fragment和Activity的状态一致。

##	 				优先级低的Activity在内存不足被回收后怎样做可以恢复到销毁前状态

##	 				如何启动其他应用的Activity

另一个程序中的Activity要能够被启动，首先这个Activity在manifest的声明中必须具有<intent-filter>属性。否则将不能被启动。

我们必须知道：Android程序中Context分成两种。一种是**Activity Context**，另一种是**Application Context**。通过Activity Context来启动另一个程序代码是很简单。代码如下。

```
Intent i = new Intent();
    	i.setClassName("packagename", "classname");
    	startActivity(i);
```

但是如果通过Application Context来启动Activity的话。就需要FLAG_ACTIVITY_NEW_TASK属性，不管这个Activity是属于其他程序还是自己这个程序的。

```
Intent i = new Intent();
    	i.setClassName("packagename", "classname");
    	i.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);//必须添加
    	getApplicationContext().startActivity(i);
```

这样的话会把启动的程序放到一个新的TASK中。

##	 				Activity的启动过程

##	 				intent传递有没有大小限制，是多少？

Intent携带信息的大小其实是受Binder限制

数据以`Parcel`对象的形式存放在Binder传递缓存中。 如果数据或返回值比传递buffer大，则此次传递调用失败并抛出`TransactionTooLargeException`异常。

Binder传递缓存有一个限定大小，通常是1Mb。但同一个进程中所有的传输共享缓存空间。

多个地方在进行传输时，即时它们各自传输的数据不超出大小限制，`TransactionTooLargeException`异常也可能会被抛出。

在使用Intent传递数据时，1Mb并不是安全上限。因为Binder中可能正在处理其它的传输工作。 不同的机型和系统版本，这个上限值也可能会不同。

https://juejin.im/post/5caa01b15188254aa83f8154

## Activity何时销毁何时回收

onDestory销毁 回收需要等系统gc

# 横竖屏切换的Activity生命周期变化

# 如何启动其他应用的Activity

# Activity的启动过程