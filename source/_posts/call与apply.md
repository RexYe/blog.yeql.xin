---
layout: w
title: call与apply
date: 2017-10-12 18:43:59
tags: Javascript
---
## call与apply
两者的功能大致一样

均是为了动态改变this，当一个object没有某个方法，但是其他的有，我们可以借助call或apply用其它对象的方法来操作。

具体例子如下：

````Javascript
function add(a,b){
    return a+b;
}

function sub(a,b){
    return a*b;
}
add.call(sub,3,8);
add.apply(sub,[4,9]);
````
sub函数中没有加法，此时利用call或者apply即可"借"到add中的加法。

实现对象继承的例子如下：
````Javascript
var Father = function() {
    this.FamilyName = 'Ye';
}
var Son = {};
Father.call(Son);
Father.apply(Son);
````

实现多重继承的例子如下：
````Javascript
function Class1()  
{  
    this.showSub = function(a,b)  
    {  
        console.log(a-b);  
    }  
}  
function Class2()  
{  
    this.showAdd = function(a,b)  
    {  
        console.log(a+b);  
    }  
}  
function Class3()  
{  
    Class1.call(this);
      
    Class2.call(this);  
} 
var result = new Class3;
result.showSub(7,2);//5
result.showAdd(7,2);//9
````

#### *区别* 在于接受参数形式不同
> call 接受连续参数

> apply 最多两个参数，且第二个参数仅接受数组参数或者arguments对象
