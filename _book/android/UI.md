# UI

			TextView 文本
				TextView
					SpannableStringBuilder
						Span
							ForegroundColorSpan	设置文字颜色
							BackgroundColorSpan	设置背景色
							StrikethroughSpan	设置删除线样式
							UnderlineSpan	设置下划线样式
							URLSpan：设置链接样式（配合LinkMovementMethod）
							ClickableSpan	设置可点击样式（配合LinkMovementMethod）
							StyleSpan	设置粗体、斜体等样式（1为粗体、2为斜体、3为粗斜体）
							SubscriptSpan	设置下标样式
							SuperscriptSpan	设置上标样式
					常用属性
						DrawableXXX
						android:textAllCaps = "true"	是否自动将小写字母转化为大写字母	实测自动将我们的字母转化成大写字母
						android:textStyle = "bold"	字体风格，可选值为[bold、italic、normal][加粗、斜体、正常]	实测有效
						android:maxLines = "3"	最大行数	实测有效（多余的部分将被直接省略），设置为1行时直接使用（android:singleLine = "true"）
						android:minLines = "1"	最小行数	实测有效（缺少的部分由空白填充 等于 设置了对应行数的高度）
						android:ellipsize = "end"	设置文字长度超出TextView时出现省略符号的位置。可选值为[none、start 、end、middle、marquee][无省略符、开头、结尾、中间、跑马灯模式]。当选择marquee时需要配合singleLine使用	测试有效，但是需要配合单行使用，不是单行时，会自动换行，并且跑马灯的效果还需要设置一个 android:focusableInTouchMode="true" 属性才可以动起来
						android:drawableXXX = "@drawable/img"	用于在文字周围设置图片	实测有效，但是需要注意的是，图片会显示它本身的大小，如果Tv设置了高度，那么图片也只是显示这么高/宽的内容，如果是自适应，那么图片将会直接显示原大小。
						android:lineSpacingExtra = "10dp"	设置行间距	实测有效
						android:lineSpacingMultiplier = "0.5"	设置行间距的倍数	实测有效，与上面的属性一起用更好哦
						android:textIsSelectable = "true"	文本内容是否可以选中	实测有效，这样子我们的TextView显示的内容就能被选中复制了
						android:textColorHighlight = "@color/blue"	文本被选中后高亮显示的颜色	实测有效，与上面的内容一起使用更好哦
						android:autoLink = "all"	设置需要自动识别的链接格式。可选值为[none、all、email、phone、web][不识别、全部识别、邮箱、电话号码、网址]	实测有效，可放心食用
						android:textColorLink = "@color/red"	设置链接颜色	实测有效，与上面的属性一起用更好哦
						android:letterSpacing = "1.5"	以标准字体宽度的倍数作为字符间距	实测有效，但是最低支持到API 21
					图片要入如何居中在宽度最大的情况下
						layer-list
					HTML
						fromHtml
						Html.ImageGetter
				EditText
					限制输入的小技巧
						inputType
						setFilters
						digits
							DigitsKeyListener
							android:digits
					焦点
						父布局设置两个属性失去焦点
							Parent.setFocusable(true);\nParent.setFocusableInTouchMode(true);
							android:focusable="true"\nandroid:focusableInTouchMode="true"
						EditText自动获取焦点并弹出键盘
							EditText.setFocusable(true);   \nEditText.setFocusableInTouchMode(true);\nEditText.requestFocus();
					TextWatcher
						beforeTextChanged
							输入过程中执行该方法
						onTextChanged
							输入前确认执行该方法
						afterTextChanged
							输入结束执行该方法
					游标
					底部横线
					输入类型
			ImageView
				background 背景
				foreground指的是前景
					foreground属性只有在以下两种情况下生效：
					(1) Android M版本（6.0）及以上 ；
					(2) FrameLayout本身及其子类。
				src内容
				adjustViewBounds
					用于设置缩放时是否保持原图长宽比。 adjustViewBounds
				alpha 透明度
					android:alpha // 0f~1f
					setAlpha(float alpha); // 0f~1f
					setAlpha(int alpha); // 0~255,已过时
					setImageAlpha(int alpha); // API>=16
				ScaleType
					MATRIX / matrix：用矩阵的方式绘制，从ImageView的左上角开始绘制原图，不缩放图片， 超过ImageView部分作裁剪处理；
					CENTER / center：保持原图的大小，显示在ImageView的中心。当原图的尺寸大于ImageView的尺寸，超过部分裁剪处理；
					CENTER_CROP / centerCrop：保持横纵比缩放图片，直到完全覆盖ImageView为止（指的是ImageView的宽和高都要填满），原图超过ImageView的部分作裁剪处理；
					CENTER_INSIDE / centerInside：将图片的内容完整居中显示，通过按比例缩小原图尺寸的宽高等于或小于ImageView的宽高。如果原图的尺寸本身就小于ImageView的尺寸，则原图的尺寸不作任何处理，居中显示在ImageView；
					FIT_XY / fitXY：把原图宽高进行不保持原比例放缩，直到填充满ImageView为止；
					FIT_START / fitStart：把原图按比例放缩使之等于ImageView的宽高，缩放完成后将图片放在ImageView的左上角；
					FIT_CENTER / fitCenter：把原图按比例放缩使之等于ImageView的宽高使之居中显示，缩放后放于中间；
					FIT_END / fitEnd：把原图按比例放缩到ImageView的宽高，缩放完成后将图片放在ImageView的右下角
			Button 按钮
				Button
				Switch
				CheckBox
				RadioGroup
				RadioButton
			widgets 小部件
				SeekBar
				ProgressBar
				RatingBar
				ImageView
					scaleType
						android:scaleType=“center”
							保持原图的大小，显示在ImageView的中心。当原图的size大于ImageView的size时，多出来的部分被截掉。
						android:scaleType=“center_inside”
							以原图正常显示为目的，如果原图大小大于ImageView的size，就按照比例缩小原图的宽高，居中显示在ImageView中。如果原图size
						android:scaleType=“center_crop”
							以原图填满ImageView为目的，如果原图size大于ImageView的size，则与center_inside一样，按比例缩小，居中显示在ImageView上。如果原图size小于ImageView的size，则按比例拉升原图的宽和高，填充ImageView居中显示。
						android:scaleType=“matrix”
							不改变原图的大小，从ImageView的左上角开始绘制，超出部分做剪切处理。
						.androd:scaleType=“fit_xy”
							把图片按照指定的大小在ImageView中显示，拉伸显示图片，不保持原比例，填满ImageView.
						.android:scaleType=“fit_start”
							把原图按照比例放大缩小到ImageView的高度，显示在ImageView的start（前部/上部）。
						android:sacleType=“fit_center”
							把原图按照比例放大缩小到ImageView的高度，显示在ImageView的center（中部/居中显示）。
						android:scaleType=“fit_end”
							把原图按照比例放大缩小到ImageView的高度，显示在ImageVIew的end（后部/尾部/底部）
					ImageView设置background和src的区别
					adjustViewBounds
					colorMatrix
				WebView
					说说WebSettings & WebViewClient & WebChromeClient这三个类的作用 & 用法
					WebView会导致内存泄露吗？原因是什么？解决方式有哪些？
					JSBridge
					Deeplink
					首屏加速
					离线包
			containers 容器
				ScrollView
				NestedScrollView
				Toolbar
				TabLayout
					28.+与27.+的差异
					如何实现底部横线与文字大小一致
					如何自定义item
				RecycleView
					为什么要用RecycleView
					RecycleView与ListView的区别
					RecycleView的三级缓存/四级缓存
					如何实现点击/长按功能
					如何将item滑动到顶部
						LayoutManager.scrollToPositionWithOffset
						如果item内容超过一个屏幕怎么办
					DiffUtil类差异更新
					如何进行局部刷新
				Fragment
					懒加载/如何避免 onCreateView 多次执行
					述说V4下的Fragment与Android下的Fragment有什么区别
					fragment 重叠问题
					FragmentPagerAdapter与FragmentStatePagerAdapter 区别
					getSupportFragmentManager  getFragmentManager  getChildFragmentManager 的区别
					Fragment如何实现类似Activity栈的压栈和出栈效果的
				ListView
					ListView 如何优化
						 ViewHolder配合setTag getTag 是否是空的 避免多次导入
					getView 执行多次问题
					ListView  嵌套EditText 焦点问题
				DrawerLayout
				ViewPage
					ViewPage2
					ViewPage
						ViewPage搭配Fragment 如何处理内存泄漏
			Layout 布局
				LinearLayout 线性布局
				RelativeLayout 相对布局
				FrameLayout 帧布局
				TableLayout 表格布局
				AbsoluteLayout 绝对布局 (已过时)
				ConstainLayout 约束布局
				FlexboxLayout 弹性布局
				MotionLayout 约束布局的子类
				折叠布局(微博折叠三件套)
					CoordinatorLayout
					AppBarLayout
					CollapsingToolbarLayout
				抽象布局(布局优化)
					include
					Viewstub
					merge
				?
					LinearLayout 和 RelativeLayout 相同层级下效率比较
			View  自定义
				View的事件分发
					能给我谈谈Android中坐标体系吗？
					.OnTouchListener & OnTouchEvent & onClickListener三者之间的关系
					说说事件分发的流程 
				View的绘制流程
				在Activity中如何获取View的高度
				说说Activity View树结构
				自定义View的方式有哪些
				自定义View时常常重写的一些方法？
				自定义View中如何自定义属性
				requestLayout(),onLayout(),onDraw(),drawChild()区别和联系
				如何计算出一个View的嵌套层级
				自定义View如何考虑机型适配
				MotionEvent是什么？包含几种事件？什么条件下会产生？
				scrollTo()和scrollBy()的区别？
				Scroller中最重要的两个方法是什么？主要目的是？
				MeasureSpec是什么？有什么作用？
				自定义View/ViewGroup需要注意什么？
				onTouch()、onTouchEvent()和onClick()关系？
				invalidate()和postInvalidate()的区别？
				SurfaceView和View的区别？
				ViewGroup 绘制顺序
			Tint 着色
				tintMode
					multiply
					screen
					src_in(默认)
					src_over
					src_atop
					add
				不支持shape的边框 简单的纯色可以是用tint 着色
				ImagView\nImageButton 
					tint
						src
					backgroundTint
						背景
					foregroundTint
						前景
				button\nEditText\ntextView
					backgroundTint
					foregroundTint
					drawableTint
				ProgressBar
					backgroundTint
					foregroundTint
					IndeterminateTint
					ProgressBackgroundTint
					ProgressTint
					SecondaryProgressTint
			屏幕适配
				抖音轻量级屏幕适配
					说说实现的原理
					他的优点与缺点
				资源文件适配
				ppi px与dp之间的关系
				其他适配方案
					鸿洋的百分比适配
			Toask
				权限问题
					系统禁用通知权限 无法显示toask
			dialog
				dialog
				dialogFragment
			PopupWindow
				PopupWindow和Dialog区别

	