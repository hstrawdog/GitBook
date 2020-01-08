# ImageView

1. 				background 背景
1. 				foreground指的是前景

 foreground属性只有在以下两种情况下生效：

	* (1) Android M版本（6.0）及以上 ；
	* (2) FrameLayout本身及其子类。

1. src内容
1. adjustViewBounds

					用于设置缩放时是否保持原图长宽比。 

1. adjustViewBounds

1. alpha 透明度

	* 					android:alpha // 0f~1f
	* 					setAlpha(float alpha); // 0f~1f
	* 					setAlpha(int alpha); // 0~255,已过时
	* 					setImageAlpha(int alpha); // API>=16

1. scaleType

 1. android:scaleType=“center”
    	

    	保持原图的大小，显示在ImageView的中心。当原图的size大于ImageView的size时，多出来的部分被截掉。

    1. android:scaleType=“center_inside”

     以原图正常显示为目的，如果原图大小大于ImageView的size，就按照比例缩小原图的宽高，居中显示在ImageView中。如果原图size

    1. android:scaleType=“center_crop”

    	以原图填满ImageView为目的，如果原图size大于ImageView的size，则与center_inside一样，按比例缩小，居中显示在ImageView上。如果原图size小于ImageView的size，则按比例拉升原图的宽和高，填充ImageView居中显示。

    1. android:scaleType=“matrix”

    						不改变原图的大小，从ImageView的左上角开始绘制，超出部分做剪切处理。

    1. 	.androd:scaleType=“fit_xy”
        					
        把图片按照指定的大小在ImageView中显示，拉伸显示图片，不保持原比例，填满ImageView.
    1. 	.android:scaleType=“fit_start”

    						把原图按照比例放大缩小到ImageView的高度，显示在ImageView的start（前部/上部）。

    1. android:sacleType=“fit_center”

        把原图按照比例放大缩小到ImageView的高度，显示在ImageView的center（中部/居中显示）。

    1. android:scaleType=“fit_end”

     把原图按照比例放大缩小到ImageView的高度，显示在ImageVIew的end（后部/尾部/底部）

1. ImageView设置background和src的区别

1. adjustViewBounds

1. colorMatrix

1. 					