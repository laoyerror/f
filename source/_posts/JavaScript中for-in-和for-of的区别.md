---
title: JavaScript中for in 和for of的区别
tags:
  - JavaScript
  - 代码
index_img: 'https://cdn.staticaly.com/gh/yeyulingfeng01/hexo@main/assets/cover/2022/20201117b.jpg'
categories: Web前端
abbrlink: 2e4a4aec
date: 2020-11-17 15:57:13
---

对数组的遍历大家最常用的就是for循环，ES5的话也可以使用forEach，ES5具有遍历数组功能的还有map、filter、some、every、reduce、reduceRight等，只不过他们的返回结果不一样。但是使用foreach遍历数组的话，使用break不能中断循环，使用return也不能返回到外层函数。

## 区别

for in遍历的是数组的索引（即键名），而for of遍历的是数组元素值。 所以for in更适合遍历对象，不要使用for in遍历数组。

那么接下来我们一起看一下for in 和for of 的区别吧。

## for in

``` bash
//for in 应用于数组
Array.prototype.sayHello = function(){
    console.log("Hello")
}
Array.prototype.str = 'world';
var myArray = [1,2,10,30,100];
myArray.name='数组';

for(let index in myArray){
    console.log(index);
}
//输出结果如下
0,1,2,3,4,name,str,sayHello

//for in  应用于对象中
Object.prototype.sayHello = function(){
    console.log('Hello');
}
Obeject.prototype.str = 'World';
var myObject = {name:'zhangsan',age:100};

for(let index in myObject){
    console.log(index);
}
//输出结果
name,age,str,sayHello
//首先输出的是对象的属性名，再是对象原型中的属性和方法，
//如果不想让其输出原型中的属性和方法，可以使用hasOwnProperty方法进行过滤
for(let index in myObject){
    if(myObject.hasOwnProperty(index)){
        console.log(index)
    }
}
//输出结果为
name,age
//你也可以用Object.keys()方法获取所有的自身可枚举属性组成的数组。
Object.keys(myObject)
```

可以看出for in 应用于数组循环返回的是数组的下标和数组的属性和原型上的方法和属性，而for in应用于对象循环返回的是对象的属性名和原型中的方法和属性。

使用for in 也可以遍历数组，但是会存在以下问题：

1.index索引为字符串型数字，不能直接进行几何运算

2.遍历顺序有可能不是按照实际数组的内部顺序

3.使用for in会遍历数组所有的可枚举属性，包括原型。例如上栗的原型方法method和name属性

## for of 

``` bash
Object.prototype.sayHello = function(){
    console.log('Hello');
}
var myObject = {
    name:'zhangsan',
    age:10
}

for(let key of myObject){
    consoloe.log(key);
}
//输出结果
//typeError

Array.prototype.sayHello = function(){
    console.log("Hello");
}
var myArray = [1,200,3,400,100];
for(let key of myArray){
    console.log(key);
}
//输出结果
1,200,3,400,100
```

## 来源：

<p class="note note-primary">https://juejin.im/post/6844903601261772808</p>

