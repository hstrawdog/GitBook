# RecycleView

# Recycleview四级缓存

|                    |                                               |                                             |                                                              |
| ------------------ | --------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------ |
| 类型               | 变量名                                        | 存储说明                                    | 备注                                                         |
| Scrap              | mAttachedScrap屏幕内                          | 存放可见范围内的 ViewHolder                 | 从这里复用的 ViewHolder 如果 position 或者 id 对应的上，则不需要重新绑定数据。在 onLayoutChildren 的时候，会将所有 View 都会缓存到这 |
| mChangedScrap      | 存放可见范围内并且数据发生了变化的 ViewHolder | 从这里复用的 ViewHolder 需要重新绑定数据。  |                                                              |
| Cache              | mCachedViews 屏幕外                           | 存放 remove 掉的 ViewHolder                 | 从这里复用的 ViewHolder 如果 position 或者 id 对应的上，则不需要重新绑定数据。 |
| ViewCacheExtension | mViewCacheExtension                           | 自定义缓存                                  | 自定义缓存                                                   |
| RecycledViewPool   | mRecyclerPool 缓存池                          | 存放 remove 掉，并且重置了数据的 ViewHolder | 从这里复用的 ViewHolder 需要重新绑定数据。                   |


1. mAttachedScrap(屏幕内)

   用于屏幕内itemview快速重用，不需要重新createView和bindView

1. mCacheViews(屏幕外)

   保存最近移出屏幕的ViewHolder，包含数据和position信息，复用时必须是相同位置的ViewHolder才能复用，应用场景在那些需要来回滑动的列表中，当往回滑动时，能直接复用ViewHolder数据，不需要重新bindView。

1. mViewCacheExtension(自定义缓存)

   不直接使用，需要用户自定义实现，默认不实现

1. mRecyclerPool(缓存池)

   当cacheView满了后或者adapter被更换，将cacheView中移出的ViewHolder放到Pool中，放之前会把ViewHolder数据清除掉，所以复用时需要重新bindView

1. [为什么要用RecycleView](http://zjutkz.net/2016/08/10/%E6%88%91%E4%BB%AC%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E4%BD%BF%E7%94%A8RecyclerView/)

  - 效率 多级缓存池
  -  解耦  拓展性强
  -  灵活 可以深层的定制或者灵活修改 动画效果之类的
  -  专注 没有多余与列表无关的东西

1. RecycleView 与 ListView的区别

1. RecycleVIew 与ListView  有哪些优势

1. 如何实现点击/长按功能

1. 如何将item滑动到顶部

1. LayoutManager.scrollToPositionWithOffset

1. 如果item内容超过一个屏幕怎么办

1. DiffUtil类差异更新

1. 如何进行局部刷新

1. 布局管理器LayoutMager

1. 条目装饰ItemDecoretion

1. ViewHoleder与回收复用机制

1. [RecycleView item悬停](https://stackoverflow.com/questions/32949971/how-can-i-make-sticky-headers-in-recyclerview-without-external-lib?tdsourcetag=s_pctim_aiomsg)

1. #### Recycleview 缓存过程

      四级缓存按照顺序需要依次读取。所以完整缓存流程是：

      1) 保存缓存流程：

         - 插入或是删除itemView时，先把屏幕内的ViewHolder保存至AttachedScrap中

         - 滑动屏幕的时候，先消失的itemview会保存到CacheView，CacheView大小默认是2，超过数量的话按照先入先出原则，移出头部的itemview保存到RecyclerPool缓存池（如果有自定义缓存就会保存到自定义缓存里），RecyclerPool缓存池会按照itemview的itemtype进行保存，每个itemTyep缓存个数为5个，超过就会被回收。

      2) 获取缓存流程：
         - AttachedScrap中获取，通过pos匹配holder——>获取失败，从CacheView中获取，也是通过pos获取holder缓存 ——>获取失败，从自定义缓存中获取缓存——>获取失败，从mRecyclerPool中获取 ——>获取失败，重新创建viewholder——createViewHolder并bindview。

      需要注意的是，如果从缓存池找到缓存，还需要重新bindview

      

1. #### 说说RecyclerView性能优化

      1. bindViewHolder方法是在UI线程进行的，此方法不能耗时操作，不然将会影响滑动流畅性。比如进行日期的格式化。

      1. 对于新增或删除的时候，可以使用diffutil进行局部刷新，少用全局刷新

      1. 对于itemVIew进行布局优化，比如少嵌套等。

      1. 25.1.0 (>=21)及以上使用Prefetch 功能，也就是预取功能，嵌套时且使用的是LinearLayoutManager，子RecyclerView可通过setInitialPrefatchItemCount设置预取个数

      1. 加大RecyclerView缓存，比如cacheview大小默认为2，可以设置大点，用空间来换取时间，提高流畅度

      1. 如果高度固定，可以设置setHasFixedSize(true)来避免requestLayout浪费资源，否则每次更新数据都会重新测量高度。

           ```
           void onItemsInsertedOrRemoved() {
              if (hasFixedSize) layoutChildren();
              else requestLayout();
           }
           ```
           
      1. 如果多个RecycledView 的 Adapter 是一样的，比如嵌套的 RecyclerView 中存在一样的 Adapter，可以通过设置 RecyclerView.setRecycledViewPool(pool);来共用一个 RecycledViewPool。这样就减少了创建VIewholder的开销。
      1. 在RecyclerView的元素比较高，一屏只能显示一个元素的时候，第一次滑动到第二个元素会卡顿。这种情况就可以通过设置额外的缓存空间，重写getExtraLayoutSpace方法即可。
      
           ```java
           new LinearLayoutManager(this) {
               @Override
               protected int getExtraLayoutSpace(RecyclerView.State state) {
                   return size;
               }
           };
           ```
           
      1. 设置RecyclerView.addOnScrollListener();来在滑动过程中停止加载的操作。
      2. 减少对象的创建，比如设置监听事件，可以全局创建一个，所有view公用一个listener，并且放到CreateView里面去创建监听，因为CreateView调用要少于bindview。这样就减少了对象创建所造成的消耗
      3. 用notifyDataSetChange时，适配器不知道整个数据集中的那些内容以及存在，再重新匹配ViewHolder时会花生闪烁。设置adapter.setHasStableIds(true)，并重写getItemId()来给每个Item一个唯一的ID，也就是唯一标识，就使itemview的焦点固定，解决了闪烁问题。

