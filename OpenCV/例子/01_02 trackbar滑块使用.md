

# 例子

```python
import cv2 as cv
import numpy as np


def callback(pos):
    pass

# 创建窗口
cv.namedWindow('trackbar', cv.WINDOW_NORMAL)

# 创建滑块
cv.createTrackbar('R', 'trackbar', 10, 255, callback)
cv.createTrackbar('G', 'trackbar', 20, 255, callback)
cv.createTrackbar('B', 'trackbar', 30, 255, callback)

#  创建图片  (宽,高,通道) 
img = np.zeros((480, 460, 3), np.uint8)

while True:
    #  读取滑块值
    r = cv.getTrackbarPos('R', 'trackbar')
    g = cv.getTrackbarPos('G', 'trackbar')
    b = cv.getTrackbarPos('B', 'trackbar')
    #  设置图片颜色   bgr格式 不是rgb
    img[:] = [b, g, r]
    # 显示
    cv.imshow('trackbar', img)

    key = cv.waitKey(10)
    if key & 0xff == ord('q'):
        break

cv.destroyAllWindows()

```

# API  

创建一个轨迹栏并将其附加到指定的窗口。

函数 createTrackbar 创建具有指定名称和范围的轨迹条（滑块或范围控件），将变量值分配为与轨迹条同步的位置，并指定在轨迹条位置变化时调用的回调函数 onChange。 创建的轨迹栏显示在指定的窗口winname中。

- int cv::createTrackbar	(	const String & 	trackbarname,const String & 	winname,int * 	value,int 	count,TrackbarCallback 	onChange = 0,void * 	userdata = 0 )		
  - trackbarname 创建的轨迹栏的名称。
  - winname 将用作已创建轨迹栏的父级的窗口的名称。
  - value 指向一个整数变量的可选指针，其值反映了滑块的位置。创建时，滑块位置由此变量定义
  - count 滑块的最大位置。最小位置始终为 0
  - onChange 指向每次滑块改变位置时要调用的函数的指针。 这个函数的原型应该是 void Foo(int,void*); ，其中第一个参数是trackbar位置，第二个参数是用户数据（见下一个参数）。 如果回调是 NULL 指针，则不调用回调，而只更新值。
  - userdata 按原样传递给回调的用户数据。它可用于在不使用全局变量的情况下处理轨迹栏事件。

- cv.getTrackbarPos(trackbarname, winname) ->retval
  - trackbarname 轨迹栏的名称
  - winname 作为轨迹栏父级的窗口的名称

​	返回轨迹栏位置。 该函数返回指定轨迹栏的当前位置。

