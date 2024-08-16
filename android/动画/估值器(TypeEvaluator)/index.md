#				估值器

- 定义：一个接口

- 作用：设置 属性值 从初始值过渡到结束值 的变化具体数值

   > 插值器（Interpolator）决定值的变化规律（匀速、加速等等），即决定的是变化趋势；而估值器决定数值的具体变化。
   > 属性动画特有的属性。

- 应用场景：配合插值器一起使用，实现非线性运动的动画效果。

- 估值器的种类

   1. 						ArgbEvaluator 以Argb类型的形式从初始值 - 结束值 进行过渡
   1. 						IntEvaluator 以整型的形式从初始值 - 结束值 进行过渡
   1. 						IntArrayEvaluator
   1. 						FloatEvaluator  以浮点型的形式从初始值 - 结束值 进行过渡
   1. 						FloatArrayEvaluator
   1. 						PointFEvaluator

- 自定义估值器

