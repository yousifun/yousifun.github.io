---
title: centos7安装wordpress
date: 2018年11月15日15:53:41
categories:
- wordpress
tags:
- wordpress
- apache
---

```
wget https://cn.wordpress.org/wordpress-4.9.4-zh_CN.zip   //下载
unzip wordpress-4.9.4-zh_CN.zip    //解压
cp -r wordpress/* /var/www/html/      //将wordprss下所有的文件复制到apache服务器下的根目录
yum -y install ftp vsftpd
cp -r wordpress /var/www/html/yousifun
```
