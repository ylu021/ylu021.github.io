---
title: 属性标签,对象标签,序列化
layout: post
---
---
#标签
##属性标签
查看
* Object.getOwnPropertyDescriptor({pro:true},'tagname')  
* Object.keys()

## 原型标签
`__proto__`

## class标签

##extensible标签
isExtensible(obj)
preventExtensions(obj) 不可以添加新的属性yo
obj.z = 1不可以yo
.seal(obj) //不可以改
configurable变为false
.freeze(obj)//不可写
writable变为false

#序列化
`JSON.stringify(obj)`  
> undefined会被忽略
> NaN会变成null
> new Date()是UTC格式

变为对象
var obj = JSON.parse('{`"x"`:1}')
> 后端返回来JSON数据时，采用JSON.parse来转化  
> 合法的JSON的属性必须用双引号引起来

#### inner函数
- toJSON
o里面有o1:1和o2:2,利用
toJSON: function(){
	return this.o1+this.o2
}的方法可以得到JSON.stringify=> o: 3

- 自定义toString/valueOf
obj.toString/valueOf = function(){return this.x + this.y}
"result "+ obj //"result 3" obj.x 和y还是可以被访问到的

> valueOf是返回对象原始值,toString是将转化成字符串。  
> valueOf - 尝试把对象转换为基本类型时自动调用的函数

>当toString 和 valueOf 同时存在，先寻找valueOf，如果不存在或不合法的值（为对象），则再寻找toString；否则使用valueOf的方法。
