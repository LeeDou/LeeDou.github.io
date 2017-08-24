---
title: 深复制与浅复制
date: 2017-08-23 17:35:46
tags:
---

## 基本数据类型和对象类型
 - Number、String、Boolean、Null、Undefined 对于这五种基本数据类型在存储时会在栈内存中为其开辟存储空间，直接存值。
 - 对于引用类型，在声明时会为在栈中存储指向堆内存的指针，在堆内存中为其开辟存储空间。
 - 栈内存只会以键值对的方式来存储数据，引用类型会按需在堆中开辟空间进行存储。

## js 中的浅复制
 基本类型都是键值的形式存储在栈中，故不存在深（浅）复制，只是普通的赋值运算。
 对于引用类型，声明一个对象时就为其在堆中开辟了内存空间，当声明另一个对像引用指向当前对象就产生了浅复制。
 ```
 var obj = {age:'20',name:'lee'}; // 创建一个对象
 var a = obj; // a将指向obj指向的堆中地址
 a.age = 18; // 修改age
 cosole.age; // 18
 ```
 在浅复制中，因为引用指向的是同一个地址，故但我们改变`a.age`的值的时候就改变了在堆内存中age的值，因obj也指向同一地址，故`obj.age`的值也会是18。
 > 浅复制是引用的复制，不会重新开辟新的内存空间。

 ## 深复制
 深复制是将原对象所用属性值重新开辟块内存空间进行保存。
 ### 数组的复制方法
 concat、slice 这两种方法会创建元数组的副本，对于数组元素全为基本类型的数组对象可以用这种方式进行复制，他会开辟新的内存空间，不会存在指向元数组的引用。
 ```
 var arr = [1, boolean, 'hello'];
 var narr = arr;  // [1, boolean, 'hello'];
 ```
 在es6中新增的Array.from方法也可以对数组进行复制，这种方式也是一种浅复制。
 ```
 var arr = [1, 'hello', {name:'lee'}];
 var narr = Array.from(arr); // [1, 'hello', {name:'lee'}]
 narr[2].name = 'kant'; 
 narr[2].name; // kant
 arr[2].name;  // kant
 arr.push([2]); // [1, 'hello', {name:'lee'}, [2]]
 narr;  // [1, 'hello', {name:'lee'}, [2]]
 ```

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