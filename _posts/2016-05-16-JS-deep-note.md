---
title: JS进阶笔记
layout: post
---

## JS类型  
五大原始类型--number,string,boolean,null,undefined  
Object对象类型，对象类型又包括--array,date,function

## 巧用+/-规则转换类型
把字符串变量转换成数字：num-0  
把数字变量转化成字符串型：num+''　　
## 比较
### 类型相同  
`null===null`, `undefined===undefined`  

NaN和任何东西都不相等，包括它本身  ```NaN≠NaN```  
Object同类型不相等，除非和它本身作比较 ``` new object() ≠ new object()```, ```x===x```  
### 类型不同
a === b 类型不同直接返回false  
a  == b 类型不同会尝试隐式转换(尝试类型转换和比较)  
    number== string // 把字符串转化为数字比较  
    boolean== ？(任何) // bool值转化为数字1或0  
    object == number|string // 尝试对象转为基本类型 
```new String('hi')=='hi' //true```  

## 包装类型
number string boolean 三种原始数据类型是有各自对应的对象包装类型的  
如果对一个原始的数据类型比如说var string = "xiaoyu" 进行对象的操作js会智能地将原始数据类型转换为一个对应的包装类型  ```string.length```  
等到你的操作结束之后这个临时产生的包装类型就会自动销毁。```string.tempobj```

## 类型检测
5种方法  
1. typeof 最简单的方法，以字符串的方式返回类型 `typeof "bob" === "string"`  

    > 弊端是null的失效(typeof返回的是"object"，因此不可以用来检测)  

2. 对象 instanceof 函数 原形链  

    > 弊端原生对象在不同iframe和window检测失效  

```
function Student(){}
function Person(){}
Student.prototype = new Person() //student指向person
var bob = new Student()
//bob instanceof student -> true
//bob instanceof person -> true
var bob_mom = new Person()
//mom instanceof student -> false
//mom instanceof person -> true
```
3. Object.prototype.toString.apply(函数)
    > 弊端null和undefined失效(IE返回object)

比较小窍门  
× ```arr1.sort().toString===arr2.sort().toString```  
× 比较类型保险款```Object.prototype.toString.apply(null)-> [Object Null]```

## 表达式expression
1. 原始表达式 // 常量、直接量、关键字、变量 3.14、"test"、this、null、i、k、j
2. 初始化表达式 //[1,2]、{x:1, y:2}
3. 函数表达式 //  var fe = function(){}、(function(){})()
4. 属性访问表达式 //  var o = {x:1} 可以用 o.x、o['x']来访问
5. 调用表达式 // func()；
6. 对象创建表达式 // new Func(1,2)、new Object

## 运算符operator
---
1、条件运算符 c?a:b c为true 则取a,否则取b  
2、逗号运算符 a,b 例如 var s = (1,2,3),则s依次赋值，最后输出为3  
3、delete运算符 delete obj.x 删除对象obj中的x属性     
> 在IE9下，obj中必须configurable:true 才可以删除，否则无效 

4、in运算符 判断obj是否有值或window里是否有变量，返回bool值   
    例如 attr in json 或 'document' in window  
5、instanceof 判断对象类型 {} instanceof Object // true  
6、new运算符 创建一个新对象 new obj / new array ...   
* 可以通过```hasOwnProperty()```判断属性是对象上的还是对象的原型链上的 (```in```判断obj是否有值,因此只要赋值就会返回true)
    
    ```
    function foo(){}
    foo.prototype.x = 1 //原形链赋值
    var obj = new foo() //obj.x = 1
    obj.hasOwnProperty('x') -> false
    obj.__proto__.hasOwnProperty('x') -> true
    obj.y = 1 //obj.hasOwnProperty('y') -> true
    
    ```
7、this对象 全局用指向window，函数内指向函数本身，浮动指针  
8、typeof 判断对象，返回对象类型 例如 typeof 100 === 'number' // true  
9、void 一元的，判断所有值，返回均为undefined

## block v. var语句
### block - ```{..}```定义  
在ES6之前，forloop中的var i ```for(var i=0;i<arr.length;i++)```是可以在之后取值的```console.log(i)```  
从ES6开始，let的出现-有了块级作用域的概念(local variable)

```
function letTest() {
  let x = 31;
  if (true) {
    let x = 71;  // different variable
    console.log(x);  // 71
  }
  console.log(x);  // 31
}
```
### var - ```var a =1``` 变量定义
误区：在函数里创建 ```var a = b = 1```是有local scope的  
解答：b相当于隐式创建的全局变量，因此即使是在函数内定义，在函数外b依旧可以被访问到，而a是不可以的  

> 解决办法是利用逗号 ```var a, b = 1 ``` a和b都变成了local variable
