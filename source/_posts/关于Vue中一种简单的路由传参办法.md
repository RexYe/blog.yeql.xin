---
title: 关于Vue中一种简单的路由传参办法
date: 2017-09-15 10:31:22
tags:
---

*情景模拟*：
>A页面中，有一些div是根据A中的book数据通过v-for生成的，比如item。
>并且点击会根据路由跳转到B页面。
>而跳转到B页面后，我需要A中的item。

````css
 <div v-for="(item,index) in book"  :class='{on:$route.path === `/${item.to}/`}' @click='toOther(item.to)'>
 </div>
````
````Javascript
toOther(to,run) {
   if(this.$route.path!==`/${to}`){
     location.hash = to;
   }
},
````

*解决办法*：

>在A中的click事件中将item传进toOther()函数中，再根据路由传入
````Javascript
toOther(to,run) {
      if(this.$route.path!==`/${to}`){
        location.hash = to+'?'+run.key;
      }
    },
````
>即将要传的参数添加在原本url加？之后，这样既不影响路由，也比较方便。 
                                                           如图1所示：

![图1.png](http://upload-images.jianshu.io/upload_images/2979086-86d879d45020551b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![图2.png](http://upload-images.jianshu.io/upload_images/2979086-164db17214543320.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>如图2，这样子我们便可以在 this.$route 的fullPath中拿到A中我们需要传递的参数了。
具体要拿还需要进行字符串的分割取出所需的信息，
但是这样子会很繁琐，
我们只需多加几个字，
>在你的参数前加上'sth'=

````Javascript
toOther(to,run) {
      if(this.$route.path!==`/${to}`){
        location.hash = to+'?'+'book_key='+run.key;
      }
    },
````
>你就会发现你可以在query中拿到这些个数据
>并且是一个object的形式
>简直不能更完美!

![图3.png](http://upload-images.jianshu.io/upload_images/2979086-8e3f381d4f8b0fe2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
