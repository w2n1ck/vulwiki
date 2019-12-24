## WebLogic远程部署漏洞

### 漏洞描述

weblogic是一个基于JavaEE构架的中间件，安装完weblogic默认会监听7001端口，可以用来远程部署网站代码。

### 漏洞验证

默认后台地址：

http://localhost:7001/console/login/loginForm.jsp

### 漏洞危害

可上传恶意木马文件，控制服务器

### 漏洞修复

删除远程部署页面