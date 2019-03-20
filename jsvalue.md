title: 理解JS的类型、值、类型转换
transition: rollIn

[slide]
# 理解JS的类型、值、类型转换
## 陈宇

[slide]

![js的类型](/images/type1.png)

[slide]

![xmind画的图](/images/type2.png)

[slide]

## 特殊的null
用typeof来检查上述七种类型时，返回的是对应的类型字符串值

但，有一个例外
```js
typeof null === 'object' // true
// null是唯一一个用typeof检测会返回object的基本类型值
// 在JavaScript中二进制前三位为0的话都会被判断为object类型
// 而null的二进制表示全是0
```

```js
typeof Function; // 'function'
typeof new Function(); // 'function'
typeof function() {}; // 'function'

typeof Array; // 'function'
typeof Array(); // 'object'
typeof new Array(); // 'object'
typeof []; // 'object'

typeof Boolean; // "function"
typeof Boolean(); // "boolean"
typeof new Boolean(); // "object"

typeof Math; // 'object'
typeof Math(); // Math is not a function
typeof new Math(); // Math is not a constructor
```

typeof适合用来检查基本类型

[slide]

## 拿Array举例子
```js
typeof Array; // 'function'
typeof Array(); // 'object'
typeof new Array(); // 'object'
typeof []; // 'object'
```
Array是个构造函数，所以直接打印出function
但构造出来的Array()却又是另一回事了，构造出来的结果是个数组，自然属于引用类型，所以也就打印出了'object'

> 构造函数 Array(..) 不要求必须带 new 关键字。不带时，它会被自动补上。 因此 Array(1,2,3) 和 new Array(1,2,3) 的效果是一样的

## 基本包装类型
```js
typeof Boolean; // "function"
typeof Boolean(); // "boolean"
typeof new Boolean(); // "object"
```
Boolean是个构造函数，第一句没问题
Boolean()直接执行，得出了布尔值，所以得到了'boolean'

而new出来的是个Boolean对象，具体来说就是：通过构造函数创建出来的是封装了基本类型值的封装对象

## Math到底是什么？
Math和Global（浏览器中替代为window）都是内置的对象，并不是引用类型的一种。既不是对象也不是构造器
```js
typeof Math; // 'object'
typeof Math(); // Math is not a function
typeof new Math(); // Math is not a constructor
```

[slide]
## 值

JS的执行上下文生成之后，会创建一个叫做变量对象的特殊对象（关于变量对象在我的其他文章中有讲到），JS的基础类型都保存在变量对象中

> 严格意义上来说，变量对象也是存放于堆内存中，但是由于变量对象的特殊职能，我们在理解时仍然需要将其于堆内存区分开来。

但引用数据类型的值是保存在堆内存中的对象。JavaScript不允许直接访问堆内存中的位置，因此我们不能直接操作对象的堆内存空间。
在操作对象时，实际上是在操作对象的引用而不是实际的对象。因此，引用类型的值都是按引用访问的。
这里的引用，我们可以理解为保存在变量对象中的一个地址，该地址与堆内存的实际值相关联。

![store2](/images/store2.png)

[slide]
## 强制类型转换
> 类型转换发生在静态类型语言的编译阶段，而强制类型转换则发生在动态类型语言的运行时(runtime)。

然而在 JavaScript 中通常将它们统称为强制类型转换，还可以用“隐式强制类型转换”(implicit coercion)和“显式强制类型转换”(explicit coercion)来区分。


## 字符串、数字和布尔值之间类型转换的基本规则

### 显示类型转换
1. 转换为字符串
- String(mix)
（1）如果有toString()方法，则调用该方法（不传递radix参数）并返回结果
（2）如果是null，返回'null'
（3）如果是undefined，返回'undefined'
- toString(radix)可以被显式调用，或者在需要字符串化时自动调用
除undefined和null之外的所有类型的值都具有toString()方法，其作用是返回对象的字符串表示。

null 转换为 "null"，undefined 转换为 "undefined"，true 转换为 "true"。
> 数字的字符串化则遵循通用规则
> 极小和极大的 数字使用指数形式:
```js
// 1.07 连续乘以七个 1000
var a = 1.07 * 1000 * 1000 * 1000 * 1000 * 1000 * 1000 * 1000;
// 七个1000一共21位数字 
a.toString(); // "1.07e21"
```

数组的默认 toString() 方法经过了重新定义，将所有单元字符串化以后再用 "," 连接起 来
```js
var a = [1,2,3];
a.toString(); // "1,2,3"
```

2. 转化为数字
- Number(mix)
其中 true 转换为 1，false 转换为 0。undefined 转换为 NaN，null 转换为 0。
处理失败时返回 NaN(处理数字常量失败时会产生语法错误)
如果是字符串，遵循以下规则：

1、如果字符串中只包含数字，则将其转换为十进制（忽略前导0）
2、如果字符串中包含有效的浮点格式，将其转换为浮点数值（忽略前导0）
3、如果是空字符串，将其转换为0
4、如果字符串中包含非以上格式，则将其转换为NaN

如果是对象，则调用对象的valueOf()方法，然后依据前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的toString()方法，再次依照前面的规则转换返回的字符串值。

3. Boolean(mix)
假值的概念 所有的对象都是真值
- undefined
- null
- false
- +0、-0 和 NaN
- ""

[slide]
## 隐式类型转换
1. 用于检测是否为非数值的函数：isNaN(mix)
> isNaN()函数，该函数会尝试将参数值用Number()进行转换，如果结果为NaN则返回true，否则返回false。

2. 算数运算符、一元正负符号操作符、取模运算符(%)、递增递减运算符(前置后置)
如果操作值之一不是数值，则被隐式调用Number()函数进行转换
```js
+true // 1

-'' // 0

1*true // 1

1/true // 1

2%true // 0

let a = false;
++a; // 1

+new Date() // 调用对象的valueOf()方法
```

3. 关系操作符（<, >, <=, >=）
调用Number()转换
NaN是非常特殊的值，它不和任何类型的值相等，包括它自己，同时它与任何类型的值比较大小时都返回false。 

4. ` + `也用于字符串连接符如果, + 的其中一个操作数是字符串(或者通过以上步骤可以得到字符串)， 则执行字符串拼接;否则执行数字加法。

```js
'42' + '0'; // "420"
'42' + 0; // "420"
42 + 0; // 42
```

如果只有一个操作值为字符串，则将另外操作值转换为字符串，然后拼接起来
如果一个操作数是对象、数值或者布尔值，则调用toString()方法取得字符串值，然后再应用前面的字符串规则。对于undefined和null，分别调用String()显式转换为字符串。

[slide]
```js
console.log([] + {}); // [object Object]
console.log({} + []); // [object Object]
[] + {} // "" + "[object Object]" => "[object Object]"
{} + [] // +[] => 0
// {} 其实应该当成一个代码块，而不是一个 Object，但在console.log使用的时候，{} 被当成了一个 Object
```

[slide]
3. 发生强制转换成布尔值的场景
1. if (..)语句中的条件判断表达式。
2. for ( .. ; .. ; .. )语句中的条件判断表达式(第二个)。
3. while (..) 和 do..while(..) 循环中的条件判断表达式。
4. ? :中的条件判断表达式。
5. 逻辑运算符 ||(逻辑或)和 &&(逻辑与)左边的操作数(作为条件判断表达式)。逻辑非（！）操作符首先通过Boolean()函数将它的操作值转换为布尔值，然后求反。

```js
a || b;
// a ? a : b;
a && b;
// a ? b : a;
```

## ==和===
> "== 允许在相等比较中进行强制类型转换，而 === 不允许。"

- x == y

首先判断 x 和 y 的数据类型，如果数据类型相同，则判断值是否相同，如果相同则为 true , 否则为 false。其中需要注意的是 Number 类型，如果 x 和 y，二者中至少有一个为 NaN，则为 false；。如果类型不同，则会进行类型转换。
如果 x 和 y，二者中一个为 null ，一个为 undefined ，则为 true；
如果 x 和 y 中，一个是 Number 类型，一个是 String 类型，则将 String 类型的数据转换为 Number 类型；
如果 x 和 y 中，一个是 Boolearn 类型，则将 Boolearn 类型的数据转换为 Number 类型，true -> 1，false -> 0；
如果 x 和 y，二者中一个为 Object ，另一个为 Number 或 String ，则为会调用 ToPrimitive(Object)，然后再将其返回值跟另一个值进行比较；
如果不满足上述的判断，则返回 false 。除了 null 和 undefined 以外，其他类型的数据，与 null 和 undefined 
进行 == 比较时，直接返回 false。

```js
'123' == new String('123') // true
```

[slide]

Thanks!
