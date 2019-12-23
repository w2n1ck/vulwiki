# 跨站脚本漏洞

即XSS漏洞，利用跨站脚本漏洞可以在网站中插入任意代码，它能够获取网站管理员或普通用户的cookie，隐蔽运行网页木马，甚至格式化浏览者的硬盘。

### **漏洞危害：**

1. 网络钓鱼，盗取管理员或用户帐号和隐私信息等；
2. 劫持合法用户会话，利用管理员身份进行恶意操作，篡改页面内容、进一步渗透网站；
3. 网页挂马、传播跨站脚本蠕虫等；
4. 控制受害者机器向其他系统发起攻击。

### **修复建议：**

#### 设置httponly

httponly无法完全的防御xss漏洞，它只是规定了不能使用js去获取cookie的内容，因此它只能防御利用xss进行cookie劫持的问题。Httponly是在set-cookie时标记的，可对单独某个参数标记也可对全部参数标记。由于设置httponly的方法比较简单，使用也很灵活，并且对防御cookie劫持非常有用，因此已经渐渐成为一种默认的标准。

#### xss filter

Xss filter往往是一个文本文件，里面包含了允许被用户输入提交的字符（也有些是包含不允许用户提交的字符）。它检测的点在于用户输入的时候，xss filter分为白名单与黑名单，推荐使用白名单，但即使使用白名单还是无法完全杜绝xss问题，并且使用不当可能会带来很高的误报率。

#### 编码转义

编码方式有很多，比如html编码、url编码、16进制编码、javascript编码等。
在处理用户输入时，除了用xss filter的方式过滤一些敏感字符外，还需要配合编码，将一些敏感字符通过编码的方式改变原来的样子，从而不能被浏览器当成js代码执行。

#### 处理富文本

有些网页编辑器允许用户提交一些自定义的html代码，称之为”富文本”。想要在富文本处防御xss漏洞，最简单有效的方式就是控制用户能使用的标签，限制为只能使用*a、div*等安全的标签。

#### 处理所有输出类型的xss漏洞

xss漏洞本质上是一种html注入，也就是将html代码注入到网页中。那么其防御的根本就是在将用户提交的代码显示到页面上时做好一系列的过滤与转义。

### 其他**修复方案**

##### 1. 开发者应该严格按照[openid和openkey的校验规则](http://wiki.open.qq.com/wiki/概念和术语#2.1_OpenID)判断openid和openkey是否合法，且判断其它参数的合法性，不合法不返回任何内容。

##### 2. 严格限制URL参数输入值的格式，不能包含不必要的特殊字符（ %0d、%0a、%0D 、%0A 等）。

##### 3. 针对ASP.NET的防XSS库，Microsoft有提供统一的库，具体可以参见如下链接 微软官网：http://msdn.microsoft.com/en-us/library/aa973813.aspx

##### 4. 具体的js方法如下：

##### （1）对于用户输入的参数值展现在HTML正文中或者属性值中的情况，例如：

> ##### 展现在html正文中：<a href='[http://www.contoso.com'>Un-trusted](http://www.contoso.com'>un-trusted/) input</a> 展现在属性值中：
>
> ##### <input name="searchword" value="Un-trusted input"> 此时需要将红色的不可信内容中做如下的转码(即将<> ‘ “ ` 转成html实体)： ![sec\_hole\_10.png](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/sec_hole_10.png)

##### （2）对于用户输入落在<script>的内容中的情况，例如:

> ##### <script type="text/javascript"> … var mymsg="Un-trusted input"; var uin=Un-trusted input; … </script>
>
> ##### ![sec\_hole\_11.png](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/sec_hole_11.png)

# 未过滤HTML代码漏洞

由于页面未过滤HTML代码，攻击者可通过精心构造XSS代码（或绕过防火墙防护策略），实现跨站脚本攻击等。

**可带来如下危害：**

1. 恶意用户可以使用JavaScript、VBScript、ActiveX、HTML语言甚至Flash利用应用的漏洞，从而获取其他用户信息；
2. 攻击者能盗取会话cookie、获取账户、模拟其他用户身份，甚至可以修改网页呈现给其他用户的内容。

**修复建议：**

1. 严格过滤用户输入的数据。
2. 参考跨站脚本漏洞修复方案。