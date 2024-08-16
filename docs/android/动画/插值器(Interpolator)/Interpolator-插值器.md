# Interpolator 插值器

##				

定义：一个接口
作用：设置 属性值 从初始值过渡到结束值 的变化规律

1. 					内置的9种插值器
        1. 						动画加速进行	@android:anim/accelerate_interpolator	AccelerateInterpolator
        1. 						快速完成动画，超出再回到结束样式	@android:anim/overshoot_interpolator	OvershootInterpolator
        1. 						先加速再减速	@android:anim/accelerate_decelerate_interpolator	AccelerateDecelerateInterpolator
        1. 						先退后再加速前进	@android:anim/anticipate_interpolator	AnticipateInterpolator
        1. 						先退后再加速前进，超出终点后再回终点	@android:anim/anticipate_overshoot_interpolator	AnticipateOvershootInterpolator
        1. 						最后阶段弹球效果	@android:anim/bounce_interpolator	BounceInterpolator
        1. 						周期运动	@android:anim/cycle_interpolator	CycleInterpolator
        1. 						减速	@android:anim/decelerate_interpolator	DecelerateInterpolator
        1. 						匀速	@android:anim/linear_interpolator	LinearInterpolator
1. 					自定义插值器
        1. 						本质：根据动画的进度（0%-100%）计算出当前属性值改变的百分比
        1. 						具体使用：自定义插值器需要实现 Interpolator / TimeInterpolator接口 & 复写getInterpolation（）

##				

- AccelerateDecelerateInterpolator   在动画开始与介绍的地方速率改变比较慢，在中间的时候加速
- AccelerateInterpolator                     在动画开始的地方速率改变比较慢，然后开始加速
- AnticipateInterpolator                      开始的时候向后然后向前甩
- AnticipateOvershootInterpolator     开始的时候向后然后向前甩一定值后返回最后的值
- BounceInterpolator                          动画结束的时候弹起
- CycleInterpolator                             动画循环播放特定的次数，速率改变沿着正弦曲线
- DecelerateInterpolator                    在动画开始的地方快然后慢
- LinearInterpolator                            以常量速率改变
- OvershootInterpolator                      向前甩一定值后再回到原来位置

