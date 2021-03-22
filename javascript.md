# 题

## 题目

```javascript
function Foo() {
  var i=0;
  return function () {
    console.log(i++);
  }
}
var f1 = Foo();
var f2 = Foo();
f1();
f1();
f2();
```

## 答案

知识点：

1. 闭包
1. i++与++i

答案：0 1 0

详细：

1. f1，f2都是函数，内部分别存储单独i，每调用一次函数，会copy一份i存储在function scopes，所以各个i互不影响，详情查看下图,变量f1的scopes中存储一个Closure（Foo）
1. i++和++i，上面代码第一次调用f1，i++是0，i是1，如果改为++i，答案就是1 2 1

![image](./images/1-1.png)

# 题

## 题目

```javascript
var tt = 1;
function tt() {}
console.log(tt)
```

## 答案

知识点：变量提升

答案：1

详细：

1. 首先应该避免写这种代码
1. 如果出现，应该了解var和function都进行变量提升，但function比var先提升。
