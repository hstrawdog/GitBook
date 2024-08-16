1. 首先在系统偏好设置中将软件更新中“自动保持我的Mac运行最新版本勾掉”；
2. 打开终端输入如下指令：

```
defaults write com.apple.systempreferences AttentionPrefBundleIDs 0

killall Dock

```



BTW:
恢复提醒的方式，终端输入：

```
sudo softwareupdate --reset-ignored
defaults write com.apple.systempreferences AttentionPrefBundleIDs 0

```

————————————————
版权声明：本文为CSDN博主「飘逝才子」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_38037451/article/details/112634688