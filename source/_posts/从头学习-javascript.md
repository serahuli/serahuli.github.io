---
title: 从头学习 javascript
top: false
cover: false
toc: true
mathjax: true
date: 2020-8-12 13:50:01
password:
summary:
tags: '前端'
categories: '前端' 
---

## Javascript 介绍

> **JavaScript** 又叫 **JS**， 是一种具有[函数优先](https://developer.mozilla.org/zh-CN/docs/Glossary/First-class_Function)的轻量级，解释型或即时编译型的编程语言。
>
> JavaScript 是一种[基于原型编程](https://developer.mozilla.org/zh-CN/docs/Glossary/Prototype-based_programming)、多范式的动态脚本语言，并且支持面向对象、命令式和声明式（如函数式编程）风格。
>
> JavaScript 的标准是 [ECMAScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Language_Resources) .
>
> JavaScript 内置了一些对象的标准库，比如数组（`Array`），日期（`Date`），数学（`Math`）和一套核心语句，包括运算符、流程控制符以及声明方式等。

## 基本语法

### hello

```javascript
function sayHi (userName) {
  console.log(`hi, ${userName}`)
}

sayHi('sera') //hi, sera
```

---

### 语法和数据类型

#### **基本知识**

> - JavaScript 是**区分大小写**的，并使用 **Unicode** 字符集。
> - 在 JavaScript 中，指令被称为语句 （[Statement](https://developer.mozilla.org/zh-CN/docs/Glossary/Statement)），并用分号（;）进行分隔。如果一条语句独占一行的话，那么分号是可以省略的。（不建议）
> - 空白字符指的是空格、制表符和换行符等。

#### 注释

```javascript
// 单行注释

/* 这是一个更长的,
   多行注释
*/

/* 然而, 你不能, /* 嵌套注释 */ 语法错误 */
```

#### 声明

`var`: 声明一个变量，可选初始化一个值。

`let`: 声明一个块作用域的局部变量，可选初始化一个值。

`const`: 声明一个块作用域的只读常量。

**变量（标识符）**： 使用变量来作为值的符号名， 一个 JavaScript 标识符**必须**以字母、下划线（_）或者美元符号（$）开头；后续的字符也可以是数字（0-9）。

**声明变量**:

> 1. `var`: var x = 42, 用来声明局部变量和全局变量
> 2. 直接赋值： x = 42， 产生一个全局变量，严格模式报错
> 3. `let`: let y = 13， 声明块作用域的局部变量

**变量求值**:

> 1. 用 `var` 或 `let` 语句声明的变量，如果没有赋初始值，则其值为 `undefined` 
>
> 2. 如果访问一个未声明的变量会导致抛出一个引用错误（`ReferenceError`）异常
>
> 3. 可以使用 `undefined` 来判断一个变量是否已赋值
>
> 4. 数值类型环境中 `undefined` 值会被转换为 `NaN`
>
>    ```javascript
>    var a;
>    a + 2;    // NaN
>    ```
>
> 5. 对一个 `null` 变量求值时，空值 `null` 在数值类型环境中会被当作0来对待，而布尔类型环境中会被当作 `false`。
>
>    ```javascript
>    var n = null;
>    console.log(n * 32); // 0
>    ```

**变量的作用域**

> 在函数之外声明的变量，叫做*全局*变量，因为它可被当前文档中的任何其他代码所访问。在函数内部声明的变量，叫做*局部*变量，因为它只能在当前函数的内部访问。
>
> - ECMAScript 6 之前的 JavaScript 没有 [语句块](https://developer.mozilla.org/zh-CN/docs/JavaScript/Guide/Statements#Block_Statement) 作用域；相反，语句块中声明的变量将成为语句块所在函数（或全局作用域）的局部变量。

**变量提升**

> JavaScript 变量是被“提升”或移到了函数或语句的最前面。但是，提升后的变量将返回 undefined 值。因此在使用或引用某个变量之后进行声明和初始化操作，这个被提升的变量仍将返回 undefined 值。

```javascript
/**
 * 例子1
 */
console.log(x === undefined); // true
var x = 3;


/**
 * 例子2
 */
// will return a value of undefined
var myvar = "my value";

(function() {
  console.log(myvar); // undefined
  var myvar = "local value";
})();
```

由于存在变量提升，一个函数中所有的`var`语句应尽可能地放在接近函数顶部的地方。这个习惯将大大提升代码的清晰度。

>  在ES6+中，在变量声明之前引用这个变量，将抛出引用错误（ReferenceError）。这个变量将从代码块一开始的时候就处在一个“暂时性死区”，直到这个变量被声明为止。
>
> ```js
> console.log(x); // ReferenceError
> let x = 3;
> ```

对于函数来说，只有函数声明会被提升到顶部，而函数表达式不会被提升。

```javascript
/* 函数声明 */

foo(); // "bar"

function foo() {
  console.log("bar");
}


/* 函数表达式 */

baz(); // 类型错误：baz 不是一个函数

var baz = function() {
  console.log("bar2");
};
```

**全局变量**

> 全局变量是*全局对象*的属性。在网页中，（缺省的）全局对象是 `window`。可以用形如 `window.`*`variable`* 的语法来设置和访问全局变量

**常量(Constants)**

> 用关键字 `const` 创建一个只读的常量 。`const PI = 3.14;`
>
> 常量不可以通过重新赋值改变其值，也不可以在代码运行时重新声明。它必须被初始化为某个值。
>
> 在同一作用域中，不能使用与变量名或函数名相同的名字来命名常量。

```js
// 这会造成错误
function f() {};
const f = 5;

// 这也会造成错误
function f() {
  const g = 5;
  var g;

  //语句
}
```

- 对象属性被赋值为常量是不受保护的,数组的被定义为常量也是不受保护的

```js
const MY_OBJECT = {"key": "value"};
MY_OBJECT.key = "otherValue";

const MY_ARRAY = ['HTML','CSS'];
MY_ARRAY.push('JAVASCRIPT');
console.log(MY_ARRAY); //logs ['HTML','CSS','JAVASCRIPT'];
```

---

### 数据结构和类型

最新的 ECMAScript 标准定义了8种数据类型

- 七种基本数据类型:
  - 布尔值（Boolean），有2个值分别是：`true` 和 `false`.
  - null ， 一个表明 null 值的特殊关键字。 JavaScript 是大小写敏感的，因此 `null` 与 `Null`、`NULL`或变体完全不同。
  - undefined ，和 null 一样是一个特殊的关键字，undefined 表示变量未赋值时的属性。
  - 数字（Number），整数或浮点数，例如： `42` 或者 `3.14159`。
  - 任意精度的整数 (BigInt) ，可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。
  - 字符串（String），字符串是一串表示文本值的字符序列，例如："Howdy" 。
  - 代表（Symbol） ( 在 ECMAScript 6 中新添加的类型).。一种实例是唯一且不可改变的数据类型。
- 以及对象（Object）。

**数据类型的转换**

> JavaScript是一种动态类型语言(dynamically typed language)。这意味着你在声明变量时可以不必指定数据类型，而数据类型会在代码执行时会根据需要自动转换。

- 在包含的数字和字符串的表达式中使用加法运算符（+），JavaScript 会把数字转换成字符串。
- 在涉及其它运算符（如下面的减号'-'）时，JavaScript语言不会把数字变为字符串。

```javascript
"37" - 7 // 30
"37" + 7 // "377"
```

**字符串转换为数字**

1. **`parseInt()`**只能返回整数，会丢失小数部分。调用 parseInt 时最好总是带上进制(radix) 参数，这个参数用于指定使用哪一种进制。
2. **`parseFloat`**
3. 一元**加法运算符**

```javascript
"1.1" + "1.1" = "1.11.1"
(+"1.1") + (+"1.1") = 2.2   
```

---

### 字面量

字面量是由语法表达式定义的常量

**数组字面量 (Array literals)**

数组字面值是一个封闭在方括号对([])中的包含有零个或多个表达式的列表，其中每个表达式代表数组的一个元素。当你使用数组字面值创建一个数组时，该数组将会以指定的值作为其元素进行初始化，而其长度被设定为元素的个数。

```js
var coffees = ["French Roast", "Colombian", "Kona"];

var a=[3];

var fish = ["Lion", , "Angel"]; // Loin, undefined, Angel

console.log(a.length); // 1

console.log(a[0]); // 3
```

数组字面值同时也是数组对象, 你在同一行中连写两个逗号（,），数组中就会产生一个没有被指定的元素，其初始值是`undefined`。

**显式地将缺失的元素声明为`undefined`，将大大提高你的代码的清晰度和可维护性**。

**布尔字面量 (Boolean literals)**

- true
- false

**整数 (Integers)**

- 十进制整数字面量由一串数字序列组成，且没有前缀0。
- 八进制的整数以 0（或0O、0o）开头，只能包括数字0-7。严格模式下，八进制整数字面量必须以0o或0O开头，而不能以0开头。
- 十六进制整数以0x（或0X）开头，可以包含数字（0-9）和字母 a~f 或 A~F。
- 二进制整数以0b（或0B）开头，只能包含数字0和1。

**浮点数字面量 (Floating-point literals)**

- 一个十进制整数，可以带正负号（即前缀“+”或“ - ”），
- 小数点（“.”），
- 小数部分（由一串十进制数表示），
- 指数部分。

> 指数部分以“e”或“E”开头，后面跟着一个整数，可以有正负号（即前缀“+”或“-”）。浮点数字面量至少有一位数字，而且必须带小数点或者“e”（大写“E”也可）。

```js
3.14      
-.2345789 // -0.23456789
-3.12e+12  // -3.12*1012
.1e-23    // 0.1*10-23=10-24=1e-24
```

**对象字面量 (Object literals)**

对象字面值是封闭在花括号对({})中的一个对象的零个或多个"属性名-值"对的（元素）列表。你不能在一条语句的开头就使用对象字面值，这将导致错误或产生超出预料的行为， 因为此时左花括号（{）会被认为是一个语句块的起始符号。

> 对象属性名字可以是任意字符串，包括空串。如果对象属性名字不是合法的javascript标识符，它必须用""包裹。属性的名字不合法，那么便不能用.访问属性值，而是通过类数组标记("[]")访问和赋值。

**增强的对象字面量 (Enhanced Object literals)**

对象字面值扩展支持在创建时设置原型，简写了 foo: foo 形式的属性赋值，方法定义，支持父方法调用，以及使用表达式动态计算属性名。

```javascript
var foo = {a: "alpha", 2: "two"};
console.log(foo.a);    // alpha
console.log(foo[2]);   // two
console.log(foo.2);  // SyntaxError: missing ) after argument list
console.log(foo[a]); // ReferenceError: a is not defined
console.log(foo["a"]); // alpha
console.log(foo["2"]); // two
```

**RegExp 字面值**

```javascript
var re = /ab+c/
```

**字符串字面量 (String literals)**

```javascript
"foo"
'bar'
"1234"
"one line \n another line"
"John's cat"
`Hello ${name}, how are you ${time}?`   // ES6
```

> 可以在字符串字面值上使用字符串对象的所有方法——JavaScript会自动将字符串字面值转换为一个临时字符串对象，调用该方法，然后废弃掉那个临时的字符串对象。

**在字符串中使用的特殊字符**

```js
"one line \n another line"
```

| 字符        | 意思                                                         |
| :---------- | :----------------------------------------------------------- |
| \0          | Null字节                                                     |
| \b          | 退格符                                                       |
| \f          | 换页符                                                       |
| \n          | 换行符                                                       |
| \r          | 回车符                                                       |
| \t          | Tab (制表符)                                                 |
| \v          | 垂直制表符                                                   |
| \'          | 单引号                                                       |
| \"          | 双引号                                                       |
| \\          | 反斜杠字符（\）                                              |
| \*XXX*      | 由从0到377最多三位八进制数*XXX*表示的 Latin-1 字符。例如，\251是版权符号的八进制序列。 |
| \x*XX*      | 由从00和FF的两位十六进制数字XX表示的Latin-1字符。例如，\ xA9是版权符号的十六进制序列。 |
| *\uXXXX*    | 由四位十六进制数字XXXX表示的Unicode字符。例如，\ u00A9是版权符号的Unicode序列。见[Unicode escape sequences](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#String_literals) (Unicode 转义字符). |
| \u*{XXXXX}* | Unicode代码点 (code point) 转义字符。例如，\u{2F804} 相当于Unicode转义字符 \uD87E\uDC04的简写。 |

严格模式下，不能使用八进制转义字符。

---

## 流程控制与错误处理

- 在JavaScript中，任何表达式(expression)都可以看作一条语句(statement)

### 语句块

```js
{
   statement_1;   
   statement_2;
   .
   .
   .
   statement_n;
}
```

语句块通常用于流程控制，如`if`，`for`，`while`等等。

> 在ECMAScript 6标准之前，Javascript没有块作用域。在一个块中引入的变量的作用域是`包含函数或脚本`，并且设置它们的效果会延续到块之外。
>
> ```js
> var x = 1;
> {
>   var x = 2;
> }
> alert(x); // 输出的结果为 2
> ```

### 条件判断语句

- `if…else…`
- `if…else if… else…`
- `switch`

**if…else…**

```js
if (condition) {
  statement_1;
}else {
  statement_2;
} 

if (condition_1) {
  statement_1;
}else if (condition_2) {
  statement_2;
}else if (condition_n_1) {
  statement_n;
}else {
  statement_last;
}
```

判断是错误（false）的值

- false
- undefined
- null
- 0
- NaN
- 0

> 当传递给条件语句所有其他的值，包括所有对象会被计算为真

**重点注意，Boolean对象，Boolean对象的假在判断语句中也是真 **

```js
var b = new Boolean(false);
if (b) //结果视为真
if (b == true) // 结果视为假
```

**switch**

```javascript
switch (expression) {
   case label_1:
      statements_1
      [break;]
   case label_2:
      statements_2
      [break;]
   ...
   default:
      statements_def
      [break;]
}
```

- 计算`expression`的 值，等于 case跟的值，执行该case下的语句，该case存在`break;`则执行完之后结束该程序。
- 如果，没有匹配到case，执行`default`后面的语句

---

### 异常处理语句

用 `throw` 语句抛出一个异常并且用 `try...catch` 语句捕获处理它

**`throw`**可以抛出任意表达式而不是特定一种类型的表达式

```js
throw "Error2";   // String type
throw 42;         // Number type
throw true;       // Boolean type
throw {toString: function() { return "I'm an object!"; } };
```

例子

```js
/ Create an object type UserException
function UserException (message){
  this.message=message;
  this.name="UserException";
}

// Make the exception convert to a pretty string when used as
// a string (e.g. by the error console)
UserException.prototype.toString = function (){
  return this.name + ': "' + this.message + '"';
}

// Create an instance of the object type and throw it
throw new UserException("Value too high");
```

**`try...catch`**

> `try...catch` 语句标记一块待尝试的语句，并规定一个以上的响应应该有一个异常被抛出。如果我们抛出一个异常，`try...catch`语句就捕获它。

先执行 try中的语句，如果try中语句抛出异常，则转到catch，否则执行 catch。`finally`，跟在 `try...catch` 之后，无论是否抛出异常，都会执行 `finally`语句.

catch指定了一个标识符，来存放抛出语句指定的值

```js
try {}
catch (e) {
  console.log(e)
}
```

### 使用`Error`对象

```js
function doSomethingErrorProne () {
  if (ourCodeMakesAMistake()) {
    throw (new Error('The message'));
  } else {
    doSomethingToGetAJavascriptError();
  }
}
try {
  doSomethingErrorProne();
}
catch (e) {
  console.log(e.name); // logs 'Error'
  console.log(e.message); // logs 'The message' or a JavaScript error message)
}
```

### Promises

允许你对延时和异步操作流进行控制。

`Promise` 对象有以下几种状态：

- *pending：*初始的状态，即正在执行，不处于 fulfilled 或 rejected 状态。
- *fulfilled：*成功的完成了操作。
- *rejected：*失败，没有完成操作。
- *settled：*Promise 处于 fulfilled 或 rejected 二者中的任意一个状态, 不会是 pending。

# 循环与迭代

###  for

一个 [`for`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/for) 循环会一直重复执行，直到指定的循环条件为 false。

```js
for ([initialExpression]; [condition]; [incrementExpression])
  statement
```

```js
for(let i = 0; i < 10; i++) {
  console.log(i) // 0 1 2 3 4 5 6 7 8 9
}
```

### do...while

[`do...while`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/do...while) 语句一直重复直到指定的条件求值得到假值（false）,至少执行一次  statement

```js
do
  statement
while (condition);
```

```js
var i = 0;
do {
  i += 1;
  console.log(i); // 1 2 3 4 5 
} while (i < 5);
```

### while

一个 [`while`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/while) 语句只要指定的条件求值为真（true）就会一直执行它的语句块，可能一次也不执行

```js
while (condition)
  statement
```

```js 
var n = 0;
var x = 0;
while (n < 3) {
  n++;
  x += n;
}
console.log(x) // 6
```

```js
// 无限循环
while (true) {
  console.log("Hello, world");
}
```

### label

一个 [`label`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/label) 提供了一个让你在程序中其他位置引用它的标识符。

> `label` 的值可以是任何的非保留字的 JavaScript 标识符， `statement` 可以是任意你想要标识的语句（块）。

```js
var num = 0;
for (var i = 0 ; i < 10 ; i++) {   // i 循环
  for (var j = 0 ; j < 10 ; j++) { // j 循环
    if( i == 5 && j == 5 ) {
       break; // i = 5，j = 5 时，会跳出 j 循环
    } // 但 i 循环会继续执行，等于跳出之后又继续执行更多次 j 循环
  num++;
  }
}

alert(num); // 输出 95
```

// label

```js
var num = 0;
outPoint:
for (var i = 0 ; i < 10 ; i++){
  for (var j = 0 ; j < 10 ; j++){
    if( i == 5 && j == 5 ){
      break outPoint; // 在 i = 5，j = 5 时，跳出所有循环，
                      // 返回到整个 outPoint 下方，继续执行
    }
    num++;
  }
}

alert(num); // 输出 55
```

```js
var num = 0;
outPoint:
for(var i = 0; i < 10; i++) {
  for(var j = 0; j < 10; j++) {
    if(i == 5 && j == 5) {
      continue outPoint;
    }
    num++;
  }
}
alert(num);  // 95
```

### break

使用 [`break`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/break) 语句来终止循环，`switch`， 或者是链接到 label 语句

- 当你使用不带 label 的 `break` 时， 它会立即终止当前所在的 `while`，`do-while`，`for`，或者 `switch` 并把控制权交回这些结构后面的语句。
- 当你使用带 label 的 `break` 时，它会终止指定的带标记（label）的语句。

### continue

[`continue`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/continue) 语句可以用来继续执行（跳过代码块的剩余部分并进入下一循环）一个 `while`、`do-while`、`for`，或者 `label` 语句。

- 当你使用不带 label 的 `continue` 时， 它终止当前 `while`，`do-while`，或者 for 语句到结尾的这次的循环并且继续执行下一次循环。
- 当你使用带 label 的 `continue` 时， 它会应用被 label 标识的循环语句。

### for...in

[`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/for...in) 语句循环一个指定的变量来循环一个对象所有可枚举的属性。JavaScript 会为每一个不同的属性执行指定的语句。

### for...of

[`for...of`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/statements/for...of) 语句在[可迭代对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/iterable)（包括[`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)、[`Map`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Map)、[`Set`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)、[`arguments`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/functions/arguments) 等等）上创建了一个循环，对值的每一个独特属性调用一次迭代。

```js
let arr = [3, 5, 7];
arr.foo = "hello";

for (let i in arr) {
   console.log(i); // 输出 "0", "1", "2", "foo"
}

for (let i of arr) {
   console.log(i); // 输出 "3", "5", "7"
}
```

```js
let obj = {
    a: 12,
    b: 13
}
for (let i in obj) {
   console.log(i); // 输出 "a", "b"
}
for (let i of obj) {
   console.log(i); // Uncaught TypeError: obj is not iterable
}
```

## 函数

函数是 JavaScript 中的基本组件之一

### 定义函数

**函数声明**

> 一个**函数定义**（也称为**函数声明**，或**函数语句**）由一系列的[`function`](https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Statements/function)关键字组成，依次为：
>
> - 函数的名称。
> - 函数参数列表，包围在括号中并由逗号分隔。
> - 定义函数的 JavaScript 语句，用大括号`{}`括起来。

```js
function square(number) {
  return number * number;  // 函数体
}
```

> 关于参数：
>
> 原始参数（比如一个具体的数字）被作为**值**传递给函数；值被传递给函数，如果被调用函数改变了这个参数的值，这样的改变不会影响到全局或调用函数。
>
> 如果你传递一个对象（即一个非原始值，例如[`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Array)或用户自定义的对象）作为参数，而函数改变了这个对象的属性，这样的改变对函数外部是可见的

**函数表达式**

函数也可以由函数表达式创建。这样的函数可以是**匿名**的；

```js
const square = function(number) { return number * number; };
```

函数表达式也可以提供函数名，并且可以用于在函数内部代指其本身，或者在调试器堆栈跟踪中识别该函数

```js
const factorial = function fac(n) {return n<2 ? 1 : n*fac(n-1)};
```

当将函数作为参数传递给另一个函数时，函数表达式很方便。

```js
function map(f, a) {
  let result = []; // 创建一个数组
  let i; // 声明一个值，用来循环
  for (i = 0; i != a.length; i++) 
    result[i] = f(a[i]);
  return result;
}
const f = function(x) {
   return x * x * x; 
}
let numbers = [0, 1, 2, 5,10];
let cube = map(f,numbers);
console.log(cube);
```

根据条件来定义一个函数

```js
var myFunc;
if (num == 0){
  myFunc = function(theObject) {
    theObject.make = "Toyota"
  }
}
```

当一个函数是一个对象的属性时，称之为**方法**。

### 调用函数

定义一个函数并不会自动的执行它。定义了函数仅仅是赋予函数以名称并明确函数被调用时该做些什么。**调用**函数才会以给定的参数真正执行这些动作。

```js
square(5);  // 方法名字（[参数]）
```

函数域是指函数声明时的所在的地方，或者函数在顶层被声明时指整个程序。

函数提升仅适用于函数声明，而不适用于函数表达式。

函数可以被递归，就是说函数可以调用其本身。

### 函数作用域

> 在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数的域的内部有定义。相对应的，一个函数可以访问定义在其范围内的任何变量和函数。换言之，定义在全局域中的函数可以访问所有定义在全局域中的变量。在另一个函数中定义的函数也可以访问在其父函数中定义的所有变量和父函数有权访问的任何其他变量。

### 作用域和函数堆栈

**递归**

> 一个函数可以指向并调用自身。
>
> 1. 函数名
> 2. `arguments.callee`
> 3. 作用域下的一个指向该函数的变量名

```js
var foo = function bar() {
   bar()
	 arguments.callee() //ES5禁止在严格模式下使用此属性
	 foo()
};
```

```js
function foo(i) {
  if (i < 0)
    return;
  console.log('begin:' + i);
  foo(i - 1);
  console.log('end:' + i);
}
foo(3);

// begin:3
// begin:2
// begin:1
// begin:0
// end:0
// end:1
// end:2
// end:3
```

**嵌套函数和闭包**

> 可以在一个函数里面嵌套另外一个函数。嵌套（内部）函数对其容器（外部）函数是私有的。它自身也形成了一个闭包。一个闭包是一个可以自己拥有独立的环境与变量的表达式（通常是函数）。内部函数包含外部函数的作用域,，也就是通常说的继承

- 内部函数只可以在外部函数中访问。
- 内部函数形成了一个闭包：它可以访问外部函数的参数和变量，但是外部函数却不能使用它的参数和变量。

> 函数可以被多层嵌套.因此，闭包可以包含多个作用域；他们递归式的包含了所有包含它的函数作用域。这个称之为作用*域链*。

**命名冲突**

> 当同一个闭包作用域下两个参数或者变量同名时，就会产生命名冲突。更近的作用域有更高的优先权，所以最近的优先级最高，最远的优先级最低。这就是作用域链。链的第一个元素就是最里面的作用域，最后一个元素便是最外层的作用域。

### 闭包

> 闭包是 JavaScript 中最强大的特性之一。JavaScript 允许函数嵌套，并且内部函数可以访问定义在外部函数中的所有变量和函数，以及外部函数能访问的所有变量和函数。

此外，由于内部函数可以访问外部函数的作用域，因此当内部函数生存周期大于外部函数时，外部函数中定义的变量和函数的生存周期将比内部函数执行时间长。当内部函数以某一种方式被任何一个外部函数作用域访问时，一个闭包就产生了。

```js
var createPet = function(name) {
  var sex;
  
  return {
    setName: function(newName) {
      name = newName;
    },
    
    getName: function() {
      return name;
    },
    
    getSex: function() {
      return sex;
    },
    
    setSex: function(newSex) {
      if(typeof newSex == "string" 
        && (newSex.toLowerCase() == "male" || newSex.toLowerCase() == "female")) {
        sex = newSex;
      }
    }
  }
}

var pet = createPet("Vivie");
pet.getName();                  // Vivie
pet.setName("Oliver");
pet.setSex("male");
pet.getSex();                   // male
pet.getName();                  // Oliver
```

> 如果一个闭包的函数定义了一个和外部函数的某个变量名称相同的变量，那么这个闭包将无法引用外部函数的这个变量
>
> ```js
> var createPet = function(name) {  // Outer function defines a variable called "name"
>   return {
>     setName: function(name) {    // Enclosed function also defines a variable called "name"
>       name = name;               // ??? How do we access the "name" defined by the outer function ???
>     }
>   }
> }
> ```

### arguments 

函数的实际参数会被保存在一个类似数组的arguments对象中。

得到传入的参数：`arguments[i]`

参数数量：`arguments.length`

### 函数参数

从ECMAScript 6开始，有两个新的类型的参数：默认参数，剩余参数。

> 在JavaScript中，函数参数的默认值是`undefined`。

```js
// 默认参数和ES6-的对比

// ES6-
function multiply(a, b) {
  b = (typeof b !== 'undefined') ?  b : 1;

  return a*b;
}

multiply(5); // 5

// 默认参数
function multiply(a, b = 1) {
  return a*b;
}

multiply(5); // 5
```

> [剩余参数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/rest_parameters)语法允许将不确定数量的参数表示为数组

```js
function multiply(multiplier, ...theArgs) {
  return theArgs.map(x => multiplier * x);
}

var arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```

### 箭头函数

箭头函数总是匿名的

```js
var a = [
  "Hydrogen",
  "Helium",
  "Lithium",
  "Beryllium"
];

var a2 = a.map(function(s){ return s.length });

console.log(a2); // logs [ 8, 6, 7, 9 ]

var a3 = a.map( s => s.length );

console.log(a3); // logs [ 8, 6, 7, 9 ]
```

> 在箭头函数出现之前，每一个新函数都重新定义了自己的 [this](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this) 值（在构造函数中是一个新的对象；在严格模式下是未定义的

箭头函数捕捉闭包上下文的`this`值

```js
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // 这里的`this`正确地指向person对象
  }, 1000);
}

var p = new Person();
```

### 预定义函数

- `eval()`方法会对一串字符串形式的JavaScript代码字符求值。
- `uneval()`方法创建的一个[`Object`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)的源代码的字符串表示。  - 暂时不可以使用
- `isFinite()`函数判断传入的值是否是有限的数值。 如果需要的话，其参数首先被转换为一个数值。
- `isNaN()`函数判断一个值是否是[`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。 另一个可供选择的是ECMAScript 6 中定义[`Number.isNaN()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) , 或者使用 `typeof`来判断数值类型。
- `parseFloat()` 函数解析字符串参数，并返回一个浮点数。
- `parseInt()` 函数解析字符串参数，并返回指定的基数（基础数学中的数制）的整数。
- `decodeURI()` 函数对先前经过[`encodeURI`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)函数或者其他类似方法编码过的字符串进行解码。
- `decodeURIComponent()`方法对先前经过[`encodeURIComponent`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)函数或者其他类似方法编码过的字符串进行解码。
- `encodeURI()`与`encodeURIComponent()`都是编码的

# 表达式与运算符

### 运算符

- [赋值运算符(Assignment operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#赋值运算符)
- [比较运算符(Comparison operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#比较运算符)
- [算数运算符(Arithmetic operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#算术运算符)
- [位运算符(Bitwise operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#位运算符)
- [逻辑运算符(Logical operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#逻辑运算符)
- [字符串运算符(String operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#字符串运算符)
- [条件（三元）运算符(Conditional operator)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#conditional_operator)
- [逗号运算符(Comma operator)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#comma_operator)
- [一元运算符(Unary operators)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#delete)
- [关系运算符(Relational operator)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#关系操作符)

#### 赋值运算符

| 名字                                                         | 简写的操作符 | 含义          |
| :----------------------------------------------------------- | :----------- | :------------ |
| [赋值(Assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Assignment) | `x = y`      | `x = y`       |
| [加法赋值(Addition assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Addition_assignment) | `x += y`     | `x = x + y`   |
| [减法赋值(Subtraction assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Subtraction_assignment) | `x -= y`     | `x = x - y`   |
| [乘法赋值(Multiplication assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Multiplication_assignment) | `x *= y`     | `x = x * y`   |
| [除法赋值(Division assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Division_assignment) | `x /= y`     | `x = x / y`   |
| [求余赋值(Remainder assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Remainder_assignment) | `x %= y`     | `x = x % y`   |
| [求幂赋值(Exponentiation assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Exponentiation_assignment) | `x **= y`    | `x = x ** y`  |
| [左移位赋值(Left shift assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Left_shift_assignment) | `x <<= y`    | `x = x << y`  |
| [右移位赋值(Right shift assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Right_shift_assignment) | `x >>= y`    | `x = x >> y`  |
| [无符号右移位赋值(Unsigned right shift assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Unsigned_right_shift_assignment) | `x >>>= y`   | `x = x >>> y` |
| [按位与赋值(Bitwise AND assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Bitwise_AND_assignment) | `x &= y`     | `x = x & y`   |
| [按位异或赋值(Bitwise XOR assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Bitwise_XOR_assignment) | `x ^= y`     | `x = x ^ y`   |
| [按位或赋值(Bitwise OR assignment)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Bitwise_OR_assignment) | `x |= y`     | `x = x | y`   |

[解构赋值](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)语法是一个能从数组或对象对应的数组结构或对象字面量里提取数据的 Javascript 表达式。

```js
var foo = ["one", "two", "three"];

// 不使用解构
var one   = foo[0];
var two   = foo[1];
var three = foo[2];

// 使用解构
var [one, two, three] = foo;
```

#### 比较运算符

| 运算符                                                       | 描述                                                         | 返回true的示例                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--------------------------------- |
| [等于 Equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Equality) (`==`) | 如果两边操作数相等时返回true。                               | `3 == var1``"3" == var1``3 == '3'` |
| [不等于 Not equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Inequality) (`!=`) | 如果两边操作数不相等时返回true                               | `var1 != 4var2 != "3"`             |
| [全等 Strict equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Identity) (`===`) | 两边操作数相等且类型相同时返回true。 参见 [`Object.is`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is) and [sameness in JS](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness). | `3 === var1`                       |
| [不全等 Strict not equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Nonidentity) (`!==`) | 两边操作数不相等或类型不同时返回true。                       | `var1 !== "3"3 !== '3'`            |
| [大于 Greater than](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Greater_than_operator) (`>`) | 左边的操作数大于右边的操作数返回true                         | `var2 > var1"12" > 2`              |
| [大于等于 Greater than or equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Greater_than_or_equal_operator) (`>=`) | 左边的操作数大于或等于右边的操作数返回true                   | `var2 >= var1var1 >= 3`            |
| [小于 Less than](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Less_than_operator) (`<`) | 左边的操作数小于右边的操作数返回true                         | `var1 < var2"2" < 12`              |
| [小于等于 Less than or equal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Less_than_or_equal_operator) (`<=`) | 左边的操作数小于或等于右边的操作数返回true                   | `var1 <= var2var2 <= 5`            |

#### 算术运算符

| Operator        | Description                                                  | Example                                                      |
| :-------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 求余(`%`)       | 二元运算符. 返回相除之后的余数.                              | 12 % 5 返回 2。                                              |
| 自增(`++`)      | 一元运算符. 将操作数的值加一. 如果放在操作数前面 (`++x`), 则返回加一后的值; 如果放在操作数后面 (`x++`), 则返回操作数原值,然后再将操作数加一. | `var x=3;``console.log(++x); //4``console.log(x); //4``var y=3;``console.log(y++); //3``console.log(y); //4` |
| 自减(`--`)      | 一元运算符. 将操作数的值减一. 前后缀两种用法的返回值类似自增运算符. | var x=3; console.log(--x); //输入2,x=2var y=3;console.log(y--);//输出3,x=2; |
| 一元负值符(`-`) | 一元运算符,返回操作数的负值.                                 | var x=3; console.log(-x); //输入-3                           |
| 一元正值符(+)   | 一元运算符, 如果操作数在之前不是number，试图将其转换为number | `console.log( +'3' ); // 3``console.log( '3' ); // '3'`console.log(+true); // 1 |
| 指数运算符(**)  | 计算 `base(底数)` 的 `exponent(`指数`)次方`, 表示为`baseexponent` | `2 ** 3` returns `8`. `10 ** -1` returns `0.1`.              |

#### 位运算符

| perator                                                      | Usage     | Description                                                  |
| :----------------------------------------------------------- | :-------- | :----------------------------------------------------------- |
| 按位与[ AND](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_AND) | `a & b`   | 在a,b的位表示中，每一个对应的位都为1则返回1， 否则返回0.     |
| 按位或[ OR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_OR) | `a | b`   | 在a,b的位表示中，每一个对应的位，只要有一个为1则返回1， 否则返回0. |
| 按位异或[ XOR](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_XOR) | `a ^ b`   | 在a,b的位表示中，每一个对应的位，两个不相同则返回1，相同则返回0. |
| 按位非[ NOT](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_NOT) | `~ a`     | 反转被操作数的位。                                           |
| 左移[ shift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Left_shift) | `a << b`  | 将a的二进制串向左移动b位,右边移入0.                          |
| 算术右移                                                     | `a >> b`  | 把a的二进制表示向右移动b位，丢弃被移出的所有位.(译注:算术右移左边空出的位是根据最高位是0和1来进行填充的) |
| 无符号右移(左边空出位用0填充)                                | `a >>> b` | 把a的二进制表示向右移动b位，丢弃被移出的所有位，并把左边空出的位都填充为0 |

#### 逻辑运算符

| 运算符                                                       | 范例             | 描述                                                         |
| :----------------------------------------------------------- | :--------------- | :----------------------------------------------------------- |
| [逻辑与](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_AND)` (&&`) | `expr1 && expr2` | (逻辑与) 如果expr1能被转换为false，那么返回expr1；否则，返回`expr2`。因此`，&&`用于布尔值时，当操作数都为true时返回true；否则返回false. |
| [逻辑或 ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_OR)(`||`) | `expr1 || expr2` | (逻辑或) 如果expr1能被转换为true，那么返回expr1；否则，返回`expr2`。因此，\|\|用于布尔值时，当任何一个操作数为true则返回true；如果操作数都是false则返回false。 |
| [逻辑非](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_NOT)` (!)` | `!expr`          | (逻辑非) 如果操作数能够转换为true则返回false；否则返回true。 |

#### 字符串运算符

```js
console.log("my " + "string");

var myString = "alpha";
myString += "bet"; // 返回 "alphabet"
```

#### 条件（三元）运算符

```js
var status = (age >= 18) ? "adult" : "minor";
```

#### 逗号操作符

```js
var x = [0,1,2,3,4,5,6,7,8,9]

for (var i = 0, j = 9; i <= j; i++, j--)
  console.log('a[' + i + '][' + j + ']= ' + a[i][j]);
```

#### 一元操作符

一元操作符仅对应一个操作数。

- `delete`操作符，删除一个对象或一个对象的属性或者一个数组中某一个键值。

  ```js
  delete objectName;
  delete objectName.property;
  delete objectName[index];
  ```

  能使用 `delete` 删除各种各样的隐式声明， 但是被`var`声明的除外。

  如果 `delete` 操作成功，属性或者元素会变成 `undefined`。如果 `delete`可行会返回`true`，如果不成功返回`false`。

  > 删除数组中的元素时，数组的长度是不变的

#### typeof操作符

```js
var myFun = new Function("5 + 2");
var shape = "round";
var size = 1;
var today = new Date();

typeof myFun;     // returns "function"
typeof shape;     // returns "string"
typeof size;      // returns "number"
typeof today;     // returns "object"
typeof dontExist; // returns "undefined" =====

typeof true; // returns "boolean"
typeof null; // returns "object"   ====== 
typeof 62;    // returns "number"
typeof 'Hello world'; // returns "string"
typeof Date;     // returns "function"
typeof Function; // returns "function"
typeof Math;     // returns "object"
typeof Option;   // returns "function"  ========
typeof String;   // returns "function"
```

#### void 运算符

void表明一个运算没有返回值, 可以使用void运算符指明一个超文本链接。该表达式是有效的，但是并不会在当前文档中进行加载。

```html
<a href="javascript:void(0)">Click here to do nothing</a>

<a href="javascript:void(document.form.submit())">
Click here to submit</a>
```

#### 关系操作符

关系操作符对操作数进行比较，根据比较结果真或假，返回相应的布尔值。

**`in`**如果所指定的**属性**确实存在于所指定的对象中，则会返回`true`

```js
// Arrays
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
0 in trees;        // returns true
3 in trees;        // returns true
6 in trees;        // returns false
"bay" in trees;    // returns false (you must specify the index number,
                   // not the value at that index)
"length" in trees; // returns true (length is an Array property)

// Predefined objects
"PI" in Math;          // returns true
var myString = new String("coral");
"length" in myString;  // returns true

// Custom objects
var mycar = {make: "Honda", model: "Accord", year: 1998};
"make" in mycar;  // returns true
"model" in mycar; // returns true
```

#### `instanceof`运算符

如果所判别的对象确实是所指定的类型，则返回`true`。

### 表达式

JavaScript有以下表达式类型：

- 算数: 得出一个数字, 例如 3.14159. (通常使用 [arithmetic operators](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#Arithmetic_operators).)
- 字符串: 得出一个字符串, 例如, "Fred" 或 "234". (通常使用 [string operators](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#String_operators).)
- 逻辑值: 得出true或者false. (经常涉及到 [logical operators](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Expressions_and_Operators#Logical_operators).)
- 基本表达式: javascript中基本的关键字和一般表达式。
- 左值表达式: 分配给左值。

> [`this`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)关键字被用于指代当前的对象，通常，`this`指代的是方法中正在被调用的对象。

```js
this["propertyName"]
this.propertyName
```

扩展运算符

```js
function f(x, y, z) { }
var args = [0, 1, 2];
f(...args);
```

