### Handler与多线程





#### 实现多线程的方式
#### Hander
1. Hander如何避免内存泄漏
	* 匿名内部类持有外部类引用
	* 谨慎使用static
	* 使用Leakcannary
1. Handler Loop MessageQuery 之间的关系
1. Handler中Loop 为什么不会阻塞
1. 子线程一定不能更新UI吗
1. 使用Handler的postDealy后消息队列有什么变化
1. 可以在子线程直接new一个Handler出来吗
1. 为什么系统不建议在子线程访问UI
1. 一个Thread可以有几个Looper？几个Handler
1. IdleHandler 当线程处于空置状态下才执行

#### AsyncTask
1. AsyncTask需要实现几个方法
1. AsyncTask内部是如何实现的
1. 谈谈AsyncTask的三个泛型参数作用 & 它的一些方法作用
1. AsyncTask并发下可以同时执行几个
 * 默认是最低2个，最高4个，但是不够用时，会是CPU核数的2倍+1

####  继承Thread
1. Thread生命周期
1.	如何切换线程

#### HandlerThread
#### IntentService
#### 实现Runnable
#### RX系列


#### 线程池


#### 线程池的种类
* FixedThreadPool 可重用固定线程数的线程池

  * 线程数量固定且都是核心线程：核心线程数量和最大线程数量都是nThreads；

  * 都是核心线程且不会被回收，快速相应外界请求；

  * 没有超时机制，任务队列也没有大小限制；

  * 新任务使用核心线程处理，如果没有空闲的核心线程，则排队等待执行。

    ```java
    public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                  0L, TimeUnit.MILLISECONDS,
                  new LinkedBlockingQueue<Runnable>());
    }

* CachedThreadPool 按需创建的线程池

  * 线程数量不定，只有非核心线程，最大线程数任意大：传入核心线程数量的参数为0，最大线程数为Integer.MAX_VALUE；

  * 有新任务时使用空闲线程执行，没有空闲线程则创建新的线程来处理。

  * 该线程池的每个空闲线程都有超时机制，时常为60s（参数：60L, TimeUnit.SECONDS），空闲超过60s则回收空闲线程。

  * 适合执行大量的耗时较少的任务，当所有线程闲置超过60s都会被停止，所以这时几乎不占用系统资源。

    ```java
    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }
    ```

    

* ScheduledThreadPool  定时和周期性的线程池

  * 核心线程数量固定，非核心线程数量无限制；

  * 非核心线程闲置超过10s会被回收；

  * 主要用于执行定时任务和具有固定周期的重复任务；

    ```java
    public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
        (new ThreadPoolExecutor(1, 1,
                            0L, TimeUnit.MILLISECONDS,
                            new LinkedBlockingQueue<Runnable>()));
    }
    ```

    

* SingleThreadPool 单线程的线程池

  * 只有一个核心线程，所有任务在同一个线程按顺序执行。

  * 所有的外界任务统一到一个线程中，所以不需要处理线程同步的问题。

    ```
    private static final long DEFAULT_KEEPALIVE_MILLIS = 10L;
    
    public ScheduledThreadPoolExecutor(int corePoolSize) {
        super(corePoolSize, Integer.MAX_VALUE,
              DEFAULT_KEEPALIVE_MILLIS, MILLISECONDS,
              new DelayedWorkQueue());
    }
    ```

    


## 线程的状态
* 新生状态（New）

  新创建了一个线程对象就进入了初始状态，也就是通过上述新建线程的几个方法就能进入该状态。
* 就绪状态（Runnable）

  线程对象创建后，其他线程(比如main线程）调用了该对象的start()方法。该状态的线程位于可运行线程池中，等待被线程调度选中，获取cpu 的使用权。以下几种方式会进入可运行状态：
* 运行状态（Running）

  可运行状态(runnable)的线程获得了cpu 时间片 ，执行程序代码。线程调度程序从可运行池中选择一个线程作为当前线程，就会进入运行状态。
* 阻塞状态（Blocked）

  线程正在运行的时候，被暂停，通常是为了等待某个时间的发生（比如说某项资源就绪）之后再继续运行。wait，sleep,suspend等方法都可以导致线程阻塞。
* 等待状态(Waiting)
* 死亡状态（Terminated）

* 超时等待(Timed Waiting)

#### 线程通信
* Handler原理
* AsyncTask
* HandlerThread
* IntentService
* RxJava

#### 进程

#### IPC通信

#### IPC通信方式

1. AIDL与Binder
2. 序列化(文件)
3. Socket
4. Broadcast
5. ContentProvider
6. 匿名共享内存

?问题

* Android中进程和线程的关系？区别？
* 多进程通信可能会出现什么问题

#### lowmemorykiller 

#### 进程的优先级

#### 进程的五种状态/等级
* 前台进程 
* 可见进程
* 服务进程
* 后台进程 
* 空进程 

#### 面试问答
* 线程池的好处

* 在Service中新开线程和直接在Activity新开线程的区别

* 若我们直接在Activity中新开一条线程来做耗时操作，当该Activity退出到桌面或其他情况时将成为一个背景进程。

* 若我们在Service中新启动线程，则此时Android会依据进程中当前活跃组件重要程度，将其判断为服务进程，优先级比（1）高。

* 为什么在主线程可以直接使用 Handler？
  因为主线程已经创建了 Looper 对象并开启了消息循环

* Looper 对象是如何绑定 MessageQueue 的？或者说 Looper 对象创建 MessageQueue 过程。
  Looper 有个一成员变量 mQueue，它就是 Looper 对象默认保存的 MessageQueue。新建 Looper 对象时会直接创建 MessageQueue 并赋值给 mQueue。

* Handler、Looper、MessageQueue、Thread关系？
  一个线程可以有多个Handler实例，一个线程对应一个Looper，一个Looper也只对应一个MessageQueue，一个MessageQueue对应多个Message和Runnable。所以就形成了一对多的对应关系，一方：线程、Looper、MessageQueue；多方：Handler、Message。同时可以看出另一个一对一关系：一个Message实例对应一个Handler实例。

* handler postDelay这个延迟是怎么实现的
      简单的讲MessageQueue.next()，会产生一个阻塞从而实现延迟
       [来源参考](https://blog.csdn.net/zhangcanyan/article/details/81980166)

* Handler为何造成内存泄漏
  我们在主线程创建Handler，因此就与主线程相绑定，Handler对象隐式的持有外部对象的引用，该外部对象通常是指Activity。

  -  Handler 使用中如何造成内存泄露
     * 有延时消息，要在Activity销毁的时候移除Messages
     * 匿名内部类导致的泄露改为匿名静态内部类，并且对上下文或者Activity使用弱引用

  [来源参考](https://juejin.im/post/5c831e2a6fb9a049a97a8381)

* 进程保活

  * 	开启一个像素的Activity
     使用前台服务
     多进程相互唤醒
     JobSheduler唤醒
     粘性服务&与系统服务捆绑

​	
