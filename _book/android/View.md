# View与ViewGroup

##				view的大小

1. getWidth()

   getWidth（）获取的是这个view最终显示的大小，这个大小有可能等于原始的大小也有可能不等于原始大小。

1. getMeasuredWidth()

   getMeasuredWidth()获取的是view原始的大小，也就是这个view在XML文件中配置或者是代码中设置的大小

1. getMinimumWidth

   getMinimumWidth() 是最小宽度，是XML参数定义里的 minWidth，也是一个辅助测量展示的参数。

1. getIntrinsicWidth()

   getIntrinsicWidth() 是原有宽度，有时候原有宽度可能很大，但是实际上空间不够，所有效果上并没有那么大，这个方法可以获得原有宽度，可以辅助测量的时候选择合适的展示宽度。

1. getX，getRawX,getWidth,getTranslationX等的区别

   1. 					第一种是在onTouchEvent中
           * 						event.getX()：表示的是触摸的点距离自身左边界的距离
           * 						event.getY()：表示的是触摸的点距离自身上边界的距离
           * 						event.getRawX：表示的是触摸点距离屏幕左边界的距离
           * 						event.getRawY：表示的是触摸点距离屏幕上边界的距离
   1. 					第二种是在View中
           * 						view.getTop()：子View的顶部到父View顶部的距离
           * 						view.getRight()：子View的右边界到父View的左边界的距离
           * 						view.getBottom()：子View的底部到父View的顶部的距离
           * 						view.getLeft()：子View的左边界到父View的左边界的距离
           * 						这四个值与父控件的padding和子控件的margin无关，不管这两个属性设置多少，四个值始终是子、父控件的边界差，认准边界即可。
           * 						view.getTranslationX()：计算的是该View在X轴的偏移量。初始值为0，向左偏移值为负，向右偏移值为正。
           * 						view.getTranslationY()：计算的是该View在Y轴的偏移量。初始值为0，向上偏移为负，向下偏移为正。
           * 						view.getX=view.getTranslationX()+view.getLeft()
           * 						view.getY=view.getTranslationY()+view.getTop()
   1. 					第三种是在支持滑动的父控件中
           需要说明的一点是：当屏幕滑动时，并不是父控件在移动，而是父控件中的子控件在移动(view表示父控件)
           * 						view.getScrollX：父控件中的子控件在x方向上的滚动距离
           * 						view.getScrollY：父控件中的子控件在y方向上的滚动距离
           

##				View的六种滑动

1. scrollTo与scrollBy

   1. scrollTo

      * 							传入目标点 
                        					用于边界判断 或者初始化的时候滑动

   1. scrollBy

      * 							滑动距离 
                        					配合MotionEvent进行滑动效果

   1. 对于View来说：

      * 							mScrollX：View的内容(content)相对于View本身在水平方向的偏移量。
      * 							mScrollY：:View的内容(content)相对于View本身在垂直方向的偏移量。
      * 							scrollTo(int x, int y)：将一个视图的内容移动到指定位置.此时偏移量 mScrollX,mScrollY就分别等于x,y.
      * 							scrollBy(int x, int y)： 在现有的基础上继续移动视图的内容.

   1. 对于ViewGroup来说：

      * 							移动的是它对应的所有子View。

   1. 注意：

      scrollTo()和scrollBy()移动的只是View的内容,但是View的背景是不移动的.
      					滑动后的距离可以通过 getScrollX getScrollY 获取

1. layout(方法)

1. offsetLeftAndroidRight()与offsetTopAndButtom()

1. layoutParams(改变布局参数)

1. 动画

1. Scroller

## View的渲染机制

​		onLayout与onMeasure

​		onDraw映射机制

##			onMeasure

注意 在约束布局下设置machParent 设置宽度会出现无效

##			ViewGroup



## View的绘制流程

View的绘制流程：OnMeasure()——>OnLayout()——>OnDraw()
各步骤的主要工作：
***OnMeasure()：***
测量视图大小。从顶层父View到子View递归调用measure方法，measure方法又回调OnMeasure。
***OnLayout()***
确定View位置，进行页面布局。从顶层父View向子View的递归调用view.layout方法的过程，即父View根据上一步measure子View所得到的布局大小和布局参数，将子View放在合适的位置上。
***OnDraw()：***
绘制视图:ViewRoot创建一个Canvas对象，然后调用OnDraw()。六个步骤：①、绘制视图的背景；②、保存画布的图层（Layer）；③、绘制View的内容；④、绘制View子视图，如果没有就不用；⑤、还原图层（Layer）；⑥、绘制滚动条。



## **事件传递机制**

1).Android事件分发机制的本质是要解决：点击事件由哪个对象发出，经过哪些对象，最终达到哪个对象并最终得到处理。这里的对象是指Activity、ViewGroup、View.
2).Android中事件分发顺序：Activity（Window） -> ViewGroup -> View.
3).事件分发过程由dispatchTouchEvent() 、onInterceptTouchEvent()和onTouchEvent()三个方法协助完成

**设置Button按钮来响应点击事件事件传递情况：（如下图）**
布局如下:

![img](https://mmbiz.qpic.cn/mmbiz_png/82jN7o40p6lFIyibgZXBVqAbIuTlruyNw0iafLygh5KsBznVCzeOGqWAbFvYq4upLYmHiau3q9qic72suwFj03RsRQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



最外层：Activiy A，包含两个子View：ViewGroup B、View C
中间层：ViewGroup B，包含一个子View：View C
最内层：View C
假设用户首先触摸到屏幕上View C上的某个点（如图中黄色区域），那么Action_DOWN事件就在该点产生，然后用户移动手指并最后离开屏幕。



**按钮点击事件:**
DOWN事件被传递给C的onTouchEvent方法，该方法返回true，表示处理这个事件;
因为C正在处理这个事件，那么DOWN事件将不再往上传递给B和A的onTouchEvent()；
该事件列的其他事件（Move、Up）也将传递给C的onTouchEvent();



<img src="https://mmbiz.qpic.cn/mmbiz_png/82jN7o40p6lFIyibgZXBVqAbIuTlruyNwfyaJQNTExEpPpiap4BdMMHicD1vRPZ5SVXUedpk57cchvrgDsdibWymeg/640?wx_fmt=png&amp;tp=webp&amp;wxfrom=5&amp;wx_lazy=1&amp;wx_co=1" alt="img" style="zoom:50%;" />