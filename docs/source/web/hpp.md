# HPP漏洞

#### **漏洞描述**

即http参数污染，它是web容器处理http参数时的问题。

比如访问URL:http://www.xxx.com/index.php?str=hello此时，页面显示hello。但如果访问:http://www.xxx.com/index.php?str=hello&str=world&str=nmask此时，页面显示nmask，把前面参数的值给覆盖了，这就是http参数污染。

#### **可带来的危害：**

用来绕过WAF

#### **修复建议：**

1.修改web容器处理机制