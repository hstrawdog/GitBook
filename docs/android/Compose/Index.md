# 布局

1. #### Column

2. #### Row

   1. modifier  布局的修饰符

   2. horizontalArrangement

      布局子级的 水平 放置方式，默认从布局开始往布局结束方向放置传入 Arrangement  类型

      1. 

   3. verticalAlignment   布局子级的 垂直 对其方式，默认从布局顶部对齐

   4. content 

3. #### Box

# 控件

1. [Text](/Text.md)





# 注解



1. #### @Compose

   所有关于构建View的方法都必须添加`@Compose`的注解才可以。并且`@Compose`跟协程的`Suspend`的使用方法比较类似,被`@Compose`的注解的方法只能在同样被`@Comopse`注解的方法中才能被调用。

2. #### @Preview

   `name: String`: 为该Preview命名，该名字会在布局预览中显示。

   `showBackground: Boolean`: 是否显示背景，true为显示。

   `backgroundColor: Long`: 设置背景的颜色。

   `showDecoration: Boolean`: 是否显示Statusbar和Toolbar，true为显示。

   `group: String`: 为该Preview设置group名字，可以在UI中以group为单位显示。

   `fontScale: Float`: 可以在预览中对字体放大，范围是从0.01。

   `widthDp: Int`: 在Compose中渲染的最大宽度，单位为dp。

   `heightDp: Int`: 在Compose中渲染的最大高度，单位为dp。

   

# 主题 Theme



# 组件





# Modifier

`Modifier`是各个`Compose`的UI组件一定会用到的一个类。它是被用于设置UI的摆放位置，padding等信息的类。关于`Modifier`相关的设置实在是太多，在这里只介绍会经常用到的