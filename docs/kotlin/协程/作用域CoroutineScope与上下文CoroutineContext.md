# 作用域

## runBlocking

阻塞协程构造器

适用于单元测试的场景，而业务开发中不会用到这种方法

调用了 runBlocking 的主线程会一直 阻塞 直到 runBlocking 内部的协程执行完毕。

## GlobalScope

非阻塞协程构造器

生命周期受整个应用程序的生命周期限制，且不能取消

## CoroutineScope

非阻塞协程构造器

通过 context 参数去管理和控制协程的生命周期声明自己作用域

它会创建一个协程作用域并且在所有已启动子协程执行完毕之前不会结束



### runBlocking 与 coroutineScope 作用域的区别

在于后者在等待所有子协程执行完毕时不会阻塞当前线程。







# 上下文CoroutineContext

CoroutineContext 作为一个集合，它的元素就是源码中看到的 Element，每一个 Element 都有一个 key，因此它可以作为元素出现，同时它也是 CoroutineContext 的子接口，因此也可以作为集合出现





## 调度器CoroutineDispatcher

确定了相关的协程在哪个线程或哪些线程上执行。协程调度器可以将协程限制在一个特定的线程执行，或将它分派到一个线程池，亦或是让它不受限地运行。
所有的协程构建器诸如 launch 和 async 接收一个可选的 CoroutineContext 参数，它可以被用来显式的为一个新协程或其它上下文元素指定一个调度器

- Dispatchers.Default
- Dispatchers.Main
- Dispatchers.Unconfined
- Dispatchers.IO