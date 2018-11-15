---
title: centos7修改apache2目录权限和默认跟目录
date: 2018年11月15日15:53:41
categories:
- wordpress
tags:
- wordpress
- apache
---
一台新的linux CentOS服务器,安装好php环境后，发现apache默认解析路径是`/var/www/html`,如果不想使用这个默认路径，可以自己设置一个目录。例：在根目录下新建`/data/website`文件夹用来存放项目。
**准备工作**：创建目录在根目录下
```
mkdir data
cd data
mkdir website
```
操作步骤：
```
vi /etc/httpd/conf/httpd.conf
```
找到 DocumentRoot /var/www/html 这一段 apache 的根目录,把/var/www/html 这个目录改为/data/website,再找到定义apache /var/www/html这个区域,把 /var/www/html改成/data/website,这样我们就把apahce的默认路径改掉了

```
service httpd restart #重启Apache服务器
```
访问localhost的时候，会发现访问拒绝，这是为什么呢？主要是因为你的/home/wwwroot/web1/htdocs的权限是750，apache这个用户没有权限访问，你需要更改掉权限，可以这样改！
```
chmod -R 755 /data/website
```
然后去访问 发现正常运行了（apache的用户：apache 运行apache的组：apache）至此，Apache默认网站目录更改成功。然后把你的项目移到配置好的目录下即可。
Apache怎样设置主目录的路径：
在apache目录的`conf/httpd.conf`文件中查找`DocumentRoot`，将`DocumentRoot`后面的路径修改为你想要的路径，应该有两处。

**更改Apache的默认网站根目录地址方法如下**：
1. 找到 DocumentRoot “X:/Apache/htdocs”  将“X:/Apache/htdocs”改为你自定义的网站目录；
2. 找到 <Directory “X:/Apache/htdocs”> 将“X:/Apache/htdocs”改为你自定义的网站目录;
3. 完成。

注意：X代表实际的安装盘符目录。
