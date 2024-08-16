- Paint 
  - paint.setAntiAlias(true);//抗锯齿功能
  - paint.setColor(Color.RED);  //设置画笔颜色    
  - paint.setStrokeWidth(30);//设置画笔宽度
  - paint.setTextSize(12);//设置文字大小  
  - paint.setStyle(Style.FILL);//设置填充样式
    - Paint.Style.FILL    :填充内部
    - Paint.Style.FILL_AND_STROKE  ：填充内部和描边
    - Paint.Style.STROKE  ：仅描边
  - paint.setShadowLayer (float radius, float dx, float dy, int color)    添加阴影
    - radius:阴影的倾斜度
    - dx:水平位移
    - dy:垂直位移
  - setStrokeCap(Paint.Cap cap)
    - BUTT 无线帽
    - SQUARE 方形线帽
    - ROUND 圆形线帽
  - paint.setFakeBoldText(true);//设置是否为粗体文字  
  - paint.setUnderlineText(true);//设置下划线  
  - paint.setTextSkewX((float) -0.25);//设置字体水平倾斜度，普通斜体字是-0.25  
  - paint.setStrikeThruText(true);//设置带有删除线效果  
  - paint.setTextAlign(Paint.Align.XXX);
    - LEFT
    - CENTER
    - RIGHT
      原点(x,y)在矩形的 左 居中 右 
  - paint.setStrokeJoin(Paint.Join.MITER);  
        - Join.MITER（结合处为锐角）
        -  Join.Round(结合处为圆弧)
        -  Join.BEVEL(结合处为直线)
  - paint.setTextScaleX(2);//只会将水平方向拉伸，高度不会变  
  - paint.setTypeface(typeface); 字体样式设置（Typeface）
    -  Typeface   create(String familyName, int style) //直接通过指定字体名来加载系统中自带的文字样式
    -  Typeface   create(Typeface family, int style)     //通过其它Typeface变量来构建文字样式
    -  Typeface    createFromAsset(AssetManager mgr, String path) //通过从Asset中获取外部字体来显示字体样式
    -  Typeface  createFromFile(String path)//直接从路径创建
    -  Typeface   createFromFile(File path)//从外部路径来创建字体样式
    -  Typeface  defaultFromStyle(int style)//创建默认字体
       上面的各个参数都会用到Style变量,Style的枚举值如下:
       Typeface.NORMAL  //正常体
       Typeface.BOLD  //粗体
       Typeface.ITALIC    //斜体
       Typeface.BOLD_ITALIC //粗斜体
    -  使用系统中的字体
       - Typeface defaultFromStyle(int style)//创建默认字体
       - Typeface   create(String familyName, int style) //直接通过指定字体名来加载系统中自带的文字样式
    -  自字义字体
       -  Typeface    createFromAsset(AssetManager mgr, String path) //通过从Asset中获取外部字体来显示字体样式
       -  Typeface    createFromFile(String path)//直接从路径创建
       -  Typeface    createFromFile(File path)//从外部路径来创建字体样式  







##				Paint(画笔)

1. 文字测量FontMetrics

   * 基准点是baseline
   *Ascent是baseline之上至字符最高处的距离
   * Descent是baseline之下至字符最低处的距离
   * Leading文档说的很含糊，其实是上一行字符的descent到下一行的ascent之间的距离
   * Top指的是指的是最高字符到baseline的值，即ascent的最大值
   * bottom指的是最下字符到baseline的值，即descent的最大值

1. 抗锯齿 setAntiAlias

   - true 开启

   - false 清除

1. setStrokeWidth 画笔宽度 只有在空心的时候才会生效

1. setStyle  样式 

   2. 空心/描边 STROKE
   2. 填充 FILL
   2. 填充内部和描边 FILL_AND_STROKE

1. 画笔颜色

   1. setColor
   1. setARGB

1. setAlpha 透明度

1. reset 重置

1. setShadowLayer 阴影效果 

1. setTextSize 文字大小

1. setTextScaleX 设置字体的水平方向的缩放因子  默认值为1

1. setTextSkewX 文本在水平方向上的倾斜  

   推荐值为-0.25

1. setLetterSpacing 行的间距  

   默认值是0，负值行间距会收缩

1. setFontFeatureSettings 字体样式  

   设置CSS样式