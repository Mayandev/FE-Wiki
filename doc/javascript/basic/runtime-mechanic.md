# JavaScript 运行机制


- 第一个是JavaScript Engine，chrome 的引擎就是 V8（提供调用栈、内存 heap）
- 第二个是 WEb API，提供一些 dom 操作、ajax 的操作
- 第三个是 回调队列，也就是Web API 里的回调函数，回放入到回调队列中
- 第四个是事件循环，也就是宏任务、微任务的容器

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/javascript-run-mechanic.png)

**call stack**

是追踪函数执行流的一种机制，通过调用栈，可以知道当前哪一个函数正在被执行。每当调用一个函数，解释器就将改函数添加至调用栈并开始执行。如果正在执行的函数还调用了其他函数，那么新的函数也会被添加至调用栈中。当调用栈空间被占满时，就会引发“堆栈溢出”。因为只有一个调用栈，所以被称为单线程。

**callback queue**

回调队列，在 JavaScript 的编译阶段，将一些事件放置在执行队列中。

**EventLoop 事件循环**

将callback queue 中的事件放在 call stack 中执行