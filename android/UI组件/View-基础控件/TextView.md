# TextView

#				TextView

##					SpannableStringBuilder

### 						Span

* 							ForegroundColorSpan	设置文字颜色
* 							BackgroundColorSpan	设置背景色
* 							StrikethroughSpan	设置删除线样式
* 							UnderlineSpan	设置下划线样式
* 							URLSpan：设置链接样式（配合LinkMovementMethod）
* 							ClickableSpan	设置可点击样式（配合LinkMovementMethod）
* 							StyleSpan	设置粗体、斜体等样式（1为粗体、2为斜体、3为粗斜体）
* 							SubscriptSpan	设置下标样式
* 							SuperscriptSpan	设置上标样式

##					[属性大全](https://blog.csdn.net/qq_34368586/article/details/86595354)

* 						DrawableXXX
* 						android:textAllCaps = "true"	是否自动将小写字母转化为大写字母	实测自动将我们的字母转化成大写字母
* 						android:textStyle = "bold"	字体风格，可选值为[bold、italic、normal][加粗、斜体、正常]	实测有效
* 						android:maxLines = "3"	最大行数	实测有效（多余的部分将被直接省略），设置为1行时直接使用（android:singleLine = "true"）
* 						android:minLines = "1"	最小行数	实测有效（缺少的部分由空白填充 等于 设置了对应行数的高度）
* 						android:ellipsize = "end"	设置文字长度超出TextView时出现省略符号的位置。可选值为[none、start 、end、middle、marquee][无省略符、开头、结尾、中间、跑马灯模式]。当选择marquee时需要配合singleLine使用	测试有效，但是需要配合单行使用，不是单行时，会自动换行，并且跑马灯的效果还需要设置一个 android:focusableInTouchMode="true" 属性才可以动起来
* 						android:drawableXXX = "@drawable/img"	用于在文字周围设置图片	实测有效，但是需要注意的是，图片会显示它本身的大小，如果Tv设置了高度，那么图片也只是显示这么高/宽的内容，如果是自适应，那么图片将会直接显示原大小。
* 						android:lineSpacingExtra = "10dp"	设置行间距	实测有效
* 						android:lineSpacingMultiplier = "0.5"	设置行间距的倍数	实测有效，与上面的属性一起用更好哦
* 						android:textIsSelectable = "true"	文本内容是否可以选中	实测有效，这样子我们的TextView显示的内容就能被选中复制了
* 						android:textColorHighlight = "@color/blue"	文本被选中后高亮显示的颜色	实测有效，与上面的内容一起使用更好哦
* 						android:autoLink = "all"	设置需要自动识别的链接格式。可选值为[none、all、email、phone、web][不识别、全部识别、邮箱、电话号码、网址]	实测有效，可放心食用
* 						android:textColorLink = "@color/red"	设置链接颜色	实测有效，与上面的属性一起用更好哦
* 						android:letterSpacing = "1.5"	以标准字体宽度的倍数作为字符间距	实测有效，但是最低支持到API 21

## 图片要入如何居中在宽度最大的情况下

1. 						layer-list

##					HTML

1. 						fromHtml
1. 						Html.ImageGetter