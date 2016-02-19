---
layout:     post
title:      "解决input的display:inline时也无法换行的问题"
subtitle:   ""
date:       2016-02-17
author:     "cheekahao"
header-img: ""
tags:
    - input
    - css
    - html
---

为了移动端更好的复制剪切文本，将优化原来的一个p标签。原内容为：

```
<p>卡密:0000-8DCE-4E28-AC28</p>
```

第一个方案是用一个readonly的input来显示卡密的内容。实际操作后，发现即使input设置display：inline之后依然无法换行，因为input本来就是单行文本，尴尬。。。
后采用textarea来替代input，依然无法想span之类的行内元素一样的表现。
最后的解决方案是用一个span包裹卡密文案，textarea包裹卡密内容，并将两个全部都position:abolute，并规定外层p标签的高度，及overflow：hidden，因为如果不加的话，textarea会出现滚动条。
最后的html为

```
<p class="jd_card">
	<span class="card_name">卡密:</span>
	<textarea name="JDcard" readonly="readonly">0000-8DCE-4E28-AC28</textarea>
</p>
```

相应的css样式为：

```
.jd_card{overflow: hidden;height: 43px;}
.jd_card textarea{position: absolute;padding: 0;outline: none;border: none;display: inline;text-indent: 30px;}
.jd_card .card_name{position: absolute;z-index: 2;}
```

