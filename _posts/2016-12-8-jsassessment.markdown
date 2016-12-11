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
>啊啊啊我果然不适合学计算机。
## Array
1.熟悉Array对象方法，常见的push,pop,sort,splice,shift,join,concat,toString等方法。
## 作用域
1.全局变量和局部变量  

    var a = 1;  
    function test(){
	  alert(a);
	  a = 2;
	  alert(a);
	  var a;
	  alert(a);
	}
	test();
	alert(a);
1，2，2，1初学者应该是这样，js的作用域与其他语言相比有很多不同。实际上第一个alert是underfined。  
js在执行前会对所有声明的部分完整分析，确定变量的作用域。第一个alert是underfined，这里的a不是全局变量，在函数体内声明了var a，全局变量a被覆盖了，在test执行前，这个a指向的就是var a,但执行到第一个alert时此时a并没有被赋值，所以是underfined。  
第二个alert是2，此时还是局部变量，第三个alert还是2，之前已经赋值2给a了。最后一个alert是1，这里的a不在函数体内，a为全局变量。  
  
2.划分标准  
js以方法块划分function｛｝，for while if 不是作用域的划分标准。  
	  
	function test(){
	  alert(a);
	  for(var a = 0;a < 3;a++){
	    alert(a);
	  }
	  alert(a);
	}
	alert(a);
	test();
这段程序直接报错退出，倒数第二行Uncaught ReferenceError: a is not defined。去掉后执行test函数,第一个alert是underfined，这个是未赋值，上面提到的是未定义，第二个alert一次0，1，2，第三个alert却仍然是2，即使退出了for循环但a的值仍然保存着。