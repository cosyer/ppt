title: Javascript小知识介绍
transition: rollIn

[slide]
## const变量声明

![Store](/images/store.png)

[slide]

```javascript
const a = [0,1,2,3]
a[0] = 10086

const b = {name: 'zhangsan' , age: 25}
b.age = 30
```

- 每次使用const或者let去初始化一个变量的时候，会首先遍历当前的内存栈，看看有没有重名变量，有的话就返回错误。

```javascript
let a = 1;
let a = 1; // error
const b = 1;
const b = 1; // error
```

[slide]

## for...in遍历对象属性
```javascript
var a = {1:1,name:'cosyer',2:2}
for (let i in a) {
  if(a.hasOwnProperty(i)){
      console.log(i)
  }
}
Object.keys(a) // ['1','2',name]
// 排序规则同样适用于下列API：
// Object.entries
// Object.values
// Object.keys
// Object.getOwnPropertyNames
// Reflect.ownKeys
```

[slide]
- IE6 IE7 IE8 Firefox Safari 的 JavaScript 解析引擎遵循的是较老的 ECMA-262 第三版规范，属性遍历顺序由属性构建的顺序决定。

- Chrome Opera 中使用 for-in 语句遍历对象属性时会遵循一个规律：
它们会先提取所有 key 的 parseFloat 值为非负整数的属性，然后根据数字顺序对属性排序首先遍历出来，然后按照对象定义的顺序遍历余下的所有属性。

[slide]
## 合并对象属性 去除多余的属性参数
```javascript
Object.assign({ a: 1, b: 2 }, { b: 3, c: 3 })
const newObj = { ...{ a: 1, b: 2 }, ...{ b: 3, c: 3 } } 
```

[slide]
## Math.min()和Max.max()
```javascript
var min = Math.min(); // Infinity
var max = Math.max(); // -Infinity
console.log(min < max); // false
```

[slide]
## [1,2,11]用sort方法进行排序
```javascript
[1,2,11].sort() // [1,11,2] sort方法默认根据unicode进行排序

[1,undefined,null].sort() // [1, null, undefined]
```

[slide]
## [1,2,3].map(parseInt)
```javascript
[1,2,3].map(parseInt) // [1,NaN,NaN] 这里第二个参数是map的index，3对应下标2，3没有二进制的。

parseInt("11",2);		//返回 3 (2+1)
```
- parseInt第二个参数

> 可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。

> 如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。

> 如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN。

[slide]
## ES6数组includes方法

1. indexOf：返回的是元素的所在下标，如果不存在则返回-1
 - 优点：元素存在可获取到元素的位置 
 - 缺点：(1)无法判断是否有NaN的元素(2)返回的值不够语义化，需要我们进行处理

2. includes：返回一个Boolean值，有：true，没有：false
 - 优点：(1)可判断NaN元素(2)返回值十分语义化，不需要再次处理 
 - 缺点：无法获取元素的下标

[slide]
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

[slide]
## 清空数组
1. a = []; // 重新赋值
2. splice(0,数组length)清空
3. a.length属性赋为0

[slide]
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

[slide]
## JS Date对象溢出
```javascript
var year = 2015,month = 1,d = 1;//m is from 0 to 11

var date = new Date(); //当前日为2015年4月30.

date.setFullYear(year);

date.setMonth(month);//执行后日期变为2015年2月30.，2015年2月无此日期。28日为最后一天，30-28=2。延后2天得日期变为2015年3月2日。

date.setDate(d);//日期变为2015年3月1日

期望得到date为：2015年2月1日

实际得到date为：2015年3月1日.
```

[slide]
## 已知年月，求当月多少天
- 先判断该年份是否是闰年，来处理 2 月份情况，闰年 2 月共 29 天，非闰年 2 月共 28 天
- 再判断其他月份，如 1 月共 31 天，4 月共 30 天

**更简便的方法**
```javascript
// Date API 处理日期溢出时，会自动往后推延响应时间
// month的取值为0-11
function getMonthCountDay (year, month) {
  return 32 - new Date(year, month-1, 32).getDate();
  // 32 - (32-当月天数) = 当月天数
}
// better
function getMonthCountDay (year, month) {
  return new Date(year, month , 0).getDate();
}
```
[slide]
## JSON.parse和JSON.stringify其他参数
```javascript
var obj ={name:'cosyer',age:15}
var newobj = JSON.stringify(obj)

JSON.parse(newobj,(key,value)=>{
console.log(1111111111111,key,value);
});
// name cosyer 
// age 15 
// "" {}

// 3个参数
// JSON.stringify(jsonObj,repalce,space)
// replace可以是数组或者回调函数
const testJSON = {
   name: 'test',
   cities: {
      shanghai: 1,
   },
};

JSON.stringify(testJSON, ['name']);

// "{"name": 'test'}"
```
[slide]

```javascript
JSON.stringify(testJSON, ['name', 'cities']);
 
//  "{"name": 'test', "cities": {}}"

JSON.stringify(testJSON, ['name', 'cities', 'shanghai']);

// "{"name": 'test', "cities": {"shanghai": 1}}"

JSON.stringify(testJSON, (key, value) => {
    // 遍历对象
    if (key === 'cities') {
       return  'cities';
    } 
    return value; // 确认value???
});

// "{"name": 'test', "cities": 'cities'}"

JSON.stringify(testJSON, undefined, '...');

// "{
//    ..."name": 'test',
//    ..."city": 'shanghai',
//   }"
```

[slide]
```javascript
JSON.stringify(testJSON, undefined, 7);

// "{
//          "name": 'test',
//          "city": 'shanghai',   // 缩进7个空格
// }"

JSON.stringify({name:123,age:24},null,'\t')
// "{
// 	"name": 123,
// 	"age": 21
// }"
```

[slide]
# Thanks！