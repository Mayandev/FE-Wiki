# 盒模型

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/box-model-1.gif)


![CSS box-model](https://www.runoob.com/images/box-model.gif)

所有HTML元素可以看作盒子，在CSS中，"box model"这一术语是用来设计和布局时使用。

CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。

- **Margin(外边距)** - 清除边框外的区域，外边距是透明的。
- **Border(边框)** - 围绕在内边距和内容外的边框。
- **Padding(内边距)** - 清除内容周围的区域，内边距是透明的。
- **Content(内容)** - 盒子的内容，显示文本和图像。

background-color 设置的是 padding 以及 content 的背景色。

IE 盒模型：width = content + border + padding

标准盒模型：width = content

```css
/*使用box-sizing选择使用那种盒模型*/
/*content-box 表示标准盒模型，IE 盒模型使用borde-box*/
box-sizing: content-box | border-box;
```