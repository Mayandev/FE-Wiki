# 什么是跨域，如何解决跨域

## 什么是跨域

当一个请求 url 的协议、域名、端口三者之间任意一个与当前页面 url 不同即为跨域。

DOM 具有同源策略，即禁止对不同源页面DOM进行操作。

非同源站点有这样一些限制:

- 不能读取和修改对方的 DOM
- 不读访问对方的 Cookie、IndexDB 和 LocalStorage
- 限制 XMLHttpRequest 请求。

## 如何解决

### 1. jsonp


通常为了减轻 web 服务器端压力，我会会把 js、css、html 等静态资源放到另一台独立的域名服务器，在 html 页面中再通过相应的标签从不同域名下加载静态资源，而被浏览器允许，基于此原理，我们可以通过动态创建script，再请求一个带参网址实现跨域通信。

原生实现：

```html
<script>
    var script = document.createElement('script');
    script.type = 'text/javascript';

    // 传参一个回调函数名给后端，方便后端返回时执行这个在前端定义的回调函数
    script.src = 'http://www.domain2.com:8080/login?user=admin&callback=handleCallback';
    document.head.appendChild(script);

    // 回调执行函数
    function handleCallback(res) {
        alert(JSON.stringify(res));
    }
 </script>
```

以淘宝的扫码登录页面为例，页面会定时轮询服务器判断用户是否扫码，每次轮询都是一次 jsonp 操作，返回一个回调函数，判断扫码状态。

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/fe-wiki-http-1.png)


轮询的请求参数如下：

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/fe-wiki-http-2.png)


响应回来的是一段 jsonp 代码：

```javascript
// 轮询响应
(function(){jsonp742({"code":"10000","message":"login start state","success":true});})();
```

### 2. document.domain + iframe

如果主域名相同，子域不同，可以设置 docoument.domain 解决跨域问题。

实现原理：因为浏览器是通过document.domain属性来检查两个页面是否同源，因此只要通过设置相同的document.domain，两个页面就可以共享Cookie（此方案仅限主域相同，子域不同的跨域应用场景。

1.）父窗口：(http://www.domain.com/a.html)

```html
<iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
<script>
    document.domain = 'domain.com';
    var user = 'admin';
</script>
```

2.）子窗口：(http://child.domain.com/b.html)

```html
<script>
    document.domain = 'domain.com';
    // 获取父窗口中变量
    alert('get js data from parent ---> ' + window.parent.user);
</script>
```



### 3. postMessage

postMessage是HTML5 XMLHttpRequest Level 2中的API，且是为数不多可以跨域操作的window属性之一，它可用于解决以下方面的问题：
a.） 页面和其打开的新窗口的数据传递
b.） 多窗口之间消息传递
c.） 页面与嵌套的iframe消息传递
d.） 上面三个场景的跨域数据传递

用法：postMessage(data,origin)方法接受两个参数
data： html5规范支持任意基本类型或可复制的对象，但部分浏览器只支持字符串，所以传参时最好用JSON.stringify()序列化。
origin： 协议+主机+端口号，也可以设置为"*"，表示可以传递给任意窗口，如果要指定和当前窗口同源的话设置为"/"。

1.）a.html：(http://www.domain1.com/a.html)

```html
<iframe id="iframe" src="http://www.domain2.com/b.html" style="display:none;"></iframe>
<script>       
    var iframe = document.getElementById('iframe');
    iframe.onload = function() {
        var data = {
            name: 'aym'
        };
        // 向domain2传送跨域数据
        iframe.contentWindow.postMessage(JSON.stringify(data), 'http://www.domain2.com');
    };

    // 接受domain2返回数据
    window.addEventListener('message', function(e) {
        alert('data from domain2 ---> ' + e.data);
    }, false);
</script>
```

2.）b.html：(http://www.domain2.com/b.html)

```html
<script>
    // 接收domain1的数据
    window.addEventListener('message', function(e) {
        alert('data from domain1 ---> ' + e.data);

        var data = JSON.parse(e.data);
        if (data) {
            data.number = 16;

            // 处理后再发回domain1
            window.parent.postMessage(JSON.stringify(data), 'http://www.domain1.com');
        }
    }, false);
</script>
```

### CORS

CORS 是跨域资源分享（Cross-Origin Resource Sharing）的缩写。它是 W3C 标准，属于跨源 AJAX 请求的根本解决方法。

**1、普通跨域请求：只需服务器端设置Access-Control-Allow-Origin**

**【服务端设置】**

服务器端对于CORS的支持，主要是通过设置Access-Control-Allow-Origin来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。

**2、带cookie跨域请求：前后端都需要进行设置**

xhr.withCredentials = true;

```js
$.ajax({
   url: 'http://www.test.com:8080/login',
   type: 'get',
   data: {},
   xhrFields: {
       withCredentials: true    // 前端设置是否带cookie
   },
   crossDomain: true,   // 会让请求头中包含跨域的额外信息，但不会含cookie
});
```

### Nginx 代理

Nginx 是一种高性能的反向代理服务器，可以用来轻松解决跨域问题。

**正向代理**

帮助客户端访问客户端自己访问不到的服务器，然后将结果返回给客户端。

**反向代理**

反向代理拿到客户端的请求，将请求转发给其他的服务器，主要的场景是维持服务器集群的**负载均衡**，换句话说，反向代理帮**其它的服务器**拿到请求，然后选择一个合适的服务器，将请求转交给它。

反向代理是一个请求分发的机制，正向代理则是将请求收集。

那么 Nginx 代理是如何解决跨域的呢？

比如说现在客户端的域名为 **domain1.com**，服务器的域名为**domain2.com**，客户端向服务器发送 Ajax 请求，当然会跨域了，那这个时候让 Nginx 登场了，通过下面这个配置:

```nginx
server {
  listen  80;
  server_name  domain1.com;
  location /api {
    proxy_pass domain2.com;
  }
}
```

Nginx 向接收到 domain1.com 的请求，然后作为反向代理，将请求转发给 domain2.com，当响应返回时又将响应给到客户端，这就完成了整个跨域请求的流程。





