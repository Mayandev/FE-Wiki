# src 和 href 属性的区别

## 1. 定义

href 是 Hypertext Reference 的简写，表示超文本引用，指向网络资源所在位置。

```html
<link href="style.css" rel="stylesheet"/>
```

src 是 source 简写，指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置

```javascript
<script src ="js.js"></script>
```

## 2. 解析方式

1. 当浏览器遇到 href 会并行下载资源并且不会停止对当前文档的处理。(同时也是为什么建议使用 link 方式加载 CSS，而不是使用 @import 方式)
2. 当浏览器解析到 src ，会暂停其他资源的下载和处理，直到将该资源加载或执行完毕。(这也是 script 标签为什么放在底部而不是头部的原因)