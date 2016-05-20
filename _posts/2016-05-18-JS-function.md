---
title: JS函数
layout: post
---
---
# 函数(对象)

return语句或this作为返回值
## 不同创建方法
* 函数声明 `function foo(){}`  
声明会被前置 - 函数声明位置之前可以调用(类似于c在最前面建了constructor)
		
		var sum = add(a,b)
		function add (a,b){
			return a+b		
		} 
 
> 因此声明也不允许IEF立即调用 `function add(a,b){return a+b}()->NaN`  

* 函数表达式  

		var add = function(){}//function variable
		(function(){})()//IEF立即执行
		return function(){}//first-class function->闭包closure
		var add = function foo(){}//NFE命名式 

> 函数表达式不可以通过函数的名字去调用 `foo()//报错，add()//正常`

* **不懂** NFE命名式(不常见)  

		var func = function nfe(){}//出错
		var func = function nfe(){ nfe() }//递归callback调用

* Function构造器(不常见)  

		var func = new Function('a','b','console.log(a+b)')
		
  > local不可访问（因为被提前声明， localVal 显示为underfined），global变量可以访问  
 
## this
> this总是指向调用该方法的对象  

* 全局 this.document === document  
* 函数全局 function foo(){return this//window}  
* 作为对象方法的函数  

		var o = {
			prop: 37,
			f: function(){return this.prop}
		}
		console.log(o.f())

		var o2 = {prop:37}
		function independent(){ return this.prop }
		o2.f = independent
		console.log(o2.f())

* 对象原型链上  

		var yuanxing = {
			f: function(){
				return this.a+this.b
			}
		}		
		var o = Object.create(yuanxing)
		console.log(o.f())//undefined
		o.a = 1
		o.b = 2
		console.log(o.f())//3

* get/set方法与this  

		function product(){ return this.a*this.b }
		var num = { 
			a:1, 
			b:-1,
			get sum(){ return this.a + this.b }
		}

		Object.defineProperty(num,'product',{
			get: product,
		})//添加新的get
		console.log(num.product)//-1
		console.log(num.sum)//0

* new构造器与this  

		function foo(){ this.a = 37 }
		var obj = new foo()
		console.log(obj.a)//37 

  > 当使用new构造器创建函数时没有return，将this作为返回值  

* call/apply方法与this - 改变函数体内部 this 的指向  
  whitedog = {food:"bone"}   
  blackcat.say.call(whitedog)来让this指向whitedog并调用blackcat的say方法  

		function cat(){}
		cat.prototype = {
			food:'fish',
			say: function(){
				console.log("i love "+this.food)
			}
		}

		var blackcat = new cat()
		blackcat.say()
		var whitedog = {food:'bone'}
		blackcat.say.call(whitedog)

  > 什么时候要用 - 比如说想要调用Object.prototype.toString，但是想指定其中的某一个this时，就可以用Object.prototype.toString.call（）这样的方法去调用没办法直接调用的方法。  

* bind绑定  

		var g = function f(){return this.a}.bind({a:"test"})
		console.log(g())//test


## arguments实际传入的参数
!["chart"](http://img.mukewang.com/5608d60d000103e812800720.jpg)  

bind & currying - 可以重复使用类似的函数  
		
		function abwhatever(a,b,c){ console.log(a,b,c) }
		var Default = abwhatever.bind(undefined/null,'a','b') //没有this传入, a和b被固定住
		Default('z')//a,b,z
		Default('yo')//a,b,yo

bind & new - bind失效  
		
		function foo(){ this.b = 100; return this.a}
		var func = foo.bind({a:1})
		func()//1
		new func()//this指向原来的，a没有值，用this.b


## 作用域scope (link)

## 不同调用方式
* 直接调用 foo()  
* 对象方法 foo.method()  
* 构造器   new foo()  
* call/apply/bind func.call(obj)  


