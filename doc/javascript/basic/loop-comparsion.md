# JavaScript 中几种循环的比较

## 性能上的比较

通过下面的代码分别在 Chrome 和 Node 环境进行测试：

```javascript
let arr = new Array(100000000).fill(0);

console.log('testing...');
let forTimeStart = new Date();
for (let i = 0; i < arr.length; i++) {
  // nothing to do
}
console.log('普通 for 循环:', new Date() - forTimeStart);

let forWithLengthTime = new Date();
for (let i = 0, n = arr.length; i < n; i++) {
  // nothing to do
}
console.log('缓存 length for循环:', new Date() - forWithLengthTime);

let forOfTime = new Date();
for(let num of arr) {
  // nothing to do
}
console.log('for of 循环：', new Date() - forOfTime);

let forInTime = new Date();
for(let num of arr) {
  // nothing to do
}
console.log('for in 循环：', new Date() - forInTime);

let forEachTime = new Date();
arr.forEach(() => {
  // nothing to do
})
console.log('foreach 循环', new Date() - forEachTime);

let mapTime = new Date();
arr.map(() => {
  // nothing to do
})
console.log('map 循环', new Date() - mapTime);

```

Node 环境的结果：
![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/fe-wiki-javascript-2.png)

Chrome 环境的结果：

![](https://mayandev.oss-cn-hangzhou.aliyuncs.com/blog/fe-wiki-javascript-1.png)

可以看到，相比之下，循环速度最快的是缓存 length 的 for 循环，然后普通 for 循环次之，for...in 和 for...of 循环的速度相差不大，最慢的是 map 循环。

## 如何选择

实际开发中应该选择哪种循环呢？

在不考虑性能的因素下，应该首先考虑代码的可读性。forEach 和 map 循环代码在实际中的可读性更强一些，所以我们更多的会使用这两种循环。

ES5 中还有很多其他的迭代函数，可根据不同需求进行选择。

> 如果你需要将数组按照某种规则映射为另一个数组，就应该用 map。
> 如果你需要进行简单的遍历，用 forEach 或者 for of。
> 如果你需要对迭代器进行遍历，用 for of.
> 如果你需要过滤出符合条件的项，用 filter.
> 如果你需要先按照规则映射为新数组，再根据条件过滤，那就用一个 map 加一个 filter。
>
> 作者：黑猫
> 链接：https://www.zhihu.com/question/263645361/answer/271393425
> 来源：知乎
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

