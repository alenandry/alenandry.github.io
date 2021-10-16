# precompile js 面试 （预编译）

```js
function fn(a, c) {
  console.log(a);//function a() {}
  var a = 123; // 123
  console.log(a);//123
  console.log(c);//function c() {}
  function a() {}
  if (false) { //不执行
    var d = 56;
  }
  console.log(d);//undefined
  console.log(b);//undefined
  var b = function () {};
  console.log(b);//function b() {}
  function c() {}
  console.log(c); //function c() {}
}
function fn(12, 23)
```

```js
// precompile
//注意变量作用域
a: undefined,123,function
c: undefined,function
d: undefined,
b: undefined,function
```
