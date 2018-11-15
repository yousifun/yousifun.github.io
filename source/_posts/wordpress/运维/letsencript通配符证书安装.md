---
title: letsencript通配符证书安装
date: 2018年11月15日14:51:01
categories:
- 运维
tags:
- SSL
- https
- SSL证书
---

什么是 Let’s Encrypt？部署 HTTPS 网站的时候需要证书，证书由 CA 机构签发，大部分传统 CA 机构签发证书是需要收费的，这不利于推动 HTTPS 协议的使用。Let’s Encrypt 也是一个 CA 机构，但这个 CA 机构是免费的！！！也就是说签发证书不需要任何费用。

![](https://ws1.sinaimg.cn/large/007cqnI0gy1fx8r2wr40xj30jz0d10t6.jpg)

Let’s Encrypt 由于是非盈利性的组织，需要控制开支，他们搞了一个非常有创意的事情，设计了一个 ACME 协议，
那为什么要创建 ACME 协议呢，传统的 CA 机构是人工受理证书申请、证书更新、证书撤销，完全是手动处理的。而 ACME 协议规范化了证书申请、更新、撤销等流程，只要一个客户端实现了该协议的功能，通过客户端就可以向 Let’s Encrypt 申请证书，也就是说 Let’s Encrypt CA 完全是自动化操作的。

任何人都可以基于 ACME 协议实现一个客户端，官方推荐的客户端是Certbot 。

### linux中下载
```cmd
wget https://dl.eff.org/certbot-auto
```
### 设为可执行权限
```
chmod u+x certbot-auto
```
### 配置通配符域名
```
// 把下面的xxx替换为域名和邮箱就OK
./certbot-auto certonly --email xxx@gmail.com -d "*.xxx" -d "xxx" --manual --preferred-challenges dns-01  --server https://acme-v02.api.letsencrypt.org/directory
```
配置的时候需要在域名服务商那里添加DNS解析，一般都是添加2个。大概就和下面差不多，添加`_acme-challenge.xxx`解析：

```
Please deploy a DNS TXT record under the name
_acme-challenge.xxx with the following value:

YOagZwESm8zr2H70R26HDxsasnGbmKCQmA-RFmJFc6p8

Before continuing, verify the record is deployed.

Please deploy a DNS TXT record under the name
_acme-challenge.xxxx with the following value:


pSP_gr54AUdsfsafXlEvHeuEByLCaJuWtD_s6Nh8
_cFspEuETApARlMpntn35tpIVaEoOzmErTwU1341g2k
Before continuing, verify the record is deployed.
```
