# 自定义View/动画/Canvas

#			View
##				view的大小
1. getWidth()
	
	getWidth（）获取的是这个view最终显示的大小，这个大小有可能等于原始的大小也有可能不等于原始大小。

1. getMeasuredWidth()
	
	getMeasuredWidth()获取的是view原始的大小，也就是这个view在XML文件中配置或者是代码中设置的大小

1. getMinimumWidth
	
   getMinimumWidth() 是最小宽度，是XML参数定义里的 minWidth，也是一个辅助测量展示的参数。

1. 	getIntrinsicWidth()
	
	getIntrinsicWidth() 是原有宽度，有时候原有宽度可能很大，但是实际上空间不够，所有效果上并没有那么大，这个方法可以获得原有宽度，可以辅助测量的时候选择合适的展示宽度。
1. 	getX，getRawX,getWidth,getTranslationX等的区别
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
	1. 第三种是在支持滑动的父控件中
		需要说明的一点是：当屏幕滑动时，并不是父控件在移动，而是父控件中的子控件在移动(view表示父控件)
		* 						view.getScrollX：父控件中的子控件在x方向上的滚动距离
		* 						view.getScrollY：父控件中的子控件在y方向上的滚动距离
				
##				View的六种滑动
1. scrollTo与scrollBy
	1. 						scrollTo
		* 							传入目标点 
								用于边界判断 或者初始化的时候滑动
	1. 						scrollBy
		* 							滑动距离 
								配合MotionEvent进行滑动效果
	1. 						对于View来说：
		* 							mScrollX：View的内容(content)相对于View本身在水平方向的偏移量。
		* 							mScrollY：:View的内容(content)相对于View本身在垂直方向的偏移量。
		* 							scrollTo(int x, int y)：将一个视图的内容移动到指定位置.此时偏移量 mScrollX,mScrollY就分别等于x,y.
		* 							scrollBy(int x, int y)： 在现有的基础上继续移动视图的内容.
	1. 						对于ViewGroup来说：
		
		* 							移动的是它对应的所有子View。
	1. 注意：
		
		scrollTo()和scrollBy()移动的只是View的内容,但是View的背景是不移动的.
							滑动后的距离可以通过 getScrollX getScrollY 获取
1. 	layout(方法)
1. offsetLeftAndroidRight()与offsetTopAndButtom()
1. layoutParams(改变布局参数)
1. 动画
1. Scroller

##			onMeasure
				注意 在约束布局下设置machParent 设置宽度会出现无效
#			ViewGroup
#			Canvas
##				Paint(画笔)
1.					文字测量
	2.					FontMetrics
		* 							基准点是baseline
		* 							Ascent是baseline之上至字符最高处的距离
		* 							Descent是baseline之下至字符最低处的距离
		* 							Leading文档说的很含糊，其实是上一行字符的descent到下一行的ascent之间的距离
		* 							Top指的是指的是最高字符到baseline的值，即ascent的最大值
		* 							bottom指的是最下字符到baseline的值，即descent的最大值
		* 							参考
1.				抗锯齿
	2.					setAntiAlias
		2.					true
								开启
		2.					false
								清除
1.					宽度
	2.					setStrokeWidth
							只有在空心的时候才会生效
1.					样式
						setStyle
	2.						空心/描边
								STROKE
	2.						填充
								FILL
	2.						填充内部和描边
								FILL_AND_STROKE
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
##					变换
1.					平移
	2.					translate
1.					缩放
	2.					scale
1.					旋转
	2.					rotate
1.					斜拉
	2.					skew
1.					裁剪
	2.					clipRect
	2.					clipPath

##					绘制
1. 					背景
	2.					drawColor
	2.					drawRGB
	2.					drawARGB
1. 					点
	2.					drawPoint
	2.					drawPoints
1. 					线
	2.					drawLine
	2.					drawLines
1. 					矩形
	2.					drawRect
	2.					drawRoundRect
1. 					圆形
	2.					drawCircle
1. 					路径多边形
	2.					drawPath
	2.					贝赛尔曲线
1. 					图片
	2.					drawBitmap
	2.					drawPicture
1. 					椭圆
						drawOval
1. 					圆弧
						drawArc
	2.						drawArc(@NonNull RectF oval, float startAngle, float sweepAngle, boolean useCenter,\n	    @NonNull Paint paint)
	2.						drawArc(float left, float top, float right, float bottom, float startAngle,\n	    float sweepAngle, boolean useCenter, @NonNull Paint paint)
							参考

##						文字
1. 						drawText
1. 						drawPosText
1. 						drawTextOnPath
						
##					快照
1. 					保存当前状态
						save
1. 					回滚到上一次保存的状态
						restore
1. 					保存图层状态
						saveLayerXxx
1. 					回滚到指定状态
						restoreToCount
1. 					获取保存次数
						getSaveCount

##					矩阵

1. 					getMatrix
1. 					setMatrix
1. 					concat
					
##					顶点操作
* 					drawVertices
* drawBitmapMesh

 [参考](https://www.jianshu.com/p/1fddeb8ec9fe)
					
#				事件分发
1. 				Activity
	* 					dispatchTouchEvent
	* 					onTouchEvent
	
1. 				Group
	* 					dispatchTouchEvent
	* 					onInterceptTouchEvent
	* 					onTouchEvent
	
1. 				View
	* 					dispatchTouchEvent
	* 					onTouchEvent
	
1. 流程图
	

![img](https://img-blog.csdn.net/20130812110316937?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcWl1c2h1aXFpZmVp/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

https://blog.csdn.net/xyz_lmn/article/details/12517911


#			动画
##				Android中的动画分为哪些种类
1. ValueAnimator(属性动画)
	1. 						TimeInterpolator(插值器)
	1.					TypeEvaluator(估值器)
	1. 						ObjectAnimator
	1. 						TimeAnimator
	1. 						AnimatorSet(动画集合)
	1. 						Animator监听器
		1. 								AnimatorListener
		1. 								onAnimationStart() - 当动画开始的时候调用.
		1. 								onAnimationEnd() - 动画结束时调用.
		1. 								onAnimationRepeat() - 动画重复时调用.
		1. 								onAnimationCancel() - 动画取消时调用.取消动画也会调用onAnimationEnd，它不会关系动画是怎么结束的。
		1. 								ValueAnimator.AnimatorUpdateListener中的接口
		1. 								onAnimationUpdate()动画中每一帧更新的时候调用
							AnimatorListenerAdapter
	1. 						Animator在xml中
	
1. 视图动画（View 动画）
1. 	帧动画（Frame 动画、Drawable 动画）
1. 触摸反馈动画（Ripple Effect）
1. 揭露动画（Reveal Effect）
1. 	转场动画 & 共享元素（Activity 切换动画）
1. 	视图状态动画（Animate View State Changes）
1. 	矢量图动画（Vector 动画）
1. 	约束布局实现的关键帧动画（ConstraintSet 动画）
1. 	弹性动画 SpringAnimation
	support 25.3 之后出现的
1. 	Lottie (第三方开源动画)

参考 animator家族
							
##				插值器

 	定义：一个接口
 	作用：设置 属性值 从初始值过渡到结束值 的变化规律

1. 					内置的9种插值器
	1. 						动画加速进行	@android:anim/accelerate_interpolator	AccelerateInterpolator
	1. 						快速完成动画，超出再回到结束样式	@android:anim/overshoot_interpolator	OvershootInterpolator
	1. 						先加速再减速	@android:anim/accelerate_decelerate_interpolator	AccelerateDecelerateInterpolator
	1. 						先退后再加速前进	@android:anim/anticipate_interpolator	AnticipateInterpolator
	1. 						先退后再加速前进，超出终点后再回终点	@android:anim/anticipate_overshoot_interpolator	AnticipateOvershootInterpolator
	1. 						最后阶段弹球效果	@android:anim/bounce_interpolator	BounceInterpolator
	1. 						周期运动	@android:anim/cycle_interpolator	CycleInterpolator
	1. 						减速	@android:anim/decelerate_interpolator	DecelerateInterpolator
	1. 						匀速	@android:anim/linear_interpolator	LinearInterpolator
1. 					自定义插值器
	1. 						本质：根据动画的进度（0%-100%）计算出当前属性值改变的百分比
	1. 						具体使用：自定义插值器需要实现 Interpolator / TimeInterpolator接口 & 复写getInterpolation（）
##				估值器
1. 					定义：一个接口
1. 					作用：设置 属性值 从初始值过渡到结束值 的变化具体数值
1. 					估值器的种类
	1. 						ArgbEvaluator
	1. 						IntEvaluator
	1. 						IntArrayEvaluator
	1. 						FloatEvaluator
	1. 						FloatArrayEvaluator
	1. 						PointFEvaluator
1. 					自定义估值器
#			?问题
1. 				?知道SVG & 矢量动画吗
1. 				?说说转场动画
1. 				?谈插值器 & 估值器 的作用
1. 				?View动画和属性动画的区别
1. 				?Android动画框架实现的原理
1. 				?帧动画在使用时需要注意什么
