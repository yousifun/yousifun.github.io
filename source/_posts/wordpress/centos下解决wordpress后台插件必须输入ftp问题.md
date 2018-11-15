---
title: centos下解决wordpress后台插件必须输入ftp问题
date: 2018年11月15日15:53:41
categories:
- wordpress
tags:
- wordpress
- apache
---
`/etc/httpd/conf/httpd.conf`默认的情况下是用户名及用户组分别是Apache，

在安装wordpress到/var/www/http的时候，会发现文件夹下面的用户名及用户组分别是root。 这样 看来 还是权限的问题~ WP网站要正常运行必须是 http.conf 中制定的用户和用户组 。

好了明白了这个道理我们只需要执行如下命令即可完美解决
```
chown -R apache:apache /var/www/html
chown -R apache:apache /var/www/html
```
这样问题就得以解决了，wordpress后台再也不需要输入ftp名了。


当你的wordpress遇到以下问题时：
1. 不能上传图片
2. 不能自动安装主题、插件（需要FTP账户）
3. 不能自动更新
4. 其它任何需要wordpress写文件的问题

这些问题基本都是一个原因，你的wordpress目录不属于当前的用户和组，即web访问的用户没有权限操作wp的一切需要写权限的操作，其实就是linux下权限不足，无法写入造成的。
**解决方法：**
首先需要你有root权限，SSH登录，进入到wp的安装目录：
```
cd /var/www/html/my_wp_blog
```
给予所有的写权限：
```
chmod 777 wp-content
```
接下来给你的博客的文章上传一张图片，WP会生成一个目录，然后查看是哪个用户创建了文件夹。一般情况下，这个用户名叫“apache”，也有不少人发现这个用户是“nobody”.
进入到 wp 的`wp-content`目录，查看该目录下所有文件/文件夹的权限，所属用户、用户组：
```
cd wp-content
ls -l
total 16
-rw-r–r– 1 root root   30 May  4  2007 index.php
drwxr-xr-x 3 root root 4096 Feb 10 19:31 plugins
drwxr-xr-x 5 root root 4096 Mar 23 03:04 themes
drwxrwxrwx 3 www www 4096 Mar 24 02:08 uploads
```
注意上传目录 `uploads` 是用户 www 创建的。
接下来把`wp-content`权限还原到 755：:
```
cd ..
chmod 755 wp-content
##下来就是实际修复的命令了，改变wp所在文件夹的拥有者为刚找到的这个用户www：
cd ..
chown -R www:www my_wp_blog
```
