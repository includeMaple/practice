# 题

## 题目

```javascript
let arr = []
let obj = {}
let str = ''
function test(val){
  if (Array.isArray(val)) {
    val.push('test')
  } else if (Object.prototype.toString(val) === '[object Object]') {
    val = {
      test: ''
    }
  }else {
    val = 'test'
  }
}
test(arr);
test(obj);
test(str);
console.log(arr)
console.log(obj)
console.log(str)
```

1. 请写出上面的输出结果
1. 为什么

## 参考

```javascript
['test'] // 变量被改变
{} // 变量未改变
out // 变量未改变
```

函数参数有两种传递方式：

1. 传值（基本类型）：将实参的值copy给函数，函数内部操作对象（形参）是实参的copy，不会影响实参
1. 传地址（引用类型）：将实参的地址产地给形参，这种情况一般有两种，①形参重新赋值一个地址，切断与形参之间的联系，如上obj②操作形参数据但不改变地址，如上arr


# 题

## 题目

请分别写出下面的结果：

```JavaScript
2+3+"4"
2+"3"+4
2+"3"-4
```

## 参考

1. 54
1. 234
1. 19

加法有两种含义①数值运算②字符串拼接，另外这里涉及到加法是从左往右运算的，所以

2+3+"4" = (2+3)+"4" = 5+"4"=54

2+"3"+4 = (2+"3")+4 = "23"+4 = 234

减法只有一个功能，做数值运算

# 题

## 题目

undefined==false，结果是true还是false

## 参考

if (xx) 是false的情况有6种

1. undefined
1. null
1. 0
1. NaN
1. ”“
1. false

这六种中

1. NaN与任何不相等，包括本身
1. undefined == null // true
1. 其余3种互相相等为true
1. 其余相等结果都是false

另外值得注意的是

```javascript
1==true; // true
12 == true; // false
```
<!-- 
只能尝试性解释，==，当两边类型不同时，会进行隐式类型转换

1. Number==Boolean: 尝试转换为Number
1. Number==String：尝试转换Number
1. undefined == Boolean: 似乎也是尝试转换为Number，因为Boolean(undefined)为false，Number(undefined) = NaN
1. 但似乎不总是转换成Number，因为undefined==null为true，而NaN不等于任何值，包括本身

目前暂时未找到权威合理的解释，我只能说：

1. 不要使用==
1. 使用强制类型转换，不要使用这种
1. 了解但不使用 -->

 <!-- 3.1==与===区别
==先转换类型再比较（值是否相等）
===先判断类型，如果不是同一类型直接为false。（值和类型是否都相等）
var a=[1,2];var b=[1,2];a==b //false 引用类型，引用的地址不一致
var a=[1,2];var b=a;a[2].3; //b为[1,2,3]
 
1.       强制类型转换和隐式类型转换
强制：parseInt parseFloat toString
隐式：if、逻辑运算、==、+拼接字符串
1.       显示转换：一般指使用Number、String和Boolean三个构造函数
Number(''/[]/null/false) // 0  Number(undefined/’123abc’) // NaN  Number('123') // 123
String(undefined) // "undefined"  String(null)// "null"
Boolean(-0/0/’’/null/undefined/NaN)//false  Boolean([]/数字/字符串)//true
隐式转换
1.       字符串连接符+：有字符串时，String()拼接;没有 字符串时，Number()计算 
1+’’true’’//’1 true’’  1+true//2  1+ undefined// NaN  1+null/’’/[] //1
2.       关系运算符>  <  >=  <=  = =  !=  = = =  != = =自增自减运算符++ / --
算术运算符+  -  *  /  %：
有一边是字符串时，Number()比较；两边都是字符串时，unicode编码比较
‘’2’’>10 //false  ‘’2’’>’’10’’//true  ‘’abc’’>’’aac’’//true -->

# 题

## 题目

以下代码分别输出什么

```javascript
var b = 1;
(function (){
  b = 2;
  console.log(b)
})()
console.log(b)

var d = 10;
function testd() {
  d = 20
  console.log(d)
}
testd()
console.log(d)

var c = 100;
function test() {
  c = 200
  var c = 300
  console.log(c)
}
test()
console.log(c)
```

## 参考

知识点：

1. 作用域与作用域链（var有函数作用域）

了解：

1. 第一段和第二段代码表示，当本作用域没有定义时，变量会沿着作用域链向上查找（上面代码），直到找到全局为止（如下代码）
1. 第三段代码，如果本作用域重新定义某个变量，则这属于独立作用域（下面代码会再展开）

如下会沿着作用域链一直往上查找（不论多少层嵌套），直到找到为止，所以输出的是0

```javascript
var a = 0;
(function (){
  (function (){
    (function(){
      console.log(a)
    })()
  })()
})()
```

下面将输出undefined 300 100，因为函数test中对c做了重定义，所以只要在函数内定义前的c和定义后的c在同一个作用域。

```javascript
var c = 100;
function test() {
  console.log(c)
  var c = 300
  console.log(c)
}
test()
console.log(c)
```

# 题

## 题目一

以下输出结果是：

```javascript
function test(){
  var arr = [];
  for(var i = 0;i < 10 ;i++){
    arr[i] = function(){
      console.log(i);
    }
  }
  return arr;
}
var myArr = test();
myArr[0]();
myArr[1]();
myArr[2]();
myArr[3]();
```

## 题目二

如何输出0 1 2 3

## 参考

1. 这里arr的每个元素是一个函数，要了解非立即执行的情况很多，这是其中一种（其他还有使用setTimeout、dom操作等），i每次要到执行的时候才会去寻找，而此时i已经变成了其他值
2. 要变成正常输出的方法很多，①let利用其块级作用域(把var改为let，这里不再举例代码)②使用立即执行函数（匿名函数，立即执行），利用其函数作用域，代码如下

```javascript
function test(){
  var arr = [];
  for(var i = 0;i < 10 ;i++){
    (function (j) {
      arr[j] = function(){
        console.log(j);
      }
    })(i)
  }
  return arr;
}
var myArr = test();
myArr[0]();
myArr[1]();
myArr[2]();
myArr[3]();
```

# 题

## 题目

```javascript
for(var i=0; i<=3; i++){
  setTimeout(function(){
    console.log(i)
  }, 0)
}
```

## 参考

知识点：var没有块级作用域

输出：4 4 4 4

注意这里有两点：

1. 使用var定义i
1. setTimeout并非理解输出，这模拟了诸如dom单击操作，如果采用dom操作上面答案相同

### 异步执行再取i

var定义的i，会在执行时再去取，而这里用了setTimeout，所以去取i的时候，i的值已经变成了4，如下没有使用setTimeout，直接使用会正常输出0 1 2 3

```javascript
for(let i=0; i<=3; i++){
  console.log(i)
}
```

### 与let相比var没有块级作用域

如果把var改为let，将输出0 1 2 3，如下

```javascript
for(let i=0; i<=3; i++){
  setTimeout(function(){
    console.log(i)
  }, 0)
}
```

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

## 参考

知识点：

1. 闭包
1. i、i++与++i

输出结果：0 1 0

### 闭包

f1，f2都是函数，内部分别存储单独i，每调用一次函数，会copy一份i存储在function scopes，所以每个闭包的各个i互不影响，详情查看下图,变量f1的scopes中存储一个Closure（Foo）

![image](./images/1-1.png)

### i、i++与++i

i++和++i，上面代码第一次调用f1，i++是0，i是1，如果改为++i，答案就是1 2 1

```javascript
let i=0;
console.log(i)
console.log(++i)
console.log(i)
// 0 1 1
```

```javascript
let i=0;
console.log(i)
console.log(i++)
console.log(i)
// 0 0 1
```

由上可知，i、i++与++i是不同的，不过另一方面下面的i++ ++i似乎没什么不同

```javascript
for (let i=0;i<3;i++){
  console.log(i) // 0 1 2
}
for (let i=0;i<3;++i){
  console.log(i) // 0 1 2
}
```

差异在于是否直接使用，for循环中，我们只是用i++(或++i）做了增1操作，并没有直接在增加时使用，而案例中用console.log()直接使用了他们。

i++和++i到底有什么区别，可以参考下方C++

1. 理论上++i更快，实际与编译器优化有关，通常几乎无差别。
1. 简单来说，i++返回的是i的值，++i返回i+1的值

```c++
//i++：                                    
int operator++(int)                                  
{
  int temp = *this;                                     
  ++*this;                                             
  return temp;                                    
}
// ++i
int& operator++()
{
  *this += 1;
  return *this;
}
```

# 题

## 题目

```javascript
var tt = 1;
function tt() {}
console.log(tt)
```

## 参考

知识点：变量提升与预解析

输出：1

详细：

1. 首先应该避免这种重名
1. 如果出现，应该了解var和function都进行变量提升，预解析是有优先级的，在var和function中，function先解析，且两者解析不同，var解析成undefined，function会指向真实function。

思维串联：函数声明和函数表达式，函数声明我们可以在定前调用，函数表达式我们只能在定义后调用，与上面是同一个思路

```javascript
var test = function () {return '函数表达式'}
function test(){ return '函数声明'}
console.log(test) // 函数表达式
```

通常我们会简单的说，函数声明有变量提升，函数表达式没有，但通过上面的分析可以了解到这种说法是不严谨的，var的函数表达式也有变量提升，只是提升成了undefined，我们仍然无法当正常函数调用。
