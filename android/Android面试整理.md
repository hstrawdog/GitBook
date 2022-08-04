
<!-- toc -->

#  面试资源
1. https://juejin.im/post/5c7fe0e4e51d4541d82d9cd6
2. https://juejin.im/post/5c81db916fb9a049d37fe6a1#heading-10

# Java基础
1. String,StringBuffer,StringBuilder区别
```
String：适用于少量的字符串操作的情况
StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况
StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况
```
2. StringBuilder、StringBuffer、+、String.concat 链接字符串
	- StringBuffer 线程安全，StringBuilder 线程不安全
	- +实际上是用 StringBuilder 来实现的，所以非循环体可以直接用 +，循环体不行，因为会频繁创建 StringBuilder
	- String.concat 实质是 new String ，效率也低，耗时排序：StringBuilder < StringBuffer < concat < +
3.  [java泛型](https://juejin.im/post/5d03380ae51d455a694f9510)
	- 泛型中? extent 与 ? super
	- 	泛型的擦除
4. 判断一个对象是否可被回收
	1. 引用计数法
	2. 可达性分析法
5. 四种引用类型
	1. 强引用：不会被回收
	2. 软引用：内存不足时会被回收
	3. 弱引用：gc 时会被回收
	4. 虚引用：无法通过虚引用得到对象，可以监听对象的回收
6. [谈final、finally、finalize有什么不同？](https://mp.weixin.qq.com/s?__biz=MzI3OTU0MzI4MQ==&mid=2247488187&idx=1&sn=66d23fc417a8b9ddfa7f319ca66cac96&chksm=eb477e25dc30f7334ac0ee49ce43905f33e0b9b439543d34890dfea4bc5c537bfc764c33bd67&scene=0&xtrack=1&key=f75c0be8c395a44950a6d180b10cac0ef42540510b7ea03652d313d366e3e3632587c142d72273aa756a687e4f15bc683987d04914421ff75b03a80e1afea1d5b958c48b46ba97ffc25528d7e9722f95&ascene=1&uin=MTQ0NTQ2Mjgw&devicetype=Windows+7&version=62060833&lang=zh_CN&pass_ticket=Smx%2FiGtCk8a0SA8Gb6TTkH03%2FsG9JkNxGOgz9JeuQ9A%3D)
7. 锁的种类
	悲观锁、乐观锁  自旋锁、适应性自旋锁
	

[来源](https://www.cnblogs.com/su-feng/p/6659064.html)
# Android
## Activity
 1. Activity 的工作过程
2. Window 和WindowManager 
3. Activity的启动模式
	- standard标准模式
	- singleTop栈顶复用模式
	- singleTask栈内复用模式：
	- singleInstance单实例模式

4.  singleInstance启动模式下startActivityForResult 的回调问题
	```
	 ActivityA -> ActivityB-> ActivityC-> ActivityD 
	```
	C是独立栈的  D finish后是回到B 中

[来源](https://juejin.im/post/5c8211fee51d453a136e36b0#heading-5)

5. Activity 生命周期
 ```
	onCreate()-> onRestart()->onStart()->onResume()->onPause()->onStop()->onDestroy()
 ```
[来源](https://juejin.im/post/5c8211fee51d453a136e36b0#heading-5)

6. Activity非7个常用生命周期方法
	- onSaveInstanceState 
	- onRestoreInstanceState
	- onNewIntent 
	
		  Singletop:如果任务栈的栈顶已经存在这个activity的实例, 不会创建新的activity,而是利用旧的activity实例 调用 旧的activity的onNewIntent()方法
7. 


## 拍照、相册
## Service
## RecycleView 
   - 第三方adapter  BRVAH
   -  如何实现下拉刷新与上拉加载

## 进程与多线程相关
1. Android中多线程的实现方式
	1. 继承Thread类
	2. 实现Runnable接口
	3. [Handler](#Handler)
	4. [AsyncTask](#AsyncTask)
	5. HandlerThread

2. 进程与线程的区别
3. 进程优先级
	1.前台进程 ；2.可见进程；3.服务进程；4.后台进程；5.空进程
4. 如何实现进程保活
	开启一个像素的Activity
	使用前台服务
	多进程相互唤醒
	JobSheduler唤醒
	粘性服务&与系统服务捆绑
5. 线程池种类


<p id='Handler'></p>
1.  

1. View 与ViewGroup 有什么区别
2. [View 的事件分发](https://www.jianshu.com/p/ea0108d8510e)
	- public boolean dispatchTouchEvent(Motion e)
	- public boolean onDispatchTouchEvent(Motion e)
	- public boolean onTouchEvent(MotionEvent event)
	主要流程Activity ViewGroup   迭代View 
3. Activity的事件分发
###  自定义View/ 动画
1. View 的绘制流程/生命周期
2. Android [动画的种类](https://blog.csdn.net/shedoor/article/details/81251849)


### EditText 
1. 键盘遮挡问题
###   TextView
1. TextView字体周围的空白
	 清除TextView字体周围的空白部分 大约是2px  貌似和不用的dpi 是有关系的
	 android:includeFontPadding 
2.  [富文本]( https://blog.csdn.net/liuweiballack/article/details/47962361?tdsourcetag=s_pctim_aiomsg)
## IPC (Inter-Process Communication，进程间通信）
	- [如何选择合适的ipc方式](https://www.jianshu.com/p/b2a5ac1b9170)
	  广播应该也是可以的
## 第三方框架 
   - Glide

    	* glide的图片三级缓存
    - BRVAH
    	
    - Retrofit
    	* 常用注解 
    	* 如何实现文件上传
    	* 动态配置请求地址/ 多个请求地址
    - Arouter 
    	* 组件之间的通信 
    		通过继承与实现实现IProvider 进行通信
    - OkHttp
    	* 如何设置代理 
    		通过new Proxy()   build.proxy()进行设置
    	* 拦截器能做什么
    	* 请求是同步的还是异步的 / 如何进行异步请求
## 网络相关/Http/Https/Socket/UDP
1. POST 和 GET 区别
	Get 参数放在 url 中；Post 参数放在 request Body 中
    Get 可能不安全，因为参数放在 url 中
2. TCP 三次握手与四次挥手
##  布局按钮与键盘
	目前项状态适配不允许使用     android:fitsSystemWindows="true"
	[在 windowSoftInputMode 无效的情况下 ]( https://www.jianshu.com/p/fd46d6924b78)
	[或者设置 windowSoftInputMode]( https://mp.weixin.qq.com/s/xmlyHOpZNSI8o3EX73S9sw)
## 状态栏适配 
	 全屏  隐藏状态栏背景 
	 在状态栏下面添加一个 状态栏一样大小的View
	[参考来源]( https://juejin.im/post/5a30f1535188251c11409d77)
### 3. Builder模式

## [模块化开发 微信.api模式  ](https://blog.csdn.net/qiansg123/article/details/80130346)
## [第三方bug修复 transform  ASM ](https://www.jianshu.com/p/9039a3e46dbc)




