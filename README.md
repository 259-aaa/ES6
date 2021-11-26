# 1、简介

全称是	ECMAScript，它是由ECMA国际标准化组织，指定的**一项脚本语言的标准化规范**（泛指ES2015以及后续的版本）。



# 2、新增语法

ES6中新增的用于声明变量的关键字。

## 2.1	let

- **let**	声明的变量只在所处于的块级有效

```javascript
if (true) {
let a = 10;
    console.log(a);	//	10
}
console.log(a)	//	a is not defined
```

**总结：**

1. let关键字就是用来声明变量的，使用let关键字声明的变量具有块级作用域
2. 在一个大括号中 使用let关键字声明的变量才具有块级作用域 var关键字是不具备这个特点的
3. 防止循环变量变成全局变量
4. 使用let关键字声明的变量没有变量提升（先声明再使用）
5. 使用let关键字声明的变量具有暂时性死区特性

## 2.2	const

- **const**	声明常量，常量就是值（内存地址）不变化的量（具有块级作用域）

```javascript
if (true) {
const a = 10;
    console.log(a);	//	10
}
console.log(a)	//	a is not defined
```

**总结：**

1. 使用const关键字声明的常量具有块级作用域
2. 使用const关键字声明的常量必须赋初始值
3. 常量声明后值不可更改(值分配的内存地址)

## 2.3	let、const、var的区别

**总结：**

1. 使用 **var** 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象
2. 使用 **let** 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升
3. 使用 **const** 声明的变量，在后面出现的代码中不能再修改该常量的值

| var          | let            | const          |
| ------------ | -------------- | -------------- |
| 函数级作用域 | 块级作用域     | 块级作用域     |
| 变量提升     | 不存在变量提升 | 不存在变量提升 |
| 值可更改     | 值可更改       | 值不可更改     |

## 2.4	解构赋值

按照一定模式，从数组中或对象中，将提取出来的值赋值给另外的变量。

- 数组解构

```javascript
let ary = [1,2,3];
let [a, b, c, d, e] = ary;
console.log(a)  // 1
console.log(b)  // 2
console.log(c)  // 3
console.log(d)  // undefined
console.log(e)  // undefined
```

- 对象解构

```javascript
let person = {name: 'zsq', age:259};
let {name, age} = person;
console.log(name);	//	zsq
console.log(age);	//	259

let {name: myName} = person;
console.log(myName);	//	zsq
```

## 2.5 箭头函数

- ES6中新增的定义函数的方法。

```javascript
() => {}
```

```javascript
const fn = () => {
    console.log(123)
}
fn();
```

- 在箭头函数中，如果函数体中只有一句代码，并且代码的执行结果就是函数的返回值，函数体大括号可以省略。

```javascript
const sum = (n1, n2) => n1 + n2;
const result = sum(10, 20);
console.log(result);
```

- 在箭头函数中，如果形参只有一个 形参外侧的小括号也是可以省略的。

```javascript
const fn1 = (v) => {
    console.log(v);
};
fn1(20);
```

- 箭头函数不绑定this关键字，箭头函数中的this，指向的是**函数定义位置的上下文this**。

```javascript
const obj = {name: '张三'};
function fn () {
    console.log(this);
    return () => {
        console.log(this);
    }
}
const resFn = fn.call(obj);
resFn();

```

## 2.6	剩余参数

- 剩余参数语法允许我们将一个不定数量的参数表示为一个数组。

```javascript
function sum(first, ...args) {
    console. log (first) ; // 10
    console. log (args) ; // [20,30]，剩余函数
}
sum(10, 20, 30)

```

## 2.7	扩展运算符（展开语法，与剩余参数相反）

- 将数组或者对象转为用逗号分隔的参数序列。

```javascript
let ary = ["a", "b", "c"];
// ...ary // "a", "b", "c"
console.log(...ary);			//	a b c
console.log("a", "b", "c");		//	a b c

```

- 扩展运算符应用于数组合并

2.7.1	合并数组方法一

```javascript
let ary1 = [1, 2, 3];
let ary2 = [4, 5, 6];
// ...ary1 // 1, 2, 3
// ...ary1 // 4, 5, 6
let ary3 = [...ary1, ...ary2];
console.log(ary3);	//	[1, 2, 3, 4, 5, 6]

```

2.7.2	合并数组方法二

```javascript
let ary3 = [1, 2, 3];
let ary4 = [4, 5, 6];
ary3.push(...ary4);
console.log(ary3);

```

- 利用扩展运算符将伪数组转换为真正的数组

```javascript
var oDivs = document.getElementsByTagName("div");
console.log(oDivs);
var ary5 = [...oDivs];
ary5.push("a");
console.log(ary5);

```

# 3、Array 的扩展方法

## 3.1	构造函数方法：Array.from()

- 将伪数组或可遍历对象转换为真正的数组。

```javascript
var arrayLike = {
    "0": "张三",
    "1": "李四",
    "2": "王五",
    "length": 3
}
var ary = Array.from(arrayLike);
console.log(ary);

```

- 方法还可以接收第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

```javascript
var arrayLike = {
    0: "1",
    1: "2",
    length: 2,
};
var ary = Array.from(arrayLike, (item) => item * 2);
console.log(ary);

```

## 3.2	实例方法：find()

- 用于找出第一个符合条件的数组成员，如果没有找到返回undefined

```javascript
var ary = [
    {
        id: 1,
        name: "张三",
    },
    {
        id: 2,
        name: "李四",
    },
];
let target = ary.find((item) => item.id == 2);
let target2 = ary.find((item) => item.id == 3);
console.log(target);
console.log(target2);

```

## 3.3	findIndex()

- 用于找出第一个符合条件的数组成员的位置，如果没有找到返回-1。

```javascript
let ary = [10, 20, 50];
let index = ary.findIndex((item) => item > 15);
console.log(index);

```

## 3.4	includes()

- 表示某个数组是否包含给定的值，返回布尔值。

```javascript
let ary = ["a", "b", "c"];
let result = ary.includes("a");
result = ary.includes("e");
console.log(result);  //  true
console.log(result);  //  false

```

# 4、String 的扩展方法

## 4.1	模板字符串

ES6新增的创建字符串的方法，使用反引号定义。

- 模板字符串中可以**解析变量**。

```javascript
let name = `张三`;
let sayHello = `Hello, 我的名字叫${name}`;
console.log(sayHello);	//	Hello, 我的名字叫张三

```

- 模板字符串中可以**换行**。

```javascript
let result = {
    name: "zhangsan",
    age: 20,
};
let html = `
<div>
    <span>${result.name}</span>
    <span>${result.age}</span>
</div
`;
console.log(html);

```

- 在模板字符串中可以调用**函数**。

```javascript
const fn = () => {
    return "我是fn函数";
};
let html2 = `我是模板字符串 ${fn()}`;
console.log(html2);

```

## 4.2	startsWidth()

- 表示参数字符串是否在原字符串的头部，返回布尔值

```javascript
let str = 'Hello ECMAScript 2015';
let r1 = str.startsWith('Hello');
console.log(r1);	//	true

```

## 4.3	endsWidth()

- 表示参数字符串是否在原字符串的尾部，返回布尔值

```javascript
let str = 'Hello ECMAScript 2015';
let r2 = str.endsWith('2016');
console.log(r2);	//	false

```

## 4.4	repeat()

- 表示将原字符串重复n次，返回一个新字符串。

```javascript
console.log("y".repeat(5));

```

# 5、Set 数据结构

##  5.1	创建 Set 数据结构

```javascript
const s1 = new Set();
console.log(s1.size); //  0
const s2 = new Set(["a", "b"]);
console.log(s2.size); //  2

```

## 5.2	利用 Set 数据结构做数组去重

```javascript
const s3 = new Set(["a", "a", "b", "b"]);
console.log(s3.size); //  2
//  去重
const ary = [...s3];
console.log(ary);     //  2

```

## 5.3	实例方法

- add(value)：添加某个值，返回 Set 结构本身。

```javascript
const s4 = new Set();
s4.add("a").add("b");
console.log(s4.size); //  2

```

- delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。

```javascript
const r1 = s4.delete('c');
console.log(s4.size); //  2
console.log(r1);      //  false

```

- has(value)：返回一个布尔值，表示该值是否为 Set 的成员。

```javascript
const r2 = s4.has("d");
console.log(r2);     // false

```

- clear()：清除所有成员，没有返回值。

```javascript
s4.clear();
console.log(s4.size); //  0

```

- **遍历**

Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

```javascript
const s5 = new Set(["a", "b", "c"]);
s5.forEach((value) => {
    console.log(value); //  a b c
});

```

