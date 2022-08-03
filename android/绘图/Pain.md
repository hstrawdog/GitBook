##				Paint(画笔)

1. 文字测量FontMetrics

   * 							基准点是baseline
   * 							Ascent是baseline之上至字符最高处的距离
   * 							Descent是baseline之下至字符最低处的距离
   * 							Leading文档说的很含糊，其实是上一行字符的descent到下一行的ascent之间的距离
   * 							Top指的是指的是最高字符到baseline的值，即ascent的最大值
   * 							bottom指的是最下字符到baseline的值，即descent的最大值

1. 抗锯齿 setAntiAlias

   - true 开启

   - false 清除

1. setStrokeWidth 画笔宽度 只有在空心的时候才会生效

1. setStyle  样式 

   2.						空心/描边 STROKE
   2.						填充 FILL
   2.						填充内部和描边 FILL_AND_STROKE

1. 画笔颜色

   2.					setColor
   2.					setARGB

1. setAlpha 透明度

1. reset 重置

1. setShadowLayer 阴影效果 

1. setTextSize 文字大小

1. setTextScaleX 设置字体的水平方向的缩放因子  默认值为1

1. setTextSkewX 文本在水平方向上的倾斜  

    推荐值为-0.25

1. setLetterSpacing 行的间距  

   默认值是0，负值行间距会收缩

1.  setFontFeatureSettings 字体样式  

   设置CSS样式