# Framework

##				Application

1. 					getApplicationContext和getApplication是不是返回同一个对象

##				系统服务(service)

1. 					常用的系统服务
        *					ActivityManagerService	负责四大组件的启动、切换、调度。
        *					PackageManagerService	用来对apk进行安装、解析、删除、卸载等等操作
        *					WindowManagerService	窗口管理服务
        *					CameraService	摄像头相关服务
        *					InputManagerService	管理输入事件
        *					NotificationManagerService	通知管理服务
        *					LocationManagerService	定位管理服务

##				Window

1. 					Window有哪几种类型？
        *					系统Window
        *					应用程序Window
        *					子Window
1. 					Activity创建和Dialog创建过程的异同？
1. 					Window、Activity、DecorView以及ViewRoot

##				启动流程

1. 					Activity启动过程
1. 					APP启动过程
1. 					Android应用进程启动
1. 					Android Apk安装过程
1. 					Android系统启动过程
        *					system_server启动过程

## Manager

1. WindowManager 

   调用window，设置window里面screenBrightness参数的值，但却短暂设置屏幕亮度的亮度，在某个activity下面才可以生效

2. ActivityManager

    与系统中正在运行的所有活动进行交互。

3. ConnectivityManager 

   主要管理网络连接相关操作

4. WifiManager 

   无线管理相关的，类似获得wifi链接名字，判断是否链接，开关等一些和无线相关

5. PowerManager 

   主要是用来控制电源状态，设置屏幕状态，和电池待机状态

6. ServiceManager 

7. FragmentManager 

    在Activity中与Fragment进行交互的接口

8. PackageManager

    检索当前安装在设备上的应用程序包相关的各种信息

9. DownloadManager

    下载管理器是一个系统服务，处理长时间运行的HTTP下载

9. NotificationManager

    通知用户发生的事件

11. TelephonyManager

     提供访问设备上的电话服务的信息

12. LocationManager

     提供了系统位置服务的访问

13. AlarmManager

     提供系统报警服务的访问

##				binder工作原理

1. AIDL配置文件
2. C/S架构Binder原理
3. Messager
4. 其他IPC通信方式

##				如果工作中需要修改framework，你如何寻找切入点

##				通讯

1. 					WIFI
1. 					NFC
1. 					蓝牙