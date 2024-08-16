# Animator(动画)

1. ValueAnimator(属性动画)
   1. 						TimeInterpolator(插值器)
   1. 						TypeEvaluator(估值器)
   1. 						ObjectAnimator
   1. 						TimeAnimator
   1. 						AnimatorSet(动画集合)
   1. 						Animator监听器
            1. 								AnimatorListener
            1. 								onAnimationStart() - 当动画开始的时候调用.
            1. 								onAnimationEnd() - 动画结束时调用.
            1. 								onAnimationRepeat() - 动画重复时调用.
            1. 								onAnimationCancel() - 动画取消时调用.取消动画也会调用onAnimationEnd，它不会关系动画是怎么结束的。
            1. 								ValueAnimator.AnimatorUpdateListener中的接口
            1. 								onAnimationUpdate()动画中每一帧更新的时候调用
                                  				AnimatorListenerAdapter
   1. 						Animator在xml中

1. 视图动画（View 动画）
1. 帧动画（Frame 动画、Drawable 动画）
1. 触摸反馈动画（Ripple Effect）
1. 揭露动画（Reveal Effect）
1. 转场动画 & 共享元素（Activity 切换动画）
1. 视图状态动画（Animate View State Changes）
1. 矢量图动画（Vector 动画）
1. 约束布局实现的关键帧动画（ConstraintSet 动画）
1. 弹性动画 SpringAnimation
   support 25.3 之后出现的
1. Lottie (第三方开源动画)







https://www.jianshu.com/p/53759778284a

https://github.com/OCNYang/Android-Animation-Set