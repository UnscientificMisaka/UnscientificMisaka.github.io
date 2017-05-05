---
layout:     post
title:      "参数解构"
subtitle:   "..."
date:       2017-05-05
author:     "LRZ"
header-img: "img/17-4-5.jpg"
tags:
    - ES6
---

## Vue中用到的一些参数解构

> 最近刚开始干一票Vue的活，看文档发现了一些ES6解构这块的特性随手记录一下

1. 看到Vuex官方Exapmle中的计数器代码时	
 
	``` 	
	const actions = {
		increment: ({ commit }) => commit('increment'),
		decrement: ({ commit }) => commit('decrement'),
		incrementIfOdd ({ commit, state }) {
		    if ((state.count + 1) % 2 === 0) {
		      commit('increment')
		    }
  		},
		incrementAsync ({ commit }) {
			return new Promise((resolve, reject) => {
			  setTimeout(() => {
			    commit('increment')
			    resolve()
			  }, 1000)
			})
		}
	}	
	```

  
刚看到incremnetIfOdd就懵了，这特喵的不是在对象中吗，怎么啥都不写，随手控制台写了个例子，incrementIfOdd默认被转为incrementIfOdd： function incremnetIfOdd(){},窃以为javascript的灵活是由于它的不严谨导致的，不过扯远了这好像不是es6的特性。  

2. 然后走到注册action时有点小害怕
	
	``` 	
 	actions: {
    	increment (context) {
      	context.commit('increment')
    }

	actions: {
 		increment ({ commit }) {
    	commit('increment')
  	}
	``` 	

怎么可以这样写呢，赶紧翻出了阮老师的primer看了一圈，控制台写个例子跑一下：  
  
	var context = {
		commit(param){
			console.log(param);
		}
	}
	
	var a = {
		increment (context){
			context.commit('increment')
		}
	};
	
	var b = {
		increment ({ commit }){
			commit('increment')
		}
	}
	
	a.increment(context) // increment
	b.increment(context) //	increment

我是这样理解的，commit原始被解析成commit:commit ，然后context传进来解构为commit:context.commit,所以接下来的commit是对象中的key调用的是value:context.commit,理解可能有点出入，感觉到了chromeV8引擎的咆哮。