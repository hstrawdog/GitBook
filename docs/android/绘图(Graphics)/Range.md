
- 区域（Range）
    - 基本构造函数     
       -  public Region()  //创建一个空的区域  
       -   public Region(Region region) //拷贝一个region的范围  
       -  public Region(Rect r)  //创建一个矩形的区域  
       -   public Region(int left, int top, int right, int bottom) //创建一个矩形的区域       
       第二个构造函数是通过其它的Region来复制一个同样的Region变量
       第三个，第四个才是正规常的，根据一个矩形或矩形的左上角和右下角点构造出一个矩形区域
   - 间接构造
       - public void setEmpty()  //置空
       -  public boolean set(Region region)   
       -  public boolean set(Rect r)   
       -  public boolean set(int left, int top, int right, int bottom)   
       -  public boolean setPath(Path path, Region clip)
       这是Region所具有的一系列Set方法，我这里全部列了出来，下面一一对其讲解：
       注意：无论调用Set系列函数的Region是不是有区域值，当调用Set系列函数后，原来的区域值就会被替换成Set函数里的区域。
       SetEmpty（）：从某种意义上讲置空也是一个构造函数，即将原来的一个区域变量变成了一个空变量，要再利用其它的Set方法重新构造区域。
       set(Region region)：利用新的区域值来替换原来的区域
       set(Rect r)：利用矩形所代表的区域替换原来的区域
       set(int left, int top, int right, int bottom)：同样，根据矩形的两个点构造出矩形区域来替换原来的区域值
       setPath(Path path, Region clip)：根据路径的区域与某区域的交集，构造出新区域，这个后面具体讲解
   -  使用SetPath（）构造不规则区域
        -  boolean setPath (Path path, Region clip)
        Path path：用来构造的区域的路径
        Region clip：与前面的path所构成的路径取交集，并将两交集设置为最终的区域
        由于路径有很多种构造方法，而且可以轻意构造出非矩形的路径，这就摆脱了前面的构造函数只能构造矩形区域的限制。但这里有个问题是要指定另一个区域来取共同的交集，当然如果想显示路径构造的区域，Region clip参数可以传一个比Path范围大的多的区域，取完交集之后，当然是Path参数所对应的区域喽。机智的孩子     
   -  矩形集枚举区域——RegionIterator类
        - RegionIterator(Region region) //根据区域构建对应的矩形集
        -  boolean next(Rect r) //获取下一个矩形，结果保存在参数Rect r 中
   - 区域的合并、交叉等操作
        - public final boolean union(Rect r)   
        - public boolean op(Rect r, Op op) {  
        - public boolean op(int left, int top, int right, int bottom, Op op)   
        - public boolean op(Region region, Op op)   
        - public boolean op(Rect rect, Region region, Op op)    
          ```
            public enum Op {    
                   DIFFERENCE(0), //最终区域为region1 与 region2不同的区域    
                   INTERSECT(1), // 最终区域为region1 与 region2相交的区域    
                   UNION(2),      //最终区域为region1 与 region2组合一起的区域    
                   XOR(3),        //最终区域为region1 与 region2相交之外的区域    
                   REVERSE_DIFFERENCE(4), //最终区域为region2 与 region1不同的区域    
                   REPLACE(5); //最终区域为为region2的区域    
     
   - 其它一些方法
         /**几个判断方法*/    
           public native boolean isEmpty();//判断该区域是否为空    
           public native boolean isRect(); //是否是一个矩阵    
           public native boolean isComplex();//是否是多个矩阵组合    
           /**一系列的getBound方法，返回一个Region的边界*/    
           public Rect getBounds()     
           public boolean getBounds(Rect r)     
           public Path getBoundaryPath()     
           public boolean getBoundaryPath(Path path)   
            
           /**一系列的判断是否包含某点 和是否相交*/    
           public native boolean contains(int x, int y);//是否包含某点    
           public boolean quickContains(Rect r)   //是否包含某矩形  
           public native boolean quickContains(int left, int top, int right,    
                                                   int bottom) //是否没有包含某矩阵形   
            public boolean quickReject(Rect r) //是否没和该矩形相交    
            public native boolean quickReject(int left, int top, int right, int bottom); //是否没和该矩形相交    
            public native boolean quickReject(Region rgn);  //是否没和该矩形相交    
               
           /**几个平移变换的方法*/    
           public void translate(int dx, int dy)     
           public native void translate(int dx, int dy, Region dst);    
         
