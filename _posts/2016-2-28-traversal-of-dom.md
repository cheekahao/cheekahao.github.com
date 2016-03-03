---
layout:     post
title:      "javascript学习笔记之 DOM遍历"
subtitle:   "jQuery的index()方法的简单实现与JavaScript的DOM遍历"
date:       2016-02-28
author:     "cheekahao"
header-img: ""
tags:
    - javascript
    - 学习笔记
    - dom
---




面试中被问到怎么用原生js实现jQuery的index()功能，即返回当前元素在兄弟元素中的索引值。

所以又复习了一遍jQuery的index()的实现原理和js的DOM遍历，收获良多。

关于jQuery的index()，本文自讨论返回当前元素索引值的情况，jQuery的实现为先判断当前元素及其父元素是否存在，若不存在则返回-1，否则返回prevAll()的length，具体代码如下：

```
jQuery.fn.extend({	
	// Determine the position of an element within the set
	index: function( elem ) {
		// No argument, return index in parent
		if ( !elem ) {
			return ( this[ 0 ] && this[ 0 ].parentNode ) ? this.first().prevAll().length : -1;
		}
		//其他代码……
	}
});
```

而jQuery的prevAll()方法则是对jQuery.dir()的进一步封装，用到了DOM的"previousSibling"属性，返回的是当前元素的前面所有兄弟节点的数组，具体代码如下：

```
jQuery.extend({
	dir: function( elem, dir, until ) {
		// dir = "previousSibling"
		var matched = [],
			truncate = until !== undefined;

		while ( (elem = elem[ dir ]) && elem.nodeType !== 9 ) {
			if ( elem.nodeType === 1 ) {
				if ( truncate && jQuery( elem ).is( until ) ) {
					break;
				}
				matched.push( elem );
			}
		}
		return matched;
	}
})
```

基于此，我想到了利用dom元素的previousSibling属性实现index()功能的方法，在这期间还是遇到了previousSibling和previousElementSibling的兼容性问题，ie8以下不支持previousElementSibling属性，而chrome等现代浏览器会回返回文本节点，网上查了好多办法都没有找到好的解决办法，最终只能靠判断nodeType解决，代码如下：

```
function index(dom){
	var index = 1;
		while((dom = dom.previousSibling) && dom.nodeType !== 9){
			if(dom.nodeType == 3) continue;
			index ++;
		}
		return index;
}
```

在查找过程中，还找到了另外两种解决办法，一种是给dom添加index属性，另外一种是利用闭包，现在回想起来，考官应该是在考查我应用闭包的能力，汗。。。

附上另外两种解决方式代码：

方式一：

```
function index(){
        var pNode = getElementsById(id),
            cNode = pNode[0].getElementsByTagName("li");
        for( var i=0; i < cNode.length; i++){
            cNode[i].index= i;
            cNode[i].onclick = function(){
                alert(this.index);
            }
        }
    }
```

方法二(闭包)：

```
function index(){
        var pNode = document.getElementsById(id),
            cNode = pNode.getElementsByTagName("li");
        for( var i=0; i < cNode.length; i++){
            (function(i){
            	cNode[i].onclick = function(){
                	alert(i + 1);
            	}
            })(i)            
        }
    }
```
