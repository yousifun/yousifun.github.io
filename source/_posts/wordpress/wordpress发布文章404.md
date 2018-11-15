---
title: wordpress发布文章404
date: 2018年11月15日15:53:41
categories:
- wordpress
tags:
- wordpress
- apache
---
wordpress固定链接最好包含标题名称实现seo;

wordpress不能发布带有中文题目的文章，这里采用的是wp_slug_translate插件自动翻译题目；

这样还是不行的，需要提供修改注册文件的权限，在httpd.conf中修改：

AllowOverride 的None改成All

同时查询mod_rewrite.so，把前面的#去掉应该就可以了。
