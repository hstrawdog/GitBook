

# Flow分类

- 一般 Flow

  一般的`Fow` , 仅有一个观察者 。冷流 。

- StateFlow

  **有状态**的`Flow` ，可以有多个观察者，热流
  构造时需要传入初始值 : initialState
  常用作与UI相关的数据观察，类比`LiveData`

- SharedFlow

  可定制化的`StateFlow`，可以有多个观察者，热流. 无需初始值，有三个可选参数：
   `replay` - **重播**给新订阅者的值的数量（不能为负，默认为零）。
   `extraBufferCapacity` - 除了replay之外**缓冲**的值的数量。 当有剩余缓冲区空间时， emit不会挂起（可选，不能为负，默认为零）。
   `onBufferOverflow` - 配置缓冲区**溢出**的操作（可选，默认为暂停尝试发出值）
   使用`SharedFlow` 你可以写个 [FlowEventBus](https://juejin.cn/post/6985093305470025764)

#  操作符

## 创建Flow

  - **[flow](https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/flow.html)**
  
    创建Flow的基本方法.
    使用 **emit** 发射单个值
    使用 **emitAll** 发射一个流 ，类似 `list.addAll(anotherList)`
  - **[flowOf](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflow-of.html)**
  
    快速创建 `flow` ,类比 `listOf()`
  - **[asFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fas-flow.html)**
  
    **将其他数据转换成 普通的**`flow` **，一般是\**\*\*集合\*\**\*向**`Flow`**的转换**
  - **[callbackFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcallback-flow.html)**
  
    将回调方法改造成`flow` ,类似`suspendCoroutine`
  - **[emptyFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fempty-flow.html)**
  
    返回一个空流 .
  - **[channelFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fchannel-flow.html)**
  
    在一般的`flow`在构造代码块中不允许切换线程，`ChannelFlow`则允许内部切换线程
    
    

## 末端操作符

  - **[collect](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcollect.html)**
  
    触发flow的运行 。 通常的监听方式
  
  - **[collectIndexed](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcollect-indexed.html)**
  
    带下标的 收集操作
  
  - **[collectLatest](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcollect-latest.html)**
  
    与 `collect`的区别是 ，有新值发出时，如果此时上个收集尚未完成，则会**取消**掉上个值的收集操作
  
  - **[toCollection](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fto-collection.html)**
  
    将结果添加到集合
  
  - **[toList](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fto-list.html)**
  
    将结果转换为`List`
  
  - **[toSet](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fto-set.html)**
  
    将结果转换为`Set`
  
  - **[launchIn](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Flaunch-in.html)**
  
    直接触发流的执行，不设置`action`,入参为`coroutineScope` 一般不会直接调用，会搭配别的操作符一起使用，如`onEach`,`onCompletion` 。返回值是`Job`
  
  - **[last](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Flast.html)**
  
    返回流 发出 的**最后一个值** **,如果为空会抛异常**
  
  - **[lastOrNull](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Flast-or-null.html)**
  
    返回流 发出 的**最后一个值** **,可以为空**
  
  - **[first](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffirst.html)**
  
    返回流 发出 的**第一个值** **,如果为空会抛异常**
  
  - **[firstOrNull](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffirst-or-null.html)**
  
    返回流 发出 的**第一个值** **,可以为空**
  
  - **[single](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fsingle.html)**
  
    接收流发送的第一个值 ，区别于`first()`,如果**为空**或者发了**不止一个**值，则都会报错
  
  - **[singleOrNull](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fsingle-or-null.html)**
  
    接收流发送的第一个值 ，可以为空 ,发出多值的话除第一个，后面均被置为null
  
  - **[count](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcount.html)**
  
    返回流发送值的个数。 类似 `list.size()` ，注：`sharedFlow`无效(无意义）
  
  - **[fold](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffold.html)**
  
    从初始值开始 执行遍历,并将结果作为下个执行的 参数。
  
  - **[reduce](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Freduce.html)**
  
    和`fold` 差不多。 无初始值

## 回调操作符

- **[onStart](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fon-start.html)**

  在上游流开始之前被调用。 可以发出额外元素,也可以处理其他事情，比如发埋点

- **[onCompletion](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fon-completion.html)**

- 在流**取消或者结束**时调用。可以执行发送元素，发埋点等操作

- **[onEach](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fon-each.html)**

- 在上游向下游发出元素之前调用

- **[onEmpty](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fon-empty.html)**

- 当流完成却没有发出任何元素时回调。 可以用来兜底.。

- **[onSubscription](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fon-subscription.html)**

- `SharedFlow` **专属**操作符 （`StateFlow`是`SharedFlow` 的一种特殊实现）
  在**建立订阅之后** 回调。 和 `onStart` 有些区别 ，`SharedFlow` 是热流，因此如果在`onStart`里发送值，则下游可能接收不到。

- 

## 变换操作符

- **[map](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmap.html)**

- 将发出的值 进行变换 ，`lambda`的返回值为最终发送的值

- **[mapLatest](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmap-latest.html)**

- 类比 `collectLatest` **,当有新值发送时如果上个变换还没结束，会先取消掉**

- **[mapNotNull](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmap-not-null.html)**

- 仅发送 `map`后不为空的值

- **[transform](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftransform.html)**

- 对发出的值 进行变换 。区别于`map`， `transform`的接收者是`FlowCollector` ，因此它非常灵活，可以变换、跳过它或多次发送。

- **[transformLatest](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftransform-latest.html)**

- 类比 **[mapLatest](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmap-latest.html)** **,当有新值发送时如果上个变换还没结束，会先取消掉**

- **[transformWhile](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftransform-while.html)**

- 这个变化的`lambda` 的返回值是 `Boolean` ,如果为 `False`则不再进行后续变换, 为 `True`则继续执行

- **[asStateFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fas-state-flow.html)**

- 将 `MutableStateFlow` 转换为 `StateFlow` ，就是变成不可变的。常用在对外暴露属性时使用

- **[asSharedFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fas-shared-flow.html)**

- 将 `MutableSharedFlow` 转换为 `SharedFlow` ，就是变成不可变的。常用在对外暴露属性时使用

- **[receiveAsFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Freceive-as-flow.html)**

- 将`Channel` 转换为`Flow` ,可以有多个观察者，但不是多播，可能会轮流收到值。

- **[consumeAsFlow](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fconsume-as-flow.html)**

- 将`Channel` 转换为`Flow` ,但**不能多个观察者**（会crash）!

- **[withIndex](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fwith-index.html)**

- 将结果包装成`IndexedValue` 类型

- **[scan](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fscan.html)**

- 和 `fold` 相似，区别是`fold` 返回的是最终结果，`scan`返回的是个`flow` ，会把初始值和每一步的操作结果发送出去。

- **[produceIn](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fproduce-in.html)**

- 转换为 `ReceiveChannel` , 不常用。
  注： `Channel` 内部有 `ReceiveChannel` 和 `SendChannel`之分,看名字就是一个发送，一个接收。

- **[runningFold](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Frunning-fold.html)**

- 区别于 `fold` ，就是返回一个新流，将每步的结果发射出去。

- **[runningReduce](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Frunning-reduce.html)**

- 区别于 `reduce` ，就是返回一个新流，将每步的结果发射出去。

- **[shareIn](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fshare-in.html)**

- 

- > 将普通`flow` 转化为 `SharedFlow` , 其有三个参数
  >  `scope`:  `CoroutineScope` *开始共享的协程范围* `started`:  `SharingStarted` *控制何时开始和停止共享的策略*
  >  `replay: Int = 0` 发给 新的订阅者 的旧值数量

  > 其中 `started` 有一些可选项:
  >  `Eagerly` : 共享立即开始，永不停止
  >  `Lazily` : 当第一个订阅者出现时,永不停止
  >  `WhileSubscribed` : 在第一个订阅者出现时开始共享，在最后一个订阅者消失时立即停止（默认情况下），永久保留重播缓存（默认情况下）
  >  `WhileSubscribed` 具有以下可选参数：
  >  `stopTimeoutMillis` — 配置最后一个订阅者消失到协程停止共享之间的延迟（以毫秒为单位）。 默认为零（立即停止）。
  >  `replayExpirationMillis` - 共享的协程从停止到重新激活，这期间缓存的时效

- **[stateIn](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fstate-in.html)**

- 将普通`flow` 转化为 `StateFlow` 。 其有三个参数：
  `scope` - 开始共享的协程范围
  `started` - 控制何时开始和停止共享的策略
  `initialValue` - 状态流的初始值

  

## 过滤操作符

- **[filter](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffilter.html)**

> 筛选出符合条件的值

- **[filterInstance](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffilter-is-instance.html)**

> 筛选对应类型的值

- **[filterNot](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffilter-not.html)**

> 筛选不符合条件相反的值,相当于`filter`取反

- **[filterNotNull](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ffilter-not-null.html)**

> 筛选不为空的值

- **[drop](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fdrop.html)**

> 入参`count`为`int`类型 ,作用是 丢弃掉前 n 个的值

- **[dropWhile](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fdrop-while.html)**

> 这个操作符有点特别，和`filter` 不同！ 它是找到第一个**不满足条件的**，返回其和其之后的值。
> 如果首项就不满足条件，则是全部返回。

- **[take](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftake.html)**

> 返回前 n个 元素

- **[takeWhile](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftake-while.html)**

> 也是找第一个不满足条件的项，但是取其之前的值 ，和`dropWhile` **相反。**

> 如果第一项就不满足，则为**空流**

- **[debounce](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fdebounce.html)**

> 防抖节流 ，指定时间内的值只接收最新的一个，其他的过滤掉。搜索联想场景适用

- **[sample](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fsample.html)**

> 采样 。给定一个时间周期，仅获取周期内最新发出的值

- **[distinctUntilChangedBy](https://link.juejin.cn?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fdistinct-until-changed-by.html)**

> 去重操作符，判断连续的两个值是否重复，可以选择是否丢弃重复值。

> ```
> keySelector: (T) -> Any?` 指定用来判断是否需要比较的 `key
> ```

> 有点类似Recyclerview的DiffUtil机制。

- **[distinctUntilChanged](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fdistinct-until-changed.html)**

> 过滤用，`distinctUntilChangedBy` **的简化调用 。连续两个值一样，则跳过发送**



## 组合操作符

- **[combine](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcombine.html)**

> 组合每个流**最新**发出的值。

- **[combineTransform](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcombine-transform.html)**

> 顾名思义 **[combine](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcombine.html)** + **[transform](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftransform.html)******

- **[merge](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmerge.html)**

> 合并多个流成 一个流。 可以用在 多级缓存加载上

- **[flattenConcat](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflatten-concat.html)**

> 以顺序方式将给定的流展开为单个流 ，是`Flow<Flow<T>>`的扩展函数

- **[flattenMerge](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflatten-merge.html)**

> 作用和 `flattenConcat` **一样**，但是可以设置并发收集流的数量。

> 有个入参：`concurrency: Int` ,当其 == 1时，效果和 `flattenConcat` **一样，大于 1 时，则是并发收集。**

- **[flatMapContact](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflat-map-concat.html)**

> 这是一个组合操作符，相当于 **[map](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmap.html)** + **[flattenConcat](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflatten-concat.html)** **, 通过 map 转成一个流，在通过 flattenConcat**

> 展开合并成一个流

- **[flatMapLatest](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflat-map-latest.html)**

> 和其他 带 **Latest**的操作符 一样，如果下个值来了，上变换还没结束，就取消掉。

> 相当于 **[transformLatest](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Ftransform-latest.html)** **+ emitAll**

- **[flatMapMerge](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflat-map-merge.html)**

> 也是组合操作符，简化使用。 **[map](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fmap.html)** + **[flattenMerge](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflatten-merge.html)** **。 因此也是有** `concurrency: Int` **这样一个参数，来限制并发数。**

- **[zip](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fzip.html)**

> 对两个流进行组合，分别从二者取值，一旦一个流结束了，那整个过程就结束了。



## 功能性操作符

- **[cancellable](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcancellable.html)**

> 接收的的时候判断 协程是否被取消 ，如果已取消，则抛出异常

- **[catch](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fcatch.html)**

> 对**上游**异常进行捕获 ，对下游无影响

> **上游** 指的是 此操作符之前的流

> **下游** 指的是此操作符之后的流

- **[retryWhen](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fretry-when.html)**

> 有条件的进行重试 ，`lambda` 中有两个参数: 一个是 异常原因，一个是当前重试的 `index` (从0开始).

> `lambda` 的返回值 为 `Boolean` ，`true`则继续重试 ,`false` 则结束重试

- **[retry](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fretry.html)**

> 重试机制 ，当流发生异常时可以重新执行。`retryWhen` **的简化版。**

> `retries: ``Long`` = Long.MAX_VALUE` 指定重试次数，以及控制是否继续重试.(默认为true)

- **[buffer](https://link.juejin.cn?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fbuffer.html)**

> **如果操作符的代码需要相当\**\**长时间来执行** **，可使用**`buffer`**操作符在执行期间为其创建一个单独的协程**

> `capacity: Int = BUFFERED` 缓冲区的容量

> `onBufferOverflow: BufferOverflow = BufferOverflow.``SUSPEND` **溢出的话执行的操作

> 有三个选择 ： *SUSPEND 挂起， DROP_OLDEST 丢掉旧的，DROP_LATEST 丢掉新的*

- **[conflate](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fconflate.html)**

> 仅保留最新值, 内部就是 `buffer``(``CONFLATED``)`

- **[flowOn](https://link.juejin.cn/?target=https%3A%2F%2Fkotlin.github.io%2Fkotlinx.coroutines%2Fkotlinx-coroutines-core%2Fkotlinx.coroutines.flow%2Fflow-on.html)**

> 指定上游操作的执行线程 。 想要切换执行线程 就用它！



https://juejin.cn/post/6989536876096913439#heading-8

# Flow 合并请求

1. 使用zip 操作符 只支持两个对象

```
        //第一个网络请求
        val request1 = getFlow {
            service.listReposWithBody("zyj1609wz")
        }

        //第二个网络请求
        val request2 = getFlow {
            service.listReposWithBody("zyj1609wz")
        }

        //两个请求并行
        request1.zip(request2) { response1, response2 ->
            Pair(response1, response2)
        }
            .catch {
                it.printStackTrace()
            }
            .onEach {
                val list1 = it.first
                val list2 = it.second
            }
            .launchIn(lifecycleScope)
            .start()

```

2.  combine

```
  //第一个网络请求
        val request1 = getFlow {
            service.listReposWithBody("zyj1609wz")
        }

        //第二个网络请求
        val request2 = getFlow {
            service.listReposWithBody("zyj1609wz")
        }

        //第三个网络请求
        val request3 = getFlow {
            service.listReposWithBody("zyj1609wz")
        }

        //3个请求并行
        combine(request1, request2, request3) { response1, response2, response3 ->
            //合并结果
            mutableListOf(response1, response2, response3)
        }
            .catch {
                //处理异常
                it.printStackTrace()
            }
            .onEach {
                //处理结果
            }
            .launchIn(lifecycleScope)
            .start()

```



https://blog.csdn.net/zhaoyanjun6/article/details/121754941

