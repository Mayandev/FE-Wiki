# 扫码登录的实现原理

### 扫码登录原理

以淘宝为例，当点击扫码登录时，网页首先会请求二维码服务器，生成一张二维码。请求与响应如下图：


![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/image-20200310144235069.png)


```js
// 响应
(function(){jsonp31({"success":true,"message":"null","url":"//img.alicdn.com/imgextra/O1CN01f1PcX71rdZwYau2rM_!!5654-2-xcode.png","lgToken":"ca0cc7172af3df24af63ee6ffa30ffca","adToken":"aea482731a37b083002fd48d4089ed90"});})();
```

可以看到，响应返回了二维码的URL，以及一个重要的参数`lgToken`，这是是网页的唯一ID。

这时，网页开始不断的轮询，判断用户是否扫码登录，每次的请求轮询都会将`lgToken `带上。

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/image-20200310143345387.png)

轮询的请求参数如下：
![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/image-20200310143321062.png)

响应回来的是一段 jsonp 代码：

```javascript
// 轮询响应
(function(){jsonp742({"code":"10000","message":"login start state","success":true});})();
```

当轮询时发现二维码过期时，则轮询停止。响应的 code 为 10004，message 为 `QRCode expired!code=1, msg=data not exist`

```js
// 二维码过期响应
(function(){jsonp2683({"code":"10004","message":"QRCode expired!code=1, msg=data not exist","success":true});})();
```

点击刷新二维码，网页会再次请求二维码接口，生成新的二维码，并再次开启轮询。

当用户使用手机扫描二维码后，响应 code 变为10001，并提示扫描成功。


![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/image-20200310145205920.png)

当用户在手机上点击确认登录时，会将用户信息以及二维码上的信息传到服务器并重新生成令牌token。当网页端再次轮询请求接口时，就返回真正的登陆态Token,网页端此时就可以凭着这个Token来登陆了。