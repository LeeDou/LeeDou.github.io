---
title: 判断一个对象的类型
date: 2017-08-18 16:32:27
tags:
---


```
var isType = function (type) {
	retrun function (obj) {
        return toString.call(obj) == '[object ' + type + ']';
    };
};
// 根据函数柯里化传参，以达到按需判断类型的目的
```
- 类型判断
```
var isString = isType('String');
var isFunction = isType('Function');
var isObject = isType('Object');
```
- 使用方式
```
var a = {};
isObject(a);
```