---
layout:     post
title:      "日常bug之safari页面放大"
subtitle:   "html，body的高度小于window高度时，页面放大的bug"
date:       2016-03-09
author:     "cheekahao"
header-img: ""
tags:
    - 日常bug
    - safari
    - 页面放大
---


测试发现一个页面，在iPhone的safari浏览器中，点击按钮弹窗后，页面放大，同样的逻辑在别的页面没有问题，却只在这个页面有问题。

在排除了双击放大，input获取焦点的问题后，仔细分析页面发现，这个页面的元素较小，导致html，body的高度小于window的高度，而在弹窗过程中有遮罩层，放大后遮罩层的高度为window高度。因此推测，可能是由于html和body的高度小于window的高度导致的，当弹窗后，将body的高度放大到了window的高度导致的。

因此，在base.css加了`html, body{min-height:100%;}`后解决了此问题。
