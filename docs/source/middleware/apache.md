## Apache解析漏洞

### 漏洞描述

Apache 解析文件的规则是从右到左开始判断解析,如果后缀名为不可识别文件解析,就再往左判断。比如 test.php.owf.rar “.owf”和”.rar” 这两种后缀是apache不可识别解析,apache就会把wooyun.php.owf.rar解析成php

### 漏洞检测

本地访问http://localhost/test.php.nmask，是否能被解析成php，若能则存在此漏洞。

### 漏洞危害

配置文件上传漏洞，可绕过waf／黑名单等限制，上传木马文件，控制服务器。

### 漏洞修复

1.apache配置文件，禁止.php.这样的文件执行，配置文件里面加入

```
<Files ~ “.(php.|php3.)”>
        Order Allow,Deny
        Deny from all
</Files>
```

2.用伪静态能解决这个问题，重写类似.php.*这类文件，打开apache的httpd.conf找到LoadModule rewrite_module modules/mod_rewrite.so把#号去掉，重启apache,在网站根目录下建立.htaccess文件,代码如下:

```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteRule .(php.|php3.) /index.php
RewriteRule .(pHp.|pHp3.) /index.php
RewriteRule .(phP.|phP3.) /index.php
RewriteRule .(Php.|Php3.) /index.php
RewriteRule .(PHp.|PHp3.) /index.php
RewriteRule .(PhP.|PhP3.) /index.php
RewriteRule .(pHP.|pHP3.) /index.php
RewriteRule .(PHP.|PHP3.) /index.php
</IfModule>
```