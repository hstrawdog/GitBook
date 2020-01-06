

# String相关
# String StringBuilder StringBuffer 的区别



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