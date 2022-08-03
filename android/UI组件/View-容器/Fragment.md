# Fragment

1. Fragment懒加载怎么实现？/如何避免 onCreateView 多次执行
1. Fragment事务管理机制
1. Fragment 转场动画
1. 嵌套处理 getChildFragmentManager
1. 述说V4下的Fragment与Android下的Fragment有什么区别
1. fragment 重叠问题
1. FragmentPagerAdapter与FragmentStatePagerAdapter 区别与使用场景
1. getSupportFragmentManager  getFragmentManager  getChildFragmentManager 的区别
1. Fragment如何实现类似Activity栈的压栈和出栈效果的
1. 谈谈Activity和Fragment的区别？
1. FragmentManager中add与replace的hide区别（Fragment重叠）
1. Fragment初始化参数调用哪个方法？
1. Fragment在ViewPage中onCreateView 执行多次  retrurn View 是如何处理的



#### Fragment 与Activity之间如何通信

1. Activity 与 Fragment通信

   Activity有Fragment的实例，所以可以执行Fragment的方法，或者传入一个接口。同样，Fragment可以通过getActivity()获取Activity的实例，也是可以执行方法。

2. Fragment 与 Fragment之间通信

   1. 直接获取另一个Fragmetn的实例

      ```
      getActivity().getSupportFragmentManager().findFragmentByTag("mainFragment");
      ```

   2. 接口回调 一个Fragment里面去实现接口，另一个Fragment把接口实例传进去。

   3. Eventbus等框架。

#### Fragment的生命周期 
  1. onAttach()：Fragment和Activity相关联时调用。可以通过该方法获取Activity引用，还可以通过getArguments()获取参数。
  1. onCreate()：Fragment被创建时调用。
  1. onCreateView()：创建Fragment的布局。
  1. onActivityCreated()：当Activity完成onCreate()时调用。
  1. onStart()：当Fragment可见时调用。
  1. onResume()：当Fragment可见且可交互时调用。
  1. onPause()：当Fragment不可交互但可见时调用。
  1. onStop()：当Fragment不可见时调用。
  1. onDestroyView()：当Fragment的UI从视图结构中移除时调用。
  1. onDestroy()：销毁Fragment时调用。
  1. onDetach()：当Fragment和Activity解除关联时调用。

每个调用方法对应的生命周期变化：

  1. add(): onAttach()1.>…1.>onResume()。
  1. remove(): onPause()1.>…1.>onDetach()。
  1. replace(): 相当于旧Fragment调用remove()，新Fragment调用add()。remove()+add()的生命周期加起来
  1. show(): 不调用任何生命周期方法，调用该方法的前提是要显示的 Fragment已经被添加到容器，只是纯粹把Fragment UI的setVisibility为true。
  1. hide(): 不调用任何生命周期方法，调用该方法的前提是要显示的Fragment已经被添加到容器，只是纯粹把Fragment UI的setVisibility为false。