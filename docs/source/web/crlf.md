## HTTP消息头注入漏洞

### **漏洞描述：**

用户控制的数据以不安全的方式插入到应用程序返回的HTTP消息头中，如果攻击者能够在消息头中注入换行符，就能在响应中插入其他HTTP消息头，并在响应主体中写入任意内容。

### 漏洞检测**：**

通过修改参数来判断是否存在漏洞。比如国内某著名网站曾经出现过header注入漏洞，如下url：

> [http://www.YYYYYYYYY.com/YYYYWeb/jsp/website/agentInvoke.jsp?agentid=%0D%0AX-foo:%20bar](http://www.yyyyyyyyy.com/YYYYWeb/jsp/website/agentInvoke.jsp?agentid= X-foo: bar)

抓包时发现：

![Header\_insertion.jpg](http://qzonestyle.gtimg.cn/qzonestyle/qzone_app/qzone_dev/modWiki/Header_insertion.jpg)

### **漏洞危害：**

利用HTTP消息头注入漏洞可以控制用户访问页面的返回结果,执行恶意代码。

### **修复建议：**

1.不要把用户控制的输入插入到应用程序返回的HTTP消息头中;

2.部署Web应用防火墙。

1. 在设置HTTP响应头的代码中，过滤回车换行（%0d%0a、%0D%0A)字符。
2. 不采用有漏洞版本的apache服务器，同时对参数做合法性校验以及长度限制，谨慎的根据用户所传入参数做http返回包的header设置。