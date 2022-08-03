#				WebView

1. 说说WebSettings & WebViewClient & WebChromeClient这三个类的作用 & 用法

1. WebView会导致内存泄露吗？原因是什么？解决方式有哪些？

1. JSBridge

1. Deeplink

1. 首屏加速

1. 离线包

1. 多进程WebView使用

#### WebView与js的通信 

   1.  ##### Android调用JS代码

      1. 通过WebView的loadUrl（）

         ```
         // 调用javascript的callJS()方法
         mWebView.loadUrl("javascript:callJS()");
         ```

         但是这种不常用，因为它会自动刷新页面而且没有返回值，有点影响交互。

      1. 通过WebView的evaluateJavascript（）

         ```
         mWebView.evaluateJavascript（"javascript:callJS()", new ValueCallback<String>() {
                 @Override
                 public void onReceiveValue(String value) {
                     //此处为 js 返回的结果
                 }
             });
         
         ```

         这种就比较全面了。调用方法并且获取返回值。

   1. ##### JS调用Android端代码

      1. **通过WebView的addJavascriptInterface（）进行对象映射**

         ```
         public class AndroidtoJs extends Object {
             // 定义JS需要调用的方法
             // 被JS调用的方法必须加入@JavascriptInterface注解
             @JavascriptInterface
             public void hello(String msg) {
                 System.out.println("JS调用了Android的hello方法");
             }
         }
         mWebView.addJavascriptInterface(new AndroidtoJs(), "test");
         //js中：
         function callAndroid(){
              // 由于对象映射，所以调用test对象等于调用Android映射的对象
              test.hello("js调用了android中的hello方法");
         }
         ```

         这种方法虽然很好用，但是要注意的是4.2以后，对于被调用的函数以@JavascriptInterface进行注解，否则容易出发漏洞，因为js方可以通过反射调用一些本地命令，很危险。

      1. 通过 WebViewClient 的shouldOverrideUrlLoading ()方法回调拦截 url

         这种方法是通过shouldOverrideUrlLoading回调去拦截url，然后进行解析，如果是之前约定好的协议，就调用相应的方法。

         ```
         // 复写WebViewClient类的shouldOverrideUrlLoading方法
         mWebView.setWebViewClient(new WebViewClient() {
                 @Override
                 public boolean shouldOverrideUrlLoading(WebView view, String url) {
            Uri uri = Uri.parse(url);                                 
                     // 如果url的协议 = 预先约定的 js 协议
                     if ( uri.getScheme().equals("js")) {
            // 如果 authority  = 预先约定协议里的 webview，即代表都符合约定的协议
                      if (uri.getAuthority().equals("webview")) {
                       System.out.println("js调用了Android的方法");
                       // 可以在协议上带有参数并传递到Android上
                       HashMap<String, String> params = new HashMap<>();
                       Set<String> collection = uri.getQueryParameterNames();
             }
                      return true;
                     }
                     return super.shouldOverrideUrlLoading(view, url);
                     }
                 }
             );
         ```



#### 如何避免WebView内存泄露

​		WebView的内存泄露主要是因为在页面销毁后，WebView的资源无法马上释放所导致的。现在主流的是两种方法：

  1. 不在xml布局中添加webview标签，采用在代码中new出来的方式，并在页面销毁的时候去释放webview资源

     ```
     //addview
     private WeakReference<BaseWebActivity> webActivityReference = new WeakReference<BaseWebActivity>(this);
     mWebView = new BridgeWebView(webActivityReference .get());
     webview_container.addView(mWebView);
     
     
     //销毁
     ViewParent parent = mWebView.getParent();
     if (parent != null) {
         ((ViewGroup) parent).removeView(mWebView);
     }
     mWebView.stopLoading();
     mWebView.getSettings().setJavaScriptEnabled(false);
     mWebView.clearHistory();
     mWebView.clearView();
     mWebView.removeAllViews();
     mWebView.destroy()；
     mWebView=null；
     ```

     

  2. 另起一个进程加载webview，页面销毁后干掉这个进程。但是这个方法的麻烦之处就在于进程间通信。

     ```
     <activity android:name=".WebActivity"
        android:process=":remoteweb"/>
     
     System.exit(0)   
     ```

     

#### webView还有哪些可以优化的地方

1. 提前初始化或者使用全局WebView。首次初始化WebView会比第二次初始化慢很多。初始化后，即使WebView已释放，但一些多WebView共用的全局服务/资源对想仍未释放，而第二次初始化不需要生成，因此初始化变快。
1. DNS采用和客户端API相同的域名，DNS解析也是耗时比较多的部分，所以用客户端API相同的域名因为其DNS会被缓存，所以打开webView的时候就不会再耗时在DNS上了
1. 对于JS的优化，尽量不要用偏重的框架，比如React。其次是高性能要求页面还是需要后端渲染。最后就是app中的网页框架要统一，这样就可以对js进行缓存和复用。
1. 美团团队的总结方案，如下：
   - WebView初始化慢，可以在初始化同时先请求数据，让后端和网络不要闲着。
   - 后端处理慢，可以让服务器分trunk输出，在后端计算的同时前端也加载网络静态资源。
   - 脚本执行慢，就让脚本在最后运行，不阻塞页面解析。
   - 同时，合理的预加载、预缓存可以让加载速度的瓶颈更小。
   - WebView初始化慢，就随时初始化好一个WebView待用。
   - DNS和链接慢，想办法复用客户端使用的域名和链接。
   - 脚本执行慢，可以把框架代码拆分出来，在请求页面之前就执行好。


#### WebView 在三件套下 加载完,网页高度不正确的问

参考 NestedScrollWebView

https://github.com/m5314/NestedScrollWebView