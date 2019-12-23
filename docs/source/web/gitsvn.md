# SVN源代码泄漏

由于目标网站没有及时清除SVN服务器连接时的残留信息，导致存在此漏洞。

**可带来如下危害：**

1. 攻击者可利用该漏洞下载网站的源代码，获得数据库的连接密码等敏感信息；
2. 攻击者可通过源代码分析出新的系统漏洞，从而进一步入侵系统。

**修复建议：**

1. 删除指定SVN生成的各种文件，如“/.svn/entries”等。

# CVS 信息泄漏

### 漏洞描述

由于目标网站没有及时清除CVS服务器连接时的残留信息，导致存在此漏洞。

### 漏洞测试

访问／cvs/等页面，若出现下图内容，则表示存在此漏洞。

![img](data:image/png;base64,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)

@前面是用户名 后面是服务器地址

### 漏洞危害

- 攻击者可利用该漏洞下载网站的源代码，获得数据库的连接密码等敏感信息；
- 攻击者可通过源代码分析出新的系统漏洞，从而进一步入侵系统。

### 修复建议

删除指定CVS生成的各种文件，如“/CVS/Root”等。

## Git源代码泄露漏洞

### 漏洞描述

服务器将.git文件放在了web目录下，导致可以访问git文件内容，获取源代码。

### 漏洞验证

验证访问网站.git目录：

![img](https://nmask.gitbooks.io/vulnerability-box/assets/import.png)

可以看到git目录可以被访问，即存在此漏洞。

### 漏洞危害

可以通过此漏洞，获取项目源代码。

### 漏洞修复

1.删除网站目录下的.git文件

2.中间件上设置.git目录访问权限，禁止访问

3.防火墙上设置禁止访问此目录