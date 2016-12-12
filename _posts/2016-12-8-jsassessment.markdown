---
layout:     post
title:      "JS刷题总结"
subtitle:    "经典五十题"
date:       2016-12-12 18:46:00
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

3.apply()和call()方法  
call和apply都是为了动态改变this，当一个对象没有方法，其他对象有，用apply或call直接借助其他对象的方法操作，但两者还是有区别的，接收参数的方式不一样。
    
	var test = function(arg1,arg2){};
	test.call(this,arg1,arg2);
	test.apply(this,[arg1,arg2]);  
  
  

call是把参数按顺序传进去，apply是把参数放数组里面。展开讲很复杂，什么时候用call什么时候用apply呢，在给定对象参数的情况下如果参数形式是数组且对应一致，比如

	function people(age,name){
		this.age = age;
		this.name = name;
	};
	function student(age,name,grade){
		people.apply(this,arguments);
		this.grade = grade;
	};

	var s1 = new Student("xx","18","大一");  
  

此时console.log s1的age和name发现值已经赋过去了。如果people的参数是(name,age)此时应该用call,call需要把参数按顺序传递进去，people.call(this,name,age)。再详细一点说，当明确知道
参数数量时用call,不知道时用apply，把参数push进数组传递进去，也可以像我举的例子用arguments这个函数隐含参数直接传递所有的进去。apply还有好多其他用处，去百度逛了一圈总结一下：  
people里的是一个参数列表，但apply传递的是数组，在apply的过程中会将数组转换成参数列表，举个例子：  
	
	var max = Math.max(1,2,3);
	var max = Math.max.apply(null,[1,2,3]);	  
  

直接取出数组中最大值，超方便的嗷，顺便提一下为什么这里要传null进去：

	function test(){
		alert(this);
	}
	test.apply(null);//[object Window]  
  

其实max不需要this，传什么值都可以，只要不是未定义的变量名。看起来规范一点传了null,但主要想说用call还是apply大多数的时候传啥函数里就是啥，但传null或undefined时，js执行的是环境的全局变量。  
apply还可以应用在数组的push上，push本来只能push元素不能push数组，用了apply也很方便，只要目标函数需要参数列表而不接收数组的用apply都会省很多事，知乎上逛了一下，document.getElementsByTagName返回的是一个集合类似数组，但不能应用数组的push等方法，通过	  

	var domNodes = Array.prototype.slice.call(document.getElementsByTagName("*");
  
    
可以应用Array的方法。