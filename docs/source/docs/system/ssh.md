# SSH Services Port 22 Enabled

### 漏洞等级

中危

### 漏洞描述

22号端口是linux服务器默认的远程登录管理端口，开放该端口可导致攻击者暴力破解服务器口令，若存在弱口令可直接被攻击者入侵。

### 漏洞危害

- 黑客可能通过22端口试图连接远程控制；
- 如果主机的管理员密码过于简单，黑客就可以利用该漏洞，通过一些工具破解管理员密码，进而控制服务器。

### 漏洞修复方案

- 建议利用组策略等方法关闭22端口。
- 部署防火墙拦截内网端口。