





我们在自定义 View 控件时随处可见 Matrix 的身影，主要用于坐标转换映射，我们可以通过 Matrix 矩阵来控制视图的变换。

Matrix 本质上是一个如下图所示的矩阵：

上面每个值都有其对应的操作。
Matrix 提供了如下几个操作：

缩放（Scale）
对应 MSCALE_X 与 MSCALE_Y

位移（Translate）
对应 MTRANS_X 与 MTRANS_Y

错切（Skew）
对应 MSKEW_X 与 MSKEW_Y

旋转（Rotate）
旋转没有专门的数值来计算，Matrix 会通过计算缩放与错切来处理旋转。



https://blog.csdn.net/u013872857/article/details/91905511