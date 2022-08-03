DSL 方式实现封装可以分为以下几步：

##### 1.创建接口实现类：XxxxInterfaceDslImpl

还有上面的 TextWatcher 作为例子：

class TextWatcherDslImpl : TextWatcher {

    //原接口对应的kotlin函数对象
    private var afterTextChanged: ((Editable?) -> Unit)? = null
    
    private var beforeTextChanged: ((CharSequence?, Int, Int, Int) -> Unit)? = null
    
    private var onTextChanged: ((CharSequence?, Int, Int, Int) -> Unit)? = null
    
    /**
     * DSL中使用的函数，一般保持同名即可
     */
    fun afterTextChanged(method: (Editable?) -> Unit) {
        afterTextChanged = method
    }
    
    fun beforeTextChanged(method: (CharSequence?, Int, Int, Int) -> Unit) {
        beforeTextChanged = method
    }
    
    fun onTextChanged(method: (CharSequence?, Int, Int, Int) -> Unit) {
        onTextChanged = method
    }
    
    /**
     * 实现原接口的函数
     */
    override fun afterTextChanged(s: Editable?) {
        afterTextChanged?.invoke(s)
    }
    
    override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {
        beforeTextChanged?.invoke(s, start, count, after)
    }
    
    override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {
        onTextChanged?.invoke(s, start, before, count)
    }
    
    }
这个实现类由三个部分组成：

1. 原接口方法对应的 Kotlin 函数对象，函数对象的签名与对应的方法签名保持一致
2. DSL 函数，函数名称、签名都与原接口的方法一一对应，用于接收 lambda 赋值给 Kotlin 函数对象
3. 原接口方法的实现，每个接口方法的实现，都是对实现类中 Kotlin 函数对象的调用

##### 2.创建与原函数同名的扩展函数，函数参数为实现类扩展函数

```
etString.addTextChangedListenerDsl {
    afterTextChanged {
        if (it.toString().length >= 4) {
            KeyboardUtils.toggleSoftInput()
        }
    }
}

```

使用这种方式时，可以说相当之优雅，我们只需要调用我们需要实现的接口方法即可，不需要使用的接口方法默认空实现。

[参考](https://blog.csdn.net/u011133887/article/details/123004000)









