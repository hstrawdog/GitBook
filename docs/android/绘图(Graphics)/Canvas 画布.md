# Canvas)


- 几何图形 -> 位于 Canvas 下 
 1. 画直线  void drawLine (float startX, float startY, float stopX, float stopY, Paint paint)
        - startX:开始点X坐标
        - startY:开始点Y坐标
        - stopX:结束点X坐标
        - stopY:结束点Y坐标
             - 多条直线
            void drawLines (float[] pts, Paint paint)
            void drawLines (float[] pts, int offset, int count, Paint paint)
            pts  两两连成一条直线

 2. 点  void drawPoint (float x, float y, Paint paint)
         - float X：点的X坐标
             - float Y：点的Y坐标

 3. 多个点
       void drawPoints (float[] pts, Paint paint)
       void drawPoints (float[] pts, int offset, int count, Paint paint)
     - int offset:集合中跳过的数值个数，注意不是点的个数！一个点是两个数值；
     - count:参与绘制的数值的个数，指pts[]里人数值个数，而不是点的个数，因为一个点是两个数值
     - offset与count的含义：（跳过第一个点，画出后面两个点，第四个点不画），注意一个点是两个数值！
    - 矩形工具类RectF与Rect
        - RectF RectF(float left, float top, float right, float bottom)  根据四个点构造出一个矩形
        - Rect  Rect(int left, int top, int right, int bottom) 

 4. 矩形
        - void drawRect (float left, float top, float right, float bottom, Paint paint)
        - void drawRect (RectF rect, Paint paint)
        - void drawRect (Rect r, Paint paint)

 5. 圆角矩形 void drawRoundRect (RectF rect, float rx, float ry, Paint paint)
        - RectF rect:要画的矩形
        - float rx:生成圆角的椭圆的X轴半径
        - float ry:生成圆角的椭圆的Y轴半径

 6. 圆角矩形 drawRoundRect(float left, float top, float right, float bottom, float rx, float ry, @NonNull Paint paint)

     - left 
     - top
     - right
     - bottom
     - rx  x方向上的圆角半径。
     - ry  y方向上的圆角半径。 
     - paint  绘制时所使用的画笔。

 7. 圆形 void drawCircle (float cx, float cy, float radius, Paint paint)
        - float cx：圆心点X轴坐标 
        -  float cy：圆心点Y轴坐标
        - float radius：圆的半径

 8. 椭圆 void drawOval (RectF oval, Paint paint)

 9. 弧 void drawArc (RectF oval, float startAngle, float sweepAngle, boolean useCenter, Paint paint)
       - RectF oval:生成椭圆的矩形

       - float startAngle：弧开始的角度，以X轴正方向为0度

       - float sweepAngle：弧持续的角度

       -  boolean useCenter:是否有弧的两边，True，还两边，False，只有一条弧
     
  9. 文本绘制
     
       - void drawText (String text, float x, float y, Paint paint)

       - void drawText (CharSequence text, int start, int end, float x, float y, Paint paint)

       - void drawText (String text, int start, int end, float x, float y, Paint paint)

       -  void drawText (char[] text, int index, int count, float x, float y, Paint paint)
          第一个构造函数：最普通简单的构造函数；
          第三、四个构造函数：实现截取一部分字体给图；
          第二个构造函数：最强大，因为传入的可以是charSequence类型字体，所以可以实现绘制带图片的扩展文字（待续），而且还能截取一部分绘制
      - 指定个个文字位置
      - void drawPosText (char[] text, int index, int count, float[] pos, Paint paint)
      -  void drawPosText (String text, float[] pos, Paint paint)
         说明：
          第一个构造函数：实现截取一部分文字绘制；
        
         参数说明：
         char[] text：要绘制的文字数组
         int index:：第一个要绘制的文字的索引
         int count：要绘制的文字的个数，用来算最后一个文字的位置，从第一个绘制的文字开始算起
         float[] pos：每个字体的位置，同样两两一组，如｛x1,y1,x2,y2,x3,y3……｝

 10. 沿路径绘制
        - void drawTextOnPath (String text, Path path, float hOffset, float vOffset, Paint paint)
        - void drawTextOnPath (char[] text, int index, int count, Path path, float hOffset, float vOffset, Paint paint)
           参数说明：
           有关截取部分字体绘制相关参数（index,count），没难度，就不再讲了，下面首重讲hOffset、vOffset
           float hOffset  : 与路径起始点的水平偏移距离
           float vOffset  : 与路径中心的垂直偏移量



#			Canvas

##					Path(路径)

1. 圆形

##					变换

1.					平移
       2.					translate
1.					scale 缩放 旋转
       2.					rotate
1.					斜拉
       2.					skew
1.					裁剪
       2.					clipRect
       2.					clipPath

##					 draw(绘制)

### 背景

2. drawColor

   给画布添加颜色

   ```
   canvas.drawColor(Color.RED);
   canvas.drawColor(0x80000000);
   ```

2. drawRGB

2. drawARGB

### 点

2.					drawPoint
2.					drawPoints

### 线

2.					drawLine
2.					drawLines

### 矩形

2.					drawRect
2.					drawRoundRect

### 圆形

2.					drawCircle

3.					路径多边形
       2.					drawPath
       2.					贝赛尔曲线

### 图片

#### drawBitmap



```



   /**
     * @param bitmap 图片
     * @param src   图片需要绘制的位置
     * @param dst   图片显示的位置
     * @param paint 画笔
     */
    public void drawBitmap(@NonNull Bitmap bitmap, @Nullable Rect src, @NonNull Rect dst,
                           @Nullable Paint paint) {
        super.drawBitmap(bitmap, src, dst, paint);
    }

```





##### 绘制原图大小

```
Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.mipmap.bg_sty);
canvas.drawBitmap(bitmap, 0, 0,null);
```

##### 绘制全屏大小

```
Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.mipmap.bg_sty);
RectF rectF = new RectF(0, 0, getWidth(), getHeight());
canvas.drawBitmap(bitmap, null, rectF, null);
```

#### drawPicture

### 椭圆

drawOval

### 圆弧

drawArc

2. drawArc(@NonNull RectF oval, float startAngle, float sweepAngle, boolean useCenter,\n	    @NonNull Paint paint)
2. drawArc(float left, float top, float right, float bottom, float startAngle,\n	    float sweepAngle, boolean useCenter, @NonNull Paint paint)
   参考

## 文字

1. 						drawText
1. 						drawPosText
1. 						drawTextOnPath


##					快照

1. 					保存当前状态 save
1. 					回滚到上一次保存的状态 restore
1. 					保存图层状态 saveLayerXxx
1. 					回滚到指定状态 restoreToCount
1. 					获取保存次数 getSaveCount

##					矩阵

1. 					getMatrix
1. 					setMatrix
1. 					concat


##					顶点操作

* 					drawVertices
* 					drawBitmapMesh

 [参考](https://www.jianshu.com/p/1fddeb8ec9fe)
		

#			问题

1. 				?知道SVG & 矢量动画吗
1. 				?说说转场动画
1. 				?谈插值器 & 估值器 的作用
1. 				?View动画和属性动画的区别
1. 				?Android动画框架实现的原理
1. 				?帧动画在使用时需要注意什么
1. 				View的事件分发
       * 					能给我谈谈Android中坐标体系吗？
       * 					.OnTouchListener & OnTouchEvent & onClickListener三者之间的关系
       * 					说说事件分发的流程 
1. 				View的绘制流程
1. 				在Activity中如何获取View的高度
1. 				说说Activity View树结构
1. 				自定义View的方式有哪些
1. 				自定义View时常常重写的一些方法？
1. 				自定义View中如何自定义属性
1. 				requestLayout(),onLayout(),onDraw(),drawChild()区别和联系
1. 				如何计算出一个View的嵌套层级
1. 				自定义View如何考虑机型适配
1. 				MotionEvent是什么？包含几种事件？什么条件下会产生？
1. 				scrollTo()和scrollBy()的区别？
1. 				Scroller中最重要的两个方法是什么？主要目的是？
1. 				MeasureSpec是什么？有什么作用？
1. 				自定义View/ViewGroup需要注意什么？
1. 				onTouch()、onTouchEvent()和onClick()关系？
1. 				invalidate()和postInvalidate()的区别？
1. 				SurfaceView和View的区别？
1. 				ViewGroup 绘制顺序