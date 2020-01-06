# Service

# 两种启动方式

# 生命周期

# Service保活方案

# Service中能否进行耗时操作

Service默认并不会运行在子线程中，也不运行在一个独立的进程中，它同样执行在主线程中（UI线程）。也就是说，我们不要在Service中进行耗时操作，否则可能会出现主线程被阻塞（ANR）的情况

# 常用的系统Service都有哪些

1. WindowManager
2. LayoutInflater
3. ActivityManager
4. NotificationManager
5. LocationManager
6. ConnectivityManager
7. WifiManager
8. AudioManager
9. InputMethodManager
10. DownloadManager
11. AlarmManager

# IntentService

# JobService