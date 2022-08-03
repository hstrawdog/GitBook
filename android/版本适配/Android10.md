1. 暗黑模式
1. 隐私增强(后台能否访问定位)
1. 限制程序访问剪贴板
1. 应用黑盒
1. 权限细分需兼容
1. 后台定位单独权限需兼容
1. 设备唯一标示符需兼容
1. 后台打开Activity 需兼容
1. 非 SDK 接口限制 需兼容
1. 不能获取imei、imsi等 用oaid代替
1. 使用androidx库代替了support库，没有了suppory库
1. 后台打开activity做了限制
	1. 应用某个activity刚启动不久
	2. 最近activity调用了finish()（只适用调用了finish() ）前台任务返回栈中能找到该actviity 
	3. 收到另一个可见应用发送的pendingInten通知、 
	4. 点击通知栏打开activity 
	5. 授权了悬浮窗的权限等等）
1. 分区储存（支持不使用分区储存）
1. 引入新的定位权限background location（后台获取定位 获取限制 1. activity可见 2. 服务为前台服务）
1. 一些电话 API、蓝牙 API 和 WLAN API 需要精确位置权限

# 分区存储

`Android 10` 引入了分区存储，但不是强制的，可以通过清单配置`android:requestLegacyExternalStorage="true"`关闭分区存储

