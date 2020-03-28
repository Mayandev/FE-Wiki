# 浏览器的地址栏输入 URL 并按入回车之后发生的过程

1、浏览器的地址栏输入 URL 并按下回车。
2、浏览器查找当前 URL 是否存在缓存，并比较缓存是否过期。
3、DNS 解析 URL 对应的 IP。
4、根据 IP 建立 TCP 连接（三次握手）。
5、HTTP 发起请求。
6、服务器处理请求，浏览器接收 HTTP 响应。
7、渲染页面，构建 DOM 树。
8、关闭 TCP 连接（四次挥手）。
