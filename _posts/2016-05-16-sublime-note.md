---
title: Sublime应用笔记
layout: post
---

# Sublime hotkeys
Copy paste duplicate lines - CTRL + SHIFT + D

## 多行游标
1、Ctrl+H 查找替换  
2、Ctrl+D 选中内容  
3、Ctrl+K-->Ctrl+D 跳过选取  
4、Ctrl+D-->Atl+F3 全选匹配内容  
5、Ctrl+A --> Ctrl+Shift+L 拆分行  
6、鼠标放在单词上，按 Shift+鼠标右键下拉  

> 使用 Escape 可以退出多行游标模式。

## 命令模式 
对当前工程修改语法模式:Ctrl+shift+P -> 输入set syntax + 语言名称(如JavaScript)

### HTML
1、Alt+“.”：当前标签自动加行结尾标签。  
2、!+Ctrl+E：初始化模版。  
3、#和@：页面内查询。  
4、Ctrl+Enter：当前行代码下一换行。  
5、Ctrl+Shift+Enter：当前行代码上一换行。  
6、ul>.item$*3+Ctrl+E（注意：把光标放在当前行的末尾）  
```
    <ul>
		<li class="item1"></li>
		<li class="item2"></li>
		<li class="item3"></li>
	</ul>
```
7、Ctrl+}/]等同于tab：增加缩进；  
8、Ctrl+{/[等同于Shift+tab：减少缩进。  
9、标签名+{...}+Ctrl+E：自动排版，如：`h1{this is h1} --> <h1>this is h1</h1>`  
10、h1+Ctrl+E --> `<h1></h1>`  
11、Ctrl+E：html自动排版  
12、Ctrl+Shift+  

## Snippet及相关插件

1. ctrl+shift+p 输入 snippet：function 自动生成function的基本结构
2. 应用自动补全功能, 输入"fun",见提示后按Tab键或Enter键
3. Tab键能快速定位下一个name位置
4. 安装 Javascript& NodeJS Snippets插件,jQuery插件(get,post),和insert callback插件(alt+C)
5. 具体的snippet在插件官网查看

##目录创建新文件
使用Advance new file 插件来创建新文件 ctrl+Alt+N
列子：public/css/test.css
