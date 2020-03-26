# HTML5 的新特性


## 1. DOCTYPE 声明

`<!DOCTYPE>`只是一个说明，用来告诉浏览器当前的html页面是用什么版本的html写的。

html5 中的 `DOCTYPE` 声明只需要一段。

```html
<!DOCTYPE html>
```

而 html4 中的声明引用了DTD（document type define），因为 html4.01 是基于 SGML 的，而它引用的 DTD 指明了 html 的规则，从而浏览器能正确的渲染页面。而 html5 不是基于 SGML 所以不需要引用 DTD。

html4 中的声明：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">;
```

## 2. 语义化标签

html5 新增语义化标签。



| 标签                              | 标签                                     |
| --------------------------------- | ---------------------------------------- |
| &lt;article&gt;文档中定义文章内容       | &lt;aside&gt;                                  |
| &lt;details&gt;                         | &lt;dialog&gt;                                 |
| &lt;figcaption&gt;                      | &lt;figure&gt; img和figcaption组合放在figure里 |
| &lt;footer&gt; 一个文档可以有多个footer | &lt;header&gt;一个文档可以有多个header         |
| &lt;main&gt;                            | &lt;mark&gt;                                   |
| &lt;nav&gt; 导航                        | &lt;section&gt; 在文档中定义部分               |
| &lt;summary&gt;                         | &lt;time&gt;                                   |

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/11555850-a6fc197dc0d66ecd.gif)



**语义化标签的好处**

语义化标签能够方便开发者更好的理解文档，也使得计算机对于文档地理解更加地友好。比如人工智能的语义分析，搜索引擎的搜索分析，辅助视力阅读障碍者的屏幕阅读器之类的软件，在语义化标签的帮助下，能够更好的工作。

## 3. 新增 input 类型和属性

html 5 新增了一些 input 的类型和属性，对表单有一个增强。

| 类型type       | 属性attribute    |
| -------------- | ---------------- |
| color          | autocomplete     |
| date           | autofocus        |
| datetime       | form             |
| datetime-local | formaction       |
| email          | formenctype      |
| month          | formmethod       |
| number         | formnovalidate   |
| range          | formtarget       |
| search         | height and width |
| tel            | list             |
| search         | min and max      |
| time           | pattern(regexp)  |
| url            | placeholder      |
| week           | required         |
|                | step             |
|                | mutiple          |


## 4. 图形标签

新增 `<svg>` 和 `<canvas>` 标签。

 **SVG** 代表可缩放矢量图形，用于 Web 定义图形，本质上是 XML，通过在 XML 中描述路径进行绘制图形。目前页面中很多图片都使用 SVG 进行展示，不失真，并且体积小，加载速度快。

**canvas 和 svg 的区别：**

| Canvas                                                       | SVG                                                   |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| 与分辨率相关(可以理解为位图，图形放大会失真看到一个个像素点) | 与分辨率无关(可以理解为矢量，图形放大不会失真)        |
| 不支持事件处理程序                                           | 支持事件处理程序                                      |
| 文字呈现功能比较简单                                         | 最适合具有大型渲染区域地应用程序(如Google地图)        |
| 可以将生成的图像保存为.png或.jpg                             | 如果复杂地话渲染速度慢(其实任何使用DOM的东西都会很慢) |
| 适合图形密集性游戏                                           | 不适合游戏应用程序                                    |

## 5. 多媒体标签

新增 `<video>` 和 `<audio>` 标签，实现了对音频和视频的支持。

**思考🤔：如何使用 Canvas 实现 视频播放的功能（面试问过）**

> 思路：视频无非也是由一帧一帧的图像连续播放的，因此可以定时捕获视频每一帧的图像，并使用 Canvas 进行绘制，同时还可以添加文字实现弹幕的功能。

## 6. 新的 API

- HTML Geolocation 地理位置
- HTML Drag & Drop拖放
- HTML Local Storage 本地存储
- HTML Application Cache 应用程序缓存
- HTML Web Workers web工作者