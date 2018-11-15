---
title: 配置sll评级为A+的网站配置
date: 2018年11月15日
categories:
- 运维
tags:
- SLL
- HTTPS
---

在网站安装了ssl证书后，如果网站还有资源使用http协议，那么chrome、firefox等浏览器会出现不安全的标志。
那么只要保证全站的图片等资源都是https协议的就可以保证浏览器不会报“不安全”标志了，并且可以增加网站在搜索引擎中的权重。
![](https://ws1.sinaimg.cn/large/007cqnI0gy1fx8pmo7ndfj30m804ajrv.jpg)

当网站全站开启https后，可以去网站[https://myssl.com/](https://myssl.com/)检测自己的SSL评测等级。一般只要配置得当，至少都是B，但是为了更好地配置符合规范的SSL，可以参照[https://cipherli.st/](https://cipherli.st/)进行配置。下面是评级很差的网站。
![](https://ws1.sinaimg.cn/large/007cqnI0gy1fx8prmeguyj30uc0fhta2.jpg)

### 下面是评级A+的网站

![](https://ws1.sinaimg.cn/large/007cqnI0gy1fx8psompqtj30sw0e3wf6.jpg)

下面是我的`apache2`中的配置，仅供参考。下面中的'xxxx'是网址或者路径，在配置的时候注意更换。
```xml
<VirtualHost *:443>
DocumentRoot "/var/www/xxx"
ServerName xxxxx:443
ErrorLog logs/ssl_error_log
TransferLog logs/ssl_access_log
LogLevel warn
SSLEngine on
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLHonorCipherOrder On
Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header always set X-Frame-Options DENY
Header always set X-Content-Type-Options nosniff
SSLCertificateFile /etc/letsencrypt/live/xxxxx/cert.pem
SSLCertificateKeyFile /etc/letsencrypt/live/xxxxx/privkey.pem
SSLCertificateChainFile /etc/letsencrypt/live/xxxxx/chain.pem
<Files ~ "\.(cgi|shtml|phtml|php3?)$">
    SSLOptions +StdEnvVars
</Files>
<Directory "/var/www/xxxxx">
    SSLOptions +StdEnvVars
</Directory>

BrowserMatch "MSIE [2-5]" \
         nokeepalive ssl-unclean-shutdown \
         downgrade-1.0 force-response-1.0

CustomLog logs/ssl_request_log \
          "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"
</VirtualHost>
```
