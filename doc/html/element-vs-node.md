# Element 和 Node 的区别

在 js 中会经常使用 document.getElementById 去获取 dom 元素，也会使用 childNode 来获取子节点。

二者的区别是什么呢？

先来看一个简单的例子：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Node vs Element</title>
</head>
<body>
  <h1>Node vs Element</h1>
  <div>node vs element</div>
</body>
</html>
```

下面分别打印 `<body>` 标签下的 Element 和 ChildNodes，可以看到，getElement 返回的是 HTMLCollection 对象，而 childNodes 返回的是 NodeList 对象。

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/fe-wiki-html-3.png)



那么问题来了：

- HTMLCollection，NodeList 是啥
- NodeList 数组里的 text 又是啥

## Node 和 Element定义

先来看看 MDN 上 对 Node 的定义：

> A Node is an interface from which a number of DOM types inherit, and allows these various types to be treated (or tested) similarly.
>
> 

> The following interfaces all inherit from Node its methods and properties: Document, Element, CharacterData (which Text, Comment, and CDATASection inherit), ProcessingInstruction, DocumentFragment, DocumentType, Notation, Entity, EntityReference.

上面两段话到意思就是 `Node`是一个基类，DOM中的`Element`，`Text`和`Comment`都继承于它。

其实，Node 就是表示的是 DOM 树的结构，在 html 中，节点与节点中间是可以插入文本的，这个插入文本的间隙就是 Text。

## HTMLCollection 和 NodeList

`NodeList`是`Node`的集合，`ElementCollection`是`Element`的集合。

但需要特别注意的是：

***NodeList和ElementCollcetion都不是真正的数组\***

如果`document.getElementsByTagName('a') instanceof Array`，结果是`false`。

