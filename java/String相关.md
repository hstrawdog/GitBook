

# String相关
### String是java中的基本数据类型吗？是可变的吗？是线程安全的吗？

- String不是基本数据类型，java中把j基本据类型是：byte, short, int, long, char, float, double, boolean
- String是不可变的
- String是不可变类，一旦创建了String对象，我们就无法改变它的值。因此，它是线程安全的，可以安全地用于多线程环境中

# String StringBuilder StringBuffer 的区别

String：适用于少量的字符串操作的情况
StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况
StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况

# StringBuilder、StringBuffer、+、String.concat 链接字符串

- StringBuffer 线程安全，StringBuilder 线程不安全
- +实际上是用 StringBuilder 来实现的，所以非循环体可以直接用 +，循环体不行，因为会频繁创建 StringBuilder
- String.concat 实质是 new String ，效率也低，耗时排序：StringBuilder < StringBuffer < concat < +

# String.format()的占位符

作用:使用指定的格式字符串和参数返回一个格式化字符串。

str=String.format("Hi,%s %ss", "你好","java");

str = "Hi,你好 java"

System.out.printf("我是数字：%d %n", 100);

str = "我是数字：100"

## 常用的类型关系:

| 转换符 | 详细说明                                     | 示例                     |
| ------ | -------------------------------------------- | ------------------------ |
| %s     | 字符串类型                                   | “喜欢请收藏”             |
| %c     | 字符类型                                     | ‘m’                      |
| %b     | 布尔类型                                     | true                     |
| %d     | 整数类型（十进制）                           | 88                       |
| %x     | 整数类型（十六进制）                         | FF                       |
| %o     | 整数类型（八进制）                           | 77                       |
| %f     | 浮点类型                                     | 8.888                    |
| %a     | 十六进制浮点类型                             | FF.35AE                  |
| %e     | 指数类型                                     | 9.38e+5                  |
| %g     | 通用浮点类型（f和e类型中较短的）             | 不举例(基本用不到)       |
| %h     | 散列码                                       | 不举例(基本用不到)       |
| %%     | 百分比类型                                   | ％(%特殊字符%%才能显示%) |
| %n     | 换行符                                       | 不举例(基本用不到)       |
| %tx    | 日期与时间类型（x代表不同的日期与时间转换符) | 不举例(基本用不到)       |

# equals()和==与=== 的区别



# 如何将String转成int

```java
try {

    int a = Integer.parseInt(str);

} catch (NumberFormatException e) {

    e.printStackTrace();

}
```

```
try {

    int b = Integer.valueOf(str).intValue()

} catch (NumberFormatException e) {

    e.printStackTrace();

}

```

在转换过程中需要注意,因为字符串中可能会出现非数字的情况,所以在转换的时候需要捕捉处理异常