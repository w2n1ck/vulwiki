### PHPInfo()信息泄漏漏洞

**名称：**PHPInfo()信息泄漏漏洞

**描述：**Web站点的某些测试页面可能会使用到PHP的phpinfo()函数，会输出服务器的关键信息。如下图所示：
![](http://qzonestyle.gtimg.cn/qzone/vas/opensns/res/img/sec_hole_13.png)

**检测方法：**访问test.php以及phpinfo.php看是否成功。)

**修复方案：**删除该PHP文件。