---
layout:     post
title:      "关于typeof运算符，以及null与undefined"
subtitle:   ""
date:       2016-02-17
author:     "cheekahao"
header-img: ""
tags:
    - javascript
    - 学习笔记
    - typeof
	- null
	- undefined
---

今天面试，遇到个面试题，答错了，回来查了下资料，记录下来已被后面查看。

题目如下：

```
var a = null;
alert(typeof a);
```

查看资料后，`typeof`的返回值可能有六种情况，`'number', 'boolean','string','function', 'object', 'undefined'`。

而null是JavaScript中表示空置的特殊对象，因此返回'object'。而另外一个特殊的对象Array返回的也是'object'。

而NaN、Infinity等表示特殊数字的返回值的是'number'。

而eval、Date等内置函数，返回的是'function'。

在翻阅直接null与undefined的区别是，又学习了。

null是JavaScript的表示空值的特殊对象，而undefined不是关键字，而是预定义的*全局变量*，在ECMAScript 3中是*可读写*的，可以给他赋予任意值，在ECMAScript 5中才被改为只读的。



