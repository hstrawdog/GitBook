### 插值器（Interpolator）

- 定义：一个接口

- 作用：设置属性值从初始值过渡到结束值 的变化规律，如匀速、加速 & 减速等等
   ，即确定了 动画效果变化的模式，如匀速变化、加速变化等等。

- 应用场景：实现非线性运动的动画效果

  链接：https://www.jianshu.com/p/676bb3b4d71d
  

> 非线性运动：动画改变的速率不是一成不变的，如加速 & 减速运动都属于非线性运动

- 系统内置插值器类型

| 作用                                 | 资源ID                                           | 对应的Java类                     |
| ------------------------------------ | ------------------------------------------------ | -------------------------------- |
| 动画加速进行                         | @android:anim/accelerate_interpolator            | AccelerateInterpolator           |
| 快速完成动画，超出再回到结束样式     | @android:anim/overshoot_interpolator             | OvershootInterpolator            |
| 先加速再减速                         | @android:anim/accelerate_decelerate_interpolator | AccelerateDecelerateInterpolator |
| 先退后再加速前进                     | @android:anim/anticipate_interpolator            | AnticipateInterpolator           |
| 先退后再加速前进，超出终点后再回终点 | @android:anim/anticipate_overshoot_interpolator  | AnticipateOvershootInterpolator  |
| 最后阶段弹球效果                     | @android:anim/bounce_interpolator                | BounceInterpolator               |
| 周期运动                             | @android:anim/cycle_interpolator                 | CycleInterpolator                |
| 减速                                 | @android:anim/decelerate_interpolator            | DecelerateInterpolator           |
| 匀速                                 | @android:anim/linear_interpolator                | LinearInterpolator               |
| 路径 | |PathInterpolator|