

# 描述一下BroadcastReceiver
  Broadcast Receiver用于接收并处理广播通知(broadcast announcements)。多数的广播是系统发起的，如地域变换、电量不足、[来电短信](https://www.baidu.com/s?wd=来电短信&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)等。程序也可以播放一个广播。程序可以有任意数量的broadcast receivers来响应它觉得重要的通知。Broadcast receiver可以通过多种方式通知用户: 启动activity、使用NotificationManager、开启背景灯、振动设备、播放声音等，最典型的是在状态栏显示一个图标，这样用户就可以点它打开看通知内容。通常我们的某个应用或系统本身在某些事件(电池电量不足、来电短信)来临时会广播一个Intent出去，我们利用注册一个broadcast

receiver来监听这些Intent并获取Intent中的数据

# 生命周期

# BroadcastReceiver对象的生命周期

# BroadcastReceiver所在进程的生命周期

BroadcastReceiver的创建有关系区分两种生命周期

[参考](https://blog.csdn.net/shaw1994/article/details/48342455)

# 两种注册方式

# 代码中动态注册

1. 实例化自定义的广播接收者
2. 实例化意图过滤器，并设置要过滤的广播类型（如，我们接收收到短信系统发出的广播）
3. 使用Context的registerReceiver(BroadcastReceiver, IntentFilter, String, Handler)方法注册广播

代码：



```java
//new出上边定义好的BroadcastReceiver
MyBroadCastReceiver yBroadCastReceiver = new MyBroadCastReceiver();

//实例化过滤器并设置要过滤的广播  
IntentFilter intentFilter = new IntentFilter("android.provider.Telephony.SMS_RECEIVED");

//注册广播   
myContext.registerReceiver(smsBroadCastReceiver,intentFilter, 
             "android.permission.RECEIVE_SMS", null);  
```

# 在Manifest.xml中静态注册

直接在`Manifest.xml`文件的``节点中配置广播接收者。



```xml
 <receiver android:name=".MyBroadCastReceiver">  
            <!-- android:priority属性是设置此接收者的优先级（从-1000到1000） -->
            <intent-filter android:priority="20">
            <actionandroid:name="android.provider.Telephony.SMS_RECEIVED"/>  
            </intent-filter>  
</receiver>  
```

还要在``同级的位置配置可能使用到的权限



```xml
<uses-permission android:name="android.permission.RECEIVE_SMS">
</uses-permission>
```

# 两种注册广播的不同

1. 第一种不是常驻型广播，也就是说广播跟随程序的生命周期。
2. 第二种是常驻型，也就是说当应用程序关闭后，如果有信息广播来，程序也会被系统调用自动运行。


# 广播的种类

1. 普通广播/无序广播（Normal Broadcast）

   ```java
       Intent intent = new  Intent();
           //设置intent的动作为com.example.broadcast，可以任意定义
           intent.setAction("com.example.broadcast");
           //发送无序广播
           sendBroadcast(intent);
   ```

2. 系统广播（System Broadcast）

3. 有序广播（Ordered Broadcast）

   和无序广播使用不同的是 通过 `mContext.sendOrderedBroadcast(Intent, String, BroadCastReceiver, Handler, int, String, Bundle)`和每个接收者设置优先级，就可以在小于自己优先级的接收者得到广播前，修改或终止广播。

   ```java
     Intent intent = new  Intent();
           //设置intent的动作为com.example.broadcast，可以任意定义
           intent.setAction("com.example.broadcast");
           //发送无序广播
           //第一个参数：intent
           //第二个参数：String类型的接收者权限
           //第三个参数：BroadcastReceiver 指定的接收者
           //第四个参数：Handler scheduler
           //第五个参数：int 此次广播的标记 
           //第六个参数：String 初始数据
           //第七个参数：Bundle 往Intent中添加的额外数据
           sendOrderedBroadcast(intent, null, null, null, "这是初始数据", );
   ```

   在Manifest.xml中配置该接收者。并设置优先级：MyReceiver1>MyReceiver2>MyReceiver3。

   ```xml
   <!-- 优先级相等的话，写在前面的receiver的优先级大于后面的 -->
   <receiver
               android:name=".MyReceiver1" >
               <!-- 定义广播的优先级 -->
               <intent-filter android:priority="1000">                
                   <!-- 动作设置为发送的广播动作 -->
                   <action android:name="com.example.broadcast"/>
               </intent-filter>
   </receiver>
   <receiver 
                  android:name=".MyReceiver2" >
                      <!-- 定义广播的优先级 -->
                      <intent-filter  android:priority="0">
                      <!-- 动作设置为发送的广播动作 -->
                      <action android:name="com.example.broadcast"/>
               </intent-filter>
   </receiver>
   <receiver 
                  android:name=".MyReceiver3" >
                      <!-- 定义广播的优先级 -->
                      <intent-filter  android:priority="-1000">
                      <!-- 动作设置为发送的广播动作 -->
                      <action android:name="com.example.broadcast"/>
               </intent-filter>
   </receiver>
   ```

4. 粘性广播（Sticky Broadcast）

5. App应用内广播（Local Broadcast）

# 是同步还是异步 接收是同步的 应为可以直接更新UI

# 可以执行耗时操作么

 現象:廣播接收器中進行耗時的I/O操作導致ANR。

查資料發現每次广播到来时 , 会重新创建 BroadcastReceiver 对象 , 并且调用 onReceive() 方法 , 执行完以后

该对象即被销毁 . 当 onReceive() 方法在 10 秒内没有执行完毕， Android 会认为该程序无响应 . 所以在 

BroadcastReceiver 里不能做一些比较耗时的操作 , 否侧会弹出 ANR(Application No Response) 的对话框.

解決辦法: 
  1. 在API11之前,如果需要完成一项比较耗时的工作 , 应该通过发送 Intent 给 Service, 由 Service 来完成 . 这里不能使用子线程来解决 , 因为 BroadcastReceiver 的生命周期很短 , 子线程可能还没有结束 BroadcastReceiver 就先结束了 .BroadcastReceiver 一旦结束 , 此时 BroadcastReceiver 的 所在进程很容易在系统需要内存时被优先杀死 , 因为它属于空进程 ( 没有任何活动组件的进程 ). 如果它的宿主进程被杀死 , 那么正在工作的子线程也会被杀死 . 所以采用子线程来解决是不可靠的(API11之前)
  1. API11以後可以調用goAsync()方法,這個方法會返回一個PendingResult對象,android系統會認為OnReceive()方法還沒有執行完成直到調用PendingResult.finish(),所以可以調用goAsync方法后，新开一个线程去执行耗時操作,執行完后調用PendingResult.finish()方法。這裡耗時的操作也不能超過10秒

https://www.cnblogs.com/krislight1105/p/3748327.html

## 直接更新UI好么 可以，为什么不可以呢？在实际开发中我们不是经常这么用么？ 为什么建议动态广播尽量在 onPause() 进行注销