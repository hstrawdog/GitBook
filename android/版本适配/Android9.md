# Android 9 (28) : Pie

- 利用 Wi-Fi RTT 进行室内定位

- 刘海屏 API 支持

- 多摄像头支持和摄像头更新

- 不允许调用hide api

- 室内WIFI定位

- “刘海”屏幕支持
- 安全增强
- 等等优化很多

#### 限制明文流量的网络请求 http

Android P 限制了明文流量的网络请求，非加密的流量请求都会被系统禁止掉

解决方案：

  在资源文件新建xml目录，新建文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
复制代码
```

  清单文件配置：

```xml
<application
        android:networkSecurityConfig="@xml/network_security_config">
        <!--9.0加的，哦哦-->
        <uses-library
            android:name="org.apache.http.legacy"
            android:required="false" />
    </application>
复制代码
```

  但还是建议都使用https进行传输