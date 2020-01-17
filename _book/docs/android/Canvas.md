# Canvas)

#			

#			Canvas

##				Paint(画笔)

1.					文字测量FontMetrics
       * 							基准点是baseline
       * 							Ascent是baseline之上至字符最高处的距离
       * 							Descent是baseline之下至字符最低处的距离
       * 							Leading文档说的很含糊，其实是上一行字符的descent到下一行的ascent之间的距离
       * 							Top指的是指的是最高字符到baseline的值，即ascent的最大值
       * 							bottom指的是最下字符到baseline的值，即descent的最大值
       * 							参考
1.					抗锯齿 setAntiAlias
       2.					true 开启
       2.					false 清除
1.					宽度 setStrokeWidth
       	只有在空心的时候才会生效
1.					样式 etStyle
       2.						空心/描边 STROKE
       2.						填充 FILL
       2.						填充内部和描边 FILL_AND_STROKE
1.					画笔颜色
       2.					setColor
       2.					setARGB
1.					透明度
       2.					setAlpha
1.					重置
       2.					reset
1.					阴影效果
       2.					setShadowLayer
1.					文字大小
       2.					setTextSize
1.					设置字体的水平方向的缩放因子
       2.					setTextScaleX
              					默认值为1
1.					文本在水平方向上的倾斜
       2.					setTextSkewX
              					推荐值为-0.25
1.					行的间距
       2.					setLetterSpacing
              					默认值是0，负值行间距会收缩
1.					字体样式
       2.					setFontFeatureSettings
              					设置CSS样式
1.					参考

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
		