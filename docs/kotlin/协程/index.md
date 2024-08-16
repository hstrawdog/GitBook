### 协程是什么?

就是一个线程框架，提供了一套操作线程的api.

### 说说你对协程的理解

程和线程一样都是用来解决并发任务（异步任务）的方案。所以协程和线程是属于一个层级的概念，但是对于kotlin中的协程，又与广义的协程有所不同。kotlin中的协程其实是对线程的一种封装，或者说是一种线程框架，为了让异步任务更好更方便使用



#### 基础属性

1. 挂起函数 **suspend** 

   挂起函数中能调用任何函数。

   非挂起函数只能调用非挂起函数。

   换句话说，suspend函数只能在suspend函数中调用。

1. 派发器 Dispatchers

1. job  对象

      1. start()

      1. join()

            `join()`方法就比较特殊，他是一个`suspend`方法。`suspend` 修饰的方法(或闭包)只能调用被`suspend`修饰过的方法(或闭包)。 方法声明如下：

      1. cancel()

1. 堵塞 runBlocking 

          GlobalScope.launch {
               var num = 0
               runBlocking {
                   num++
               }
               System.out.print(num)
           }

1. 并发和异步  async()  await 

      `async()`方法也是创建一个协程并启动，甚至连方法的声明都跟`launch()`方法一模一样。
      不同的是，`async()`方法的返回值，返回的是一个`Deferred`对象。这个接口是`Job`接口的子类。
      因此上文介绍的所有方法，都可以用于`Deferred`的对象。
      Deferred`最大的用处在于他特有的一个方法`await()

1. 注解 

   1. Volatile 

   1. Synchronized  

          @Volatile
          var synclist = CopyOnWriteArrayList<String>()
          @Synchronized
          fun numAdd() {
              num += 1
              Log.e(TAG, "testSync: ${num}")
          
          }





https://www.cnblogs.com/joy99/p/15805916.html#41-%E5%8D%8F%E7%A8%8B%E4%B8%8A%E4%B8%8B%E6%96%87-coroutinecontext

