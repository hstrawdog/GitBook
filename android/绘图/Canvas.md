# Canvas)

#			

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