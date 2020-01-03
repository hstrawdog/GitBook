# 自定义View/动画/Canvas

			View
				view的大小
					getWidth()
						getWidth（）获取的是这个view最终显示的大小，这个大小有可能等于原始的大小也有可能不等于原始大小。
					getMeasuredWidth()
						getMeasuredWidth()获取的是view原始的大小，也就是这个view在XML文件中配置或者是代码中设置的大小
					getMinimumWidth
						getMinimumWidth() 是最小宽度，是XML参数定义里的 minWidth，也是一个辅助测量展示的参数。
					getIntrinsicWidth()
						getIntrinsicWidth() 是原有宽度，有时候原有宽度可能很大，但是实际上空间不够，所有效果上并没有那么大，这个方法可以获得原有宽度，可以辅助测量的时候选择合适的展示宽度。
				getX，getRawX,getWidth,getTranslationX等的区别
					第一种是在onTouchEvent中
						event.getX()：表示的是触摸的点距离自身左边界的距离
						event.getY()：表示的是触摸的点距离自身上边界的距离
						event.getRawX：表示的是触摸点距离屏幕左边界的距离
						event.getRawY：表示的是触摸点距离屏幕上边界的距离
					第二种是在View中
						view.getTop()：子View的顶部到父View顶部的距离
						view.getRight()：子View的右边界到父View的左边界的距离
						view.getBottom()：子View的底部到父View的顶部的距离
						view.getLeft()：子View的左边界到父View的左边界的距离
						这四个值与父控件的padding和子控件的margin无关，不管这两个属性设置多少，四个值始终是子、父控件的边界差，认准边界即可。
						view.getTranslationX()：计算的是该View在X轴的偏移量。初始值为0，向左偏移值为负，向右偏移值为正。
						view.getTranslationY()：计算的是该View在Y轴的偏移量。初始值为0，向上偏移为负，向下偏移为正。
						view.getX=view.getTranslationX()+view.getLeft()
						view.getY=view.getTranslationY()+view.getTop()
					第三种是在支持滑动的父控件中
						需要说明的一点是：当屏幕滑动时，并不是父控件在移动，而是父控件中的子控件在移动(view表示父控件)
						view.getScrollX：父控件中的子控件在x方向上的滚动距离
						view.getScrollY：父控件中的子控件在y方向上的滚动距离
					
					参考
						参考1 
						参考2
				View的六种滑动
					scrollTo与scrollBy
						scrollTo
							传入目标点 
								用于边界判断 或者初始化的时候滑动
						scrollBy
							滑动距离 
								配合MotionEvent进行滑动效果
						对于View来说：
							mScrollX：View的内容(content)相对于View本身在水平方向的偏移量。
							mScrollY：:View的内容(content)相对于View本身在垂直方向的偏移量。
							scrollTo(int x, int y)：将一个视图的内容移动到指定位置.此时偏移量 mScrollX,mScrollY就分别等于x,y.
							scrollBy(int x, int y)： 在现有的基础上继续移动视图的内容.
						对于ViewGroup来说：
							移动的是它对应的所有子View。
						注意：
							scrollTo()和scrollBy()移动的只是View的内容,但是View的背景是不移动的.
							滑动后的距离可以通过 getScrollX getScrollY 获取
						参考
							参考1
					layout(方法)
					offsetLeftAndroidRight()与offsetTopAndButtom()
					layoutParams(改变布局参数)
					动画
					Scroller
			onMeasure
				注意 在约束布局下设置machParent 设置宽度会出现无效
			ViewGroup
			Canvas
				Paint(画笔)
					文字测量
						FontMetrics
							基准点是baseline
							Ascent是baseline之上至字符最高处的距离
							Descent是baseline之下至字符最低处的距离
							Leading文档说的很含糊，其实是上一行字符的descent到下一行的ascent之间的距离
							Top指的是指的是最高字符到baseline的值，即ascent的最大值
							bottom指的是最下字符到baseline的值，即descent的最大值
							参考
					抗锯齿
						setAntiAlias
							true
								开启
							false
								清除
					宽度
						setStrokeWidth
							只有在空心的时候才会生效
					样式
						setStyle
							空心/描边
								STROKE
							填充
								FILL
							填充内部和描边
								FILL_AND_STROKE
					画笔颜色
						setColor
						setARGB
					透明度
						setAlpha
					重置
						reset
					阴影效果
						setShadowLayer
					文字大小
						setTextSize
					设置字体的水平方向的缩放因子
						setTextScaleX
							默认值为1
					文本在水平方向上的倾斜
						setTextSkewX
							推荐值为-0.25
					行的间距
						setLetterSpacing
							默认值是0，负值行间距会收缩
					字体样式
						setFontFeatureSettings
							设置CSS样式
					参考
				Path(路径)
				变换
					平移
						translate
					缩放
						scale
					旋转
						rotate
					斜拉
						skew
					裁剪
						clipRect
						clipPath
				绘制
					背景
						drawColor
						drawRGB
						drawARGB
					点
						drawPoint
						drawPoints
					线
						drawLine
						drawLines
					矩形
						drawRect
						drawRoundRect
					圆形
						drawCircle
					路径多边形
						drawPath
						贝赛尔曲线
					图片
						drawBitmap
						drawPicture
					椭圆
						drawOval
					圆弧
						drawArc
							drawArc(@NonNull RectF oval, float startAngle, float sweepAngle, boolean useCenter,\n	    @NonNull Paint paint)
							drawArc(float left, float top, float right, float bottom, float startAngle,\n	    float sweepAngle, boolean useCenter, @NonNull Paint paint)
							参考
					文字
						drawText
						drawPosText
						drawTextOnPath
				快照
					保存当前状态
						save
					回滚到上一次保存的状态
						restore
					保存图层状态
						saveLayerXxx
					回滚到指定状态
						restoreToCount
					获取保存次数
						getSaveCount
				矩阵
					getMatrix
					setMatrix
					concat
				顶点操作
					drawVertices
					drawBitmapMesh
				参考
					https://www.jianshu.com/p/1fddeb8ec9fe
			事件分发
				Activity
					dispatchTouchEvent
					onTouchEvent
				Group
					dispatchTouchEvent
					onInterceptTouchEvent
					onTouchEvent
				View
					dispatchTouchEvent
					onTouchEvent
				流程图
					 
				参考
					参考1
			动画
				Android中的动画分为哪些种类
					ValueAnimator(属性动画)
						TimeInterpolator(插值器)
							LinearInterpolator(匀速)
								@android:anim/linear_interpolator
							DecelerateInterpolator(减速)
								@android:anim/decelerate_interpolator
							CycleInterpolator(周期运动)
								@android:anim/cycle_interpolator
							BounceInterpolator(最后阶段弹球效果)
								@android:anim/bounce_interpolator
							AnticipateOvershootInterpolator(先退后再加速前进，超出终点后再回终点)
								@android:anim/anticipate_overshoot_interpolator
							AnticipateInterpolator(先退后再加速前进)
								@android:anim/anticipate_interpolator
							AccelerateDecelerateInterpolator(先加速再减速)
								@android:anim/accelerate_decelerate_interpolator
							OvershootInterpolator(快速完成动画，超出再回到结束样式)
								@android:anim/overshoot_interpolator
							AccelerateInterpolator(动画加速进行)
								@android:anim/accelerate_interpolator
						TypeEvaluator(估值器)
							IntEvaluator：针对整型属性 
							FloatEvaluator：针对浮点型属性 
							ArgbEvaluator：针对Color属性
							PointFEvaluator:针对Point属性
						ObjectAnimator
						TimeAnimator
						AnimatorSet(动画集合)
						Animator监听器
							AnimatorListener
								onAnimationStart() - 当动画开始的时候调用.
								onAnimationEnd() - 动画结束时调用.
								onAnimationRepeat() - 动画重复时调用.
								onAnimationCancel() - 动画取消时调用.取消动画也会调用onAnimationEnd，它不会关系动画是怎么结束的。
								ValueAnimator.AnimatorUpdateListener中的接口
								onAnimationUpdate()动画中每一帧更新的时候调用
							AnimatorListenerAdapter
						Animator在xml中
						参考
							animator家族
					视图动画（View 动画）
					帧动画（Frame 动画、Drawable 动画）
					触摸反馈动画（Ripple Effect）
					揭露动画（Reveal Effect）
					转场动画 & 共享元素（Activity 切换动画）
					视图状态动画（Animate View State Changes）
					矢量图动画（Vector 动画）
					约束布局实现的关键帧动画（ConstraintSet 动画）
					弹性动画 SpringAnimation
						support 25.3 之后出现的
					Lottie (第三方开源动画)
				插值器
					定义：一个接口
					作用：设置 属性值 从初始值过渡到结束值 的变化规律
					内置的9种插值器
						动画加速进行	@android:anim/accelerate_interpolator	AccelerateInterpolator
						快速完成动画，超出再回到结束样式	@android:anim/overshoot_interpolator	OvershootInterpolator
						先加速再减速	@android:anim/accelerate_decelerate_interpolator	AccelerateDecelerateInterpolator
						先退后再加速前进	@android:anim/anticipate_interpolator	AnticipateInterpolator
						先退后再加速前进，超出终点后再回终点	@android:anim/anticipate_overshoot_interpolator	AnticipateOvershootInterpolator
						最后阶段弹球效果	@android:anim/bounce_interpolator	BounceInterpolator
						周期运动	@android:anim/cycle_interpolator	CycleInterpolator
						减速	@android:anim/decelerate_interpolator	DecelerateInterpolator
						匀速	@android:anim/linear_interpolator	LinearInterpolator
					自定义插值器
						本质：根据动画的进度（0%-100%）计算出当前属性值改变的百分比
						具体使用：自定义插值器需要实现 Interpolator / TimeInterpolator接口 & 复写getInterpolation（）
				估值器
					定义：一个接口
					作用：设置 属性值 从初始值过渡到结束值 的变化具体数值
					估值器的种类
						ArgbEvaluator
						IntEvaluator
						IntArrayEvaluator
						FloatEvaluator
						FloatArrayEvaluator
						PointFEvaluator
					自定义估值器
			?问题
				?知道SVG & 矢量动画吗
				?说说转场动画
				?谈插值器 & 估值器 的作用
				?View动画和属性动画的区别
				?Android动画框架实现的原理
				?帧动画在使用时需要注意什么
