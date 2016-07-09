---
title: HTML5特性
layout: post
category: HTML
tags: data_passing, view_render
---
---
# data-name 

> 'a great marriage of server side and client side' -Stephen Calvert, Quora  
> resources: https://www.quora.com/What-is-the-best-way-to-pass-server-side-variables-to-client-side-JavaScript  

HTML- `<div id="mydiv" `data-myval`="10"></div>`  
JS  
- `var a = $('#mydiv').data('myval');` //getter  
- `$('#mydiv').data('myval',20);` //setter  
Older browser  `var myval = element.getAttribute('data-myval');`  
Merely use config as json object  
		
		config = {
			userName: 'Scott Patten',
			userLogin: 'spatten',
			hasBoughtCurrentBook: true,
			followers: ['peterarmstrong', 'rolandtanglao']
		};
advance way (https://teamtreehouse.com/community/how-do-i-make-a-variable-passed-to-a-jade-template-by-an-express-route-accessible-for-use-in-js-on-the-rendered-page)  
- 1)On the server side javascript file you put the object as a JSON string on the request  
		
		res.render('index', { workflowData_server: JSON.stringify(workflowData) });

- 2) on the template view file,for example index.jade file you put script  
 var workflowData_client = !{workflowData_server} the ! is needed to unescape it to html  
- 3) now you can use the workflowData_client on your client javascript file,  
for example a public/angular.js file  
		
		angular.module('TestApp', []); angular.module('TestApp') .controller('MainController', ctrlFunc);

		function ctrlFunc() { this.workflowData = workflowData_client; }



