---
title: wordpress 下载模板、更新报错 No working transports found解决办法
date: 2018年11月15日15:53:41
categories:
- wordpress
tags:
- wordpress
- apache
---
出错原因是PHP没有开启curl.

windows下开启方法如下

1. 将php.ini中的;extension=php_curl.dll前的分号去掉，
2. 将php中libeay32.ll, ssleay32.dll, php_curl.dll，libssh2.dll移入windows/system32中，然后重启Apache服务器，问题解决

注： 网上很多答案都是放libeay32.ll, ssleay32.dll, php_curl.dll三个文件就够了，但是我尝试下来不行，还需要libssh2.dll
