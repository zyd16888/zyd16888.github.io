---
title: JavaScript笔记
copyright: false
abbrlink: 2b866d21
notshow: false
tags:
categories: 学习
description: 随便写写
sticky:
date: 2019-02-12 16:25:00
password:
image:
- "http://data.singlelovely.cn/CoverPicture/2b866d21.jpg"
photos:
---

## 变量

保留字

| abstract  |            delete |              goto    |               null	    |          throws|
|---|---|---|---|---|
as  |                    do   |                  if		 |           package	  |      transient |
boolean   |              double      |           implements   |            private  |             true |
break     |              else     |              import    |               protected     |        try |
byte      |              enum      |             in     |                  public   |             typeof |
case   |                 export    |             instanceof  |             return    |            use |
catch        |           extends         |       int       |               short    |             var |
char        |            false     |             interface  |              static     |           void |
class          |         final     |             is     |                  super    |             volatile |
continue       |         finally    |            long   |                  switch   |             while |
const       |            float      |            namespace |               synchronized  |        with |
debugger         |       for     |               native   |                this      |
default        |         function       |        new    |                  throw  |

使用 `const` 声明的变量称为“常量”。它们不能被修改。

### 总结

- `let` – 新时代的变量声明方式。Chrome（V8）中代码必须开启严格模式以使用 let。
- `var` – 旧时代的变量声明方式。
- `const` – 类似于let，但是变量的值无法被修改。

## 数据类型

七种基本的类型:

- `number` 用于任何类型的数字：整数或者浮点数。
- `string` 用于字符串。一个字符串可以包含一个或多个字符，所以没有单独的单字符类型。
- `boolean` 用于 `true` 和 `false`。
- `null` 用于未知的值 —— 只有一个 `null` 值的独立类型。
- `undefined` 用于未定义的值 —— 只有一个 `undefined` 值的独立类型。
- `object` 用于更复杂的数据结构。
- `symbol` 用于唯一的标识符。

typeof 运算符可以查看变量的类型。

- 两种形式：`typeof x` 或者 `typeof(x)`。
- 返回的类型的字符串，比如 `"string"`。
- `null` 返回 `"object"` —— 这是语言中的一个错误，实际上它并不是一个对象。

JavaScript 中的 `null` 不是一个“对不存在对象的引用”或者 “null 指针”。

仅仅是一个含义为“无”、“空”或“值未知”的特殊值。

## 类型转换

有三种常用的类型转换：转换为 string 类型、转换为 number 类型和转换为 boolean 类型。

ToString —— 输出内容时 ToString 发生转换，或通过 String(value) 进行显式转换。原始类型值的 string 类型转换通常是可预见的。

ToNumber – 进行算术操作时发生 ToNumber 转换，或通过 Number(value) 进行显式转换。

ToNumber 转换遵循以下规则：

|值 |	变成…|
|---|---|
|undefined |NaN|
|null | 0|
|true / false | 1 / 0|
|string | 字符串“按原样读取”，两端的空白被忽略。空字符串变成 0。出错变成 NaN。|

ToBoolean – 进行逻辑操作时发生 ToBoolean 转换。或通过 Boolean(value) 进行显式转换。

ToBoolean 遵循以下规则：

|值|变成…|
|---|---|
|0, null, undefined, NaN, ""	|false|
|其他值	|true|

- undefined 进行 ToNumber 时变成 NaN，而非 0。
- "0" 和只有空格的字符串(比如：" " )在进行 ToBoolean 变成 true。

## 值的比较

- 字符串比较时按位比较
- 若直接比较两个值，其结果是相等的。
- 若把两个值转为布尔值，它们可能得出完全相反的结果，即 true 和 false。

示例：

```JavaScript
let a = 0;
alert( Boolean(a) ); // false

let b = "0";
alert( Boolean(b) ); // true

alert(a == b); // true!

let c = ("2" > "12");//字符串比较
alert("c = " + c);//true
```

对于 JavaScript 而言这种现象蛮正常的，因为它会把待比较的值转为数字后再做比较（因此 "0" 变成了 0 ）。若只是将一个变量转为 Boolean，则会使用其他的类型转换规则。

普通的相等性检查 == 存在一个问题，它不能区分出 0 和 false：

>alert( 0 == false ); // true

也同样无法区分空字符串和 false：

> alert( '' == false ); // true

这是因为在比较不同类型的值时，处于相等判断符号 == 两侧的值会被转换为数字的原因。空字符串和 false 也是如此，转换后它们都等于 0。

### 严格相等操作符 === 在进行比较时不会做任何的类型转换。

`undefined` 和 `null` 在相等性检测 `==` 中不会进行任何的类型转换，它们有自己独立的比较规则，所以除了它们之间互等外不会等于任何其他的值。

### 小结

- 比较操作符始终返回逻辑值。
- 字符串间按“词典”顺序逐字符比较大小。
- 当待比较的值类型不同时，它们会被转为数字（不包括严格相等检测）进行比较。
- 在非严格相等 `==` 下，`null` 和 `undefined` 相等且各自不等于任何其他的值。
- 在使用 `>` 或 `<` 进行比较时，需要注意变量可能为 `null/undefined` 的情况。比较好的方法是单独检查变量是否等于 `null/undefined`。

## 交互

alert 弹出显示信息。

prompt 要求用户输入文本，确定返回文本，取消返回`null`。

confirm 显示信息等待确定或取消，确定返回`true`取消返回`false`。

## 三元运算符 ‘?’

```JavaScript
let result = condition ? value1 : value2
```

计算条件结果，如果结果为真，则返回 `value1`，否则返回 `value2`。

Java中同样适用

使用一系列问号 ? 运算符可以返回一个取决于多个条件的值。

例如：

```JavaScript
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

## "use strict" 新模式

2009 年 ECMAScript 5 (ES5) 的出现。ES5 规范增加了新的语言特性并且修改了一些已经存在的特性。为了保证旧的功能能够使用，大部分的修改是默认不生效的。需要一个特殊的指令 —— `"use strict"` 来明确地使用这些特性。

- 请确保 `"use strict"` 出现在脚本的最顶部，否则严格模式可能无法启用。
- 没有类似于 `"no use strict"` 这样的指令，这会返回原来的默认模式。

## 函数

- 对于有参函数，如未传入参数，则默认值为 `undefined`
- 如函数无返回值，则返回`undefined`
- 空`return` 和 `return undefined` 一样

### 函数命名

一种普遍的做法是用动词前缀来开始一个函数，这个前缀模糊地描述了这个动作。团队内部必须就前缀的含义达成一致。

- `"get…"` —— 返回值，
- `"calc…"` —— 计算
- `"create…"` —— 创建，
- `"check…"` —— 检查并返回 boolean 值，等。

### 练习

使用 '?' 或者 '||' 重写函数

```JavaScript
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm('Do you have your parents permission to access this page?');
  }
}
```

```JavaScript
function checkAge(age) {
  return (age > 18) ? true : confirm('Did parents allow you?');
}
```

```JavaScript
function checkAge(age) {
  return (age > 18) || confirm('Did parents allow you?');
}
```

写一个函数 pow(x,n)，在 n 中返回 x。或者换句话说，将 x 与自身相乘 n 次，然后返回结果。

```JavaScript
function pow(x,n){
    let result = x;
    while (n>1){
        result *= x;
        n--;
    }
    return result;
}
```

## 逻辑运算符

### 或运算寻找第一个真值

> result = value1 || value2 || value3;

- 从左到右依次计算操作数。
- 将每一个操作数转化为布尔值。如果结果是 true，就停止计算，返回这个操作数的初始值。
- 如果所有的操作数都被计算过（也就是，转换结果都是 false），返回最后一个操作数。

例1：获取变量列表或者表达式的第一个真值

```JavaScript
let currentUser = null;
let defaultUser = "John";

let name = currentUser || defaultUser || "unnamed";

alert( name ); // 选出了 “John” - 第一个真值
```

例2：短路取值

```js
let x;

!true! || (x = 1);

alert(x); // undefined，因为 (x = 1) 没有被执行
```

### 与操作寻找第一个假值

> result = value1 && value2 && value3;

- 从左到右依次计算操作数。
- 将每一个操作数转化为布尔值。如果结果是 false，就停止计算，返回这个操作数的初始值。
- 如果所有的操作数都被计算过（也就是，转换结果都是 true），返回最后一个操作数。

```js
alert( 1 && 2 && null && 3 ); // null

alert( 1 && 2 && 3 ); // 3，最后一个值
```

与运算 `&&` 的优先级比或运算 `||` 要高

```js
alert( 5 || 1 && 0 ); // 5
```

### 练习题

```js
alert( null || 2 && 3 || 4 ); //3

// 执行。
// -1 || 0 的结果为 -1，真值
if (-1 || 0) alert( 'first' );

// 不执行。
// -1 && 0 = 0，假值
if (-1 && 0) alert( 'second' );

// 执行
// && 运算的优先级比 || 高
// 所以 -1 && 1 先执行，给出如下运算链：
// null || -1 && 1  ->  null || 1  ->  1
if (null || -1 && 1) alert( 'third' );
```

