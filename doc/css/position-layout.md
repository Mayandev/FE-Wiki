# position 布局

## 1、static

默认是static，使用正常的布局行为，即元素在文档常规流中当前的布局位置。`此时的top、left等属性设置无效。`

## 2、relative

relative 是相对元素正常文档位置的情况下进行布局，使用top、left等属性使其相对原来的位置进行偏移。

## 3、absolute

绝对定位，脱离文档流布局。通过指定元素最近的非 static 定位元素的偏移，来确定元素定位置。可以设置外边距（margin），且不会与其他边距合并。

## 4、fixed

不为元素预留空间，而是指定元素相对于 viewport 的位置来制定元素的位置。

## 5、sticky

相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位

## 6、inherit

规定应该从父元素继承 position 属性的值。