---
title: apache2 启动一闪而过问题
date: 2018年11月15日15:53:41
categories:
- wordpress
tags:
- wordpress
- apache
---

1.  配置文件错误
    仔细检查配置文件中的各个参数。
2.  IIS占用端口
    如果 windows 中启动了 IIS，那么会占用默认端口80，此时只要更改 IIS 的端口或者更改 apache 的端口都可以。
