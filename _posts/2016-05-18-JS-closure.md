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

## 作用域scope
因为JS有全局/局部变量的限制，不能从外部读取局部变量  

### Closure闭包 - 为了从外部读取局部变量而在函数的内部再创建的函数  
> 同时根据**chain scope**链式作用域的定义,父对象的所有变量，对子对象都是可见的，反之则不成立  
> 因此直接call f1() 没有返回值，要var result = f1()，再call result()  

  闭包的第二种用途 - 让局部变量保持在内存中(localval可以连续调用)  

好处  
函数有自己的作用域，定义的变量外部访问不到。封装具体的复杂的函数逻辑  
弊端  
  * 内存消耗，解决方法是删除不使用的局部变量  
  * 父函数的值会受闭包的影响  

循环的陷阱 - i是全局变量，addEventListener()是一个callback函数，只有等循环结束后才会执行（i=4)。  
解决方法是使用IEF匿名函数来立即调用闭包环境的i值  
		
		var i = 1		
		for(;i<4;i++){
			document.getElementById('div'+i)
			.addEventListener('click',function(){
				console.log(i)//闭包内全是4			
			})		
		}
		
		var i = 1
		for(;i<4;i++){
			(function(i){//得到闭包环境的i
				document.get...//返回正常			
			})(i)		
		}
 

公用/私用  
  私用  
    * 封装 - 从外部看不到复杂的计算并实现函数的私有变量的调用
	!["chart"](http://img.mukewang.com/56a8b573000103af12800720.jpg)  

  子函数本身的this指向它所在函数**调用**的上下文决定的  

		var name = "The Window";
		var object = {
			name : "My Object",
			getNameFunc : function(){
				return function(){
					return this.name;
				}
			}
		}
		alert(object.getNameFunc()());//window.name

  子函数得到了object的this - **著名的that = this**  

		var name = "The Window";
		var object = {
			name : "My Object",
			getNameFunc : function(){
				var that = this;
				return function(){
					return that.name;
				};
			}
		};
		alert(object.getNameFunc()());

> [更多闭包的资料](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html "阮一峰的网络日志")

## 不同调用方式
* 直接调用 foo()  
* 对象方法 foo.method()  
* 构造器   new foo()  
* call/apply/bind func.call(obj)  


