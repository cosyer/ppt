title: Javascript小知识介绍
transition: rollIn

[slide]
## const变量声明

- const 声明一个块级作用域的常量 但并不是真正意义上的'常量' 并不意味着它所持有的值是不可变的，只是变量标识符不能重新分配（赋值）。
- 基本类型的值是不变的 引用类型的值是可变的
基本类型和存储类型存储方式的不同。

-- 栈内存

对于基本类型 保存变量标识符和变量值
对于引用类型 保存变量标识符和指向堆内存中该对象的指针 
即对象的引用保存在栈内存，对象的属性名和属性值保存在堆内存。

-- 堆内存

保存引用类型具体的内容

```javascript
const a = [0,1,2,3]
a[0] = 10086

const b = {name: 'zhangsan' , age: 25}
b.age = 30
```

## for...in遍历对象属性
```javascript
var a = {1:1,name:'cosyer',2:2}
for (let i in a) {
  if(a.hasOwnProperty(i)){
      console.log(i)
  }
}
// for in 的循环顺序 => 遍历首先数字的可以接着按照创建顺序遍历
// 排序规则同样适用于下列API：
// Object.entries
// Object.values
// Object.keys
// Object.getOwnPropertyNames
// Reflect.ownKeys
```
## 合并对象属性 去除多余的属性参数
```javascript
Object.assign({ a: 1, b: 2 }, ...{ b: 3, c: 3 })
const newObj = { ...{ a: 1, b: 2 }, ...{ b: 3, c: 3 } } 
```

## Math.min()和Max.max()
```javascript
var min = Math.min();
var max = Math.max();
console.log(min < max); // false
```

## splice(index, count_to_remove, addElement1, addElement2, ...)从数组移出一些元素，（可选）并替换它们。
```javascript
var myArray = new Array ("1", "2", "3", "4", "5");
myArray.splice(1, 3, "a", "b", "c", "d"); 
// myArray is now ["1", "a", "b", "c", "d", "5"]
```

## [1,2,11]用sort方法进行排序
```javascript
[1,2,11].sort() // [1,11,2] sort方法默认根据unicode进行排序

[1,undefined,null].sort() // [1, null, undefined]
```

## [1,2,3].map(parseInt)
```javascript
[1,2,3].map(parseInt) // [1,NaN,NaN] 这里第二个参数是map的index，3对应下标2，3没有二进制的。

parseInt("11",2);		//返回 3 (2+1)
```
parseInt第二个参数	
> 可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。

> 如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。

> 如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN。

## ES6数组includes方法（判断一个数组是否包含一个指定的值，如果是返回 true，否则false。）
相同点：二者所传的参数是一样的，第一个参数传要判断的元素，第二个参数传开始检索的下标位置
不同点：返回值不同
1、indexOf：返回的是元素的所在下标，如果不存在则返回-1
优点：元素存在可获取到元素的位置 
缺点：(1)无法判断是否有NaN的元素(2)返回的值不够语义化，需要我们进行处理

2、includes：返回一个Boolean值，有：true，没有：false
优点：(1)可判断NaN元素(2)返回值十分语义化，不需要再次处理 
缺点：无法获取元素的下标
```javascript
// NaN
[NaN,1,2].indexOf(NaN) // -1
[NaN,1,2].includes(NaN) // true

// undefined
[undefined,1,2].indexOf(undefined) // 0
[undefined,1,2].includes(undefined) // true

// includes能判断未声明的undefined
var a =[];
a[1] = 2;
// a[0] === undefined true
a.indexOf(undefined) // -1
a.includes(undefined) // true

// 取反运算简化indexOf判断
if(~[1,2,3].indexOf(1)){
    // 存在
}else {
    // 不存在
}
```

## 清空数组
1. a = []; // 重新赋值
2. splice(0,数组length)清空
3. a.length属性赋为0

## 判断奇偶（只考虑数字类型为整数的情况）
```javascript
// 2&1
// 10
// 01
// 00 ->0

// 3&1
// 11
// 01
// 01 ->1

// 与运算
if(n&1){
    // 奇数
}else{
    // 偶数
}

if(num%2 ==0){
    // 偶数
}else{
    // 奇数
}
```

## 取整
[slide]