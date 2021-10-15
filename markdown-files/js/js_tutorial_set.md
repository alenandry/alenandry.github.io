## Js tutorial Set

# Set

**`Set`** 对象允许你存储任何类型的唯一值，无论是[原始值](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)或者是对象引用。

## [简述](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#简述)

`Set`对象是值的集合，你可以按照插入的顺序迭代它的元素。 Set中的元素只会**出现一次**，即 Set 中的元素是唯一的。

### [值的相等](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#值的相等)

因为 Set 中的值总是唯一的，所以需要判断两个值是否相等。在ECMAScript规范的早期版本中，这不是基于和===操作符中使用的算法相同的算法。具体来说，对于 Set s， +0 （+0 严格相等于-0）和-0是不同的值。然而，在 ECMAScript 2015规范中这点已被更改。有关详细信息，请参阅[浏览器兼容性](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#浏览器兼容性) 表中的“*Key equality for -0 and 0*”。

另外，`NaN`和`undefined`都可以被存储在Set 中， `NaN`之间被视为相同的值（NaN被认为是相同的，尽管 NaN !== NaN）。

## [Constructor](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#constructor)

- [`Set()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/Set)

  创建一个新的`Set`对象。

## [静态属性](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#静态属性)

- [`get Set[@@species\]`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/@@species)

  构造函数用来创建派生对象.

## [实例属性](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#properties)

- [`Set.prototype.size`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/size)

  返回 Set 对象中的值的个数

## [实例方法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#实例方法)

- [`Set.prototype.add(*value*)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/add)

  在`Set`对象尾部添加一个元素。返回该`Set`对象。

- [`Set.prototype.clear()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/clear)

  移除`Set`对象内的所有元素。

- [`Set.prototype.delete(*value*)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/delete)

  移除`Set`中与这个值相等的元素，返回`Set.prototype.has(value)`在这个操作前会返回的值（即如果该元素存在，返回`true`，否则返回`false`）。`Set.prototype.has(value)`在此后会返回`false`。

- [`Set.prototype.entries()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/entries)

  返回一个新的迭代器对象，该对象包含`Set`对象中的按插入顺序排列的所有元素的值的`[value, value]`数组。为了使这个方法和`Map`对象保持相似， 每个值的键和值相等。

- [`Set.prototype.forEach(*callbackFn*[, *thisArg*\])`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/forEach)

  按照插入顺序，为Set对象中的每一个值调用一次callBackFn。如果提供了`thisArg`参数，回调中的`this`会是这个参数。

- [`Set.prototype.has(*value*)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/has)

  返回一个布尔值，表示该值在`Set`中存在与否。

- [`Set.prototype.keys()` (en-US)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/values)

  与**`values()`**方法相同，返回一个新的迭代器对象，该对象包含`Set`对象中的按插入顺序排列的所有元素的值。

- [`Set.prototype.values()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/values)

  返回一个新的迭代器对象，该对象包含`Set`对象中的按插入顺序排列的所有元素的值。

- [`Set.prototype[@@iterator]()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set/@@iterator)

  返回一个新的迭代器对象，该对象包含`Set`对象中的按插入顺序排列的所有元素的值。

## [示例](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#示例)

### [使用`Set`对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#使用set对象)

```js
let mySet = new Set();

mySet.add(1); // Set [ 1 ]
mySet.add(5); // Set [ 1, 5 ]
mySet.add(5); // Set [ 1, 5 ]
mySet.add("some text"); // Set [ 1, 5, "some text" ]
let o = {a: 1, b: 2};
mySet.add(o);

mySet.add({a: 1, b: 2}); // o 指向的是不同的对象，所以没问题

mySet.has(1); // true
mySet.has(3); // false
mySet.has(5);              // true
mySet.has(Math.sqrt(25));  // true
mySet.has("Some Text".toLowerCase()); // true
mySet.has(o); // true

mySet.size; // 5

mySet.delete(5);  // true,  从set中移除5
mySet.has(5);     // false, 5已经被移除

mySet.size; // 4, 刚刚移除一个值

console.log(mySet);
// logs Set(4) [ 1, "some text", {…}, {…} ] in Firefox
// logs Set(4) { 1, "some text", {…}, {…} } in Chrome
```

Copy to Clipboard

### [迭代Set](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set#迭代set)

```js
// 迭代整个set
// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet) console.log(item);

// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet.keys()) console.log(item);

// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet.values()) console.log(item);

// 按顺序输出：1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
//(键与值相等)
for (let [key, value] of mySet.entries()) console.log(key);

// 使用 Array.from 转换Set为Array
var myArr = Array.from(mySet); // [1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}]

// 如果在HTML文档中工作，也可以：
mySet.add(document.body);
mySet.has(document.querySelector("body")); // true

// Set 和 Array互换
mySet2 = new Set([1, 2, 3, 4]);
mySet2.size;               // 4
[...mySet2];               // [1,2,3,4]

// 可以通过如下代码模拟求交集
let intersection = new Set([...set1].filter(x => set2.has(x)));

// 可以通过如下代码模拟求差集
let difference = new Set([...set1].filter(x => !set2.has(x)));

// 用forEach迭代
mySet.forEach(function(value) {
  console.log(value);
});

// 1
// 2
// 3
// 4
```
