
- Path 将多种复合路径（多个轮廓，如直线段、二次曲线、立方曲线）封装在其内部的几何路径 (BaseView)
    -   paint.setPathEffect();
         - CornerPathEffect——圆形拐角效果  public CornerPathEffect(float radius)  
         - DashPathEffect——虚线效果  
            public DashPathEffect(float intervals[], float phase) 
            intervals  长度必须大于等于2；因为必须有一个实线段和一个空线段来组成虚线。
            个数必须为偶数，如果是基数，最后一个数字将被忽略；这个很好理解，因为一组虚线的组成必然是一个实线和一个空线成对组成的
            phase：开始绘制的偏移值 
         - DiscretePathEffect——离散路径效果   
            public DiscretePathEffect(float segmentLength, float deviation)  
            第一个参数segmentLength：表示将原来的路径切成多长的线段。如果值为2，那么这个路径就会被切成一段段由长度为2的小线段。所以这个值越小，所切成的小线段越多；这个值越大，所切成的小线段越少。 
            第二参数deviation：表示被切成的每个小线段的可偏移距离。值越大，就表示每个线段的可偏移距离就越大，就显得越凌乱，值越小，每个线段的可偏移原位置的距离就越小
          - PathDashPathEffect——印章路径效果 
            public PathDashPathEffect(Path shape, float advance, float phase,Style style)   
            Path shape:表示印章路径，比如我们下面示例中的三角形加右上角一个点；
            float advance：表示两个印章路径间的距离,很容易理解，印章间距离越大，间距就越大。
            float phase：路径绘制偏移距离，与上面DashPathEffect中的float phase参数意义相同
            Style style：表示在遇到转角时，如何操作印章以使转角平滑过渡，取值有：Style.ROTATE，Style.MORPH，Style.TRANSLATE;Style.ROTATE表示通过旋转印章来过渡转角；Style.MORPH表示通过变形印章来过渡转角；Style.TRANSLATE表示通过位移来过渡转角。这三个效果的具体意义，上面会通过具体示例来分别讲解。
    - 直线路径
        - void moveTo (float x1, float y1):直线的开始点；即将直线路径的绘制点定在（x1,y1）的位置
        - void lineTo (float x2, float y2)：直线的结束点，又是下一次绘制直线路径的开始点；lineTo（）可以一直用
        - void close ():如果连续画了几条直线，但没有形成闭环，调用Close()会将路径首尾点连接起来，形成闭环
    - 矩形路径
        - void addRect (float left, float top, float right, float bottom, Path.Direction dir)
        - void addRect (RectF rect, Path.Direction dir) 
        这里Path类创建矩形路径的参数与上篇canvas绘制矩形差不多，唯一不同的一点是增加了Path.Direction参数；
        Path.Direction有两个值：
        Path.Direction.CCW：是counter-clockwise缩写，指创建逆时针方向的矩形路径；
        Path.Direction.CW：是clockwise的缩写，指创建顺时针方向的矩形路径
    - 圆角矩形路径    
        - void addRoundRect (RectF rect, float[] radii, Path.Direction dir)
        - void addRoundRect (RectF rect, float rx, float ry, Path.Direction dir)
        第一个构造函数：可以定制每个角的圆角大小：
        float[] radii：必须传入8个数值，分四组，分别对应每个角所使用的椭圆的横轴半径和纵轴半径，如｛x1,y1,x2,y2,x3,y3,x4,y4｝，其中，x1,y1对应第一个角的（左上角）用来产生圆角的椭圆的横轴半径和纵轴半径，其它类推……
        第二个构造函数：只能构建统一圆角大小
        float rx：所产生圆角的椭圆的横轴半径；
        float ry：所产生圆角的椭圆的纵轴半径
    - 圆形路径 
        -  void addCircle (float x, float y, float radius, Path.Direction dir)
            参数说明：
            float x：圆心X轴坐标 
            float y：圆心Y轴坐标
            float radius：圆半径   
    - 椭圆路径    
        - void addOval (RectF oval, Path.Direction dir)
        参数说明：
        RectF oval：生成椭圆所对应的矩形
        Path.Direction :生成方式，与矩形一样，分为顺时针与逆时针，意义完全相同，不再重复
    - 弧形路径   
        -  void addArc (RectF oval, float startAngle, float sweepAngle)
        参数：
        RectF oval：弧是椭圆的一部分，这个参数就是生成椭圆所对应的矩形；
        float startAngle：开始的角度，X轴正方向为0度
        float sweepAngel：持续的度数；
    - 线段轨迹
        - void quadTo (float x1, float y1, float x2, float y2)
    - canvas变换与操作
        - 平移（translate） void translate(float dx, float dy)
        参数说明：
        float dx：水平方向平移的距离，正数指向正方向（向右）平移的量，负数为向负方向（向左）平移的量
        flaot dy：垂直方向平移的距离，正数指向正方向（向下）平移的量，负数为向负方向（向上）平移的量
    - 旋转（Rotate）
        - void rotate(float degrees)
        - void rotate (float degrees, float px, float py)
        第一个构造函数直接输入旋转的度数，正数是顺时针旋转，负数指逆时针旋转，它的旋转中心点是原点（0，0）
        第二个构造函数除了度数以外，还可以指定旋转的中心点坐标（px,py）
    - 缩放（scale ）
        - public void scale (float sx, float sy) 
        - public final void scale (float sx, float sy, float px, float py)
        float sx:水平方向伸缩的比例，假设原坐标轴的比例为n,不变时为1，在变更的X轴密度为n*sx;所以，sx为小数为缩小，sx为整数为放大
        float sy:垂直方向伸缩的比例，同样，小数为缩小，整数为放大
    - 扭曲（skew）   
        - void skew (float sx, float sy)
        参数说明：
        float sx:将画布在x方向上倾斜相应的角度，sx倾斜角度的tan值，
        float sy:将画布在y轴方向上倾斜相应的角度，sy为倾斜角度的tan值，
    - 裁剪画布（clip系列函数）   
        - boolean  clipPath(Path path)
        -  boolean clipPath(Path path, Region.Op op)
        -  boolean clipRect(Rect rect, Region.Op op)
         - boolean clipRect(RectF rect, Region.Op op)
         - boolean clipRect(int left, int top, int right, int bottom)
        -  boolean clipRect(float left, float top, float right, float bottom)
        -  boolean clipRect(RectF rect)
        -  boolean clipRect(float left, float top, float right, float bottom, Region.Op op)
         - boolean clipRect(Rect rect)
         - boolean clipRegion(Region region)
         - boolean clipRegion(Region region, Region.Op op)
    - 画布的保存与恢复（save()、restore()）     
       - int save ()
       -  void restore()  






#### 基本属性与方法

1. moveto 移动
2. lineto 画线
3. rect 画矩形
4. arcTo (矩形 , 起点,  角度)
5. reset  清除
6. close  闭合
7. quadTo  二阶贝塞尔曲线
8. cubicTo  三阶贝塞尔曲线