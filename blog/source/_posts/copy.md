---
title: copy
date: 2017-08-23 17:35:46
tags:
---

# 复制

```
var json1={"name":"鹏哥","age":18,"arr1":[1,2,3,4,5],"string":'afasfsafa',"arr2":[1,2,3,4,5],"arr3":[{"name1":"李鹏"},{"job":"前端开发求职"}]}; 
var json2={}; 
function copy(obj1,obj2){ 
	var obj2=(obj1.constructor===Array)?[]:{}; 
	for(var name in obj1){ 
		if(typeof obj1[name] === "object"){ 
		  	obj2[name]= (obj1[name].constructor===Array)?[]:{}; 
		   	copy(obj1[name],obj2[name]); 
		} else { 
			obj2[name]=obj1[name]; 
		}
	}	
	return obj2; 
}
json2=copy(json1,json2); 
json1.arr1.push(6); 
alert(json1.arr1); 
alert(json2.arr1); 
```