# script 标签中 defer 和 async 的区别

默认情况下，脚本的下载和执行将会按照文档的先后顺序同步进行。当脚本下载和执行的时候，文档解析就会被阻塞，在脚本下载和执行完成之后文档才能往下继续进行解析。

- async 会将 js 的`加载与执行`文档的加载并行进行
- defer 会将 js 的加载与文档加载并行执行，js 的执行在加载之后。

下图展示了区别：

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/fe-wiki-html-2.jpeg)
