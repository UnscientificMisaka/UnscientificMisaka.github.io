---
layout:     post
title:      "JS刷题总结"
subtitle:    "经典五十题"
date:       2016-12-8 18:46:00
author:     "LRZ"
header-img: "img/16-12-8.jpg"
tags:
    - JavaScript
---
>第三题就跌落马下了，case通过率才百分之六十多，而且不知道问题出在哪，啊啊啊我果然不适合学计算机。
## Array
1.移除数组 arr 中的所有值与 item 相等的元素。不要直接修改数组 arr，结果返回新的数组<br>
两种方法：  

>Demo 01 直接push<br>
>反向思维，我果然很天真的先想到找到相等的删掉后将值赋给另一个数组(讲道理markdown的code每次换行换不了，有点郁闷，抽空研究一下这个标签的css)  
>fuction(arr,item){  
>  var arrNew = [];   
>  for(var i = 0;i<arr.length;i++){  
>    if(arr[i]!==item){  
>      arrNew.push(arr[i]);  
>    }    
>  }  
>  return arrNew;      
>      }  
>Demo 02 常规思路  
>function(arr,item){  
>var len = arr.length;  
>for(var i = 0;i<len;i++){  
>if(arr[i]==item){  
>arr.splice(i,1);  
>i--;  值
>len--;  
>}  
>}  
>return arrNew;  
>}
>  
>  这里有个小坑，删掉数组元素同时也得让整个数组长度减一，因为splice函数再删掉数组元素后数组值自动向前移。

2.日后更新