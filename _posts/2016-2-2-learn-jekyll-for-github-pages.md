---
layout:     post
title:      "采用jekyll搭建我的博客"
subtitle:   ""
date:       2016-02-02
author:     "cheekahao"
header-img: ""
tags:
    - 学习
    - github
    - jekyll

---



今天学习了怎么用jekyll在github pages上搭建个人博客，主要包括本地ruby开发环境的搭建、jekyll的安装，jekyll-bootstrap的使用，遇到了些小坑，记录下，以备后面查询。

搭建过程主要参考：[http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html](http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html)和[http://beiyuu.com/github-pages/](http://beiyuu.com/github-pages/)

安装过程中的小问题

1. 下载RubyInstaller后，需要默认选择添加环境变量，否则后面手动配置会特别麻烦。
2. win环境下，需要安装DevKit才能安装jekyll，linux则不需要。
3. fork下jekyll-bootstrap之后，需要修改_config.yml里的模板路径ASSET_PATH，否则会找不到css，还有最好将jquery改为本地或者百度的cdn，毕竟google在我天朝访问受限。