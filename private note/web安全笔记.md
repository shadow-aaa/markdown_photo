## 第一天-基础入门

### 1.域名

最右边的字符组称为顶级域名或一级域名、倒数第二组称为二级域名、倒数第三组称为三级域名、以此类推。顶级域名又分为三类：一是国家和地区顶级域名，200多个国家都按照ISO3166国家代码分配了顶级域名，例如中国是.cn，日本是.jp等；二是通用顶级域名例如表示工商企业的.com，表示网络提供商的 .net，表示非盈利组织的 .org等。三是新顶级域名如通用的.xyz、代表“高端”的.top、代表“红色”的.red、代表“人”的.ren等一千多种。

三级域名:二级域名的子域名,特征是包含三个“.”,例如___.___.baidu.com...

形如：china.world.com/beijing，采取目录形式并且以“/”代替“.”的不能够称为三级域名，甚至不能称为域名，一般称之为域名下的“二级目录”。

**多级域名可以使用谷歌语法探测旁站**

### 2.DNS

DNS:域名和IP地址互相转换的解析服务器

<img src="https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/8b9be752584806d1e8384ade23a257a3.76sabo6bh240.webp" alt="8b9be752584806d1e8384ade23a257a3" style="zoom:50%;" />

<br/>

HOSTS:定义IP地址和主机名的映射关系，是一个映射IP地址和主机名的规定。

系统先向host询问域名对应IP地址,然后先dns询问

<br/>

CDN:CDN的全称是Content DeliveryNetwork，即内容分发网络。

CDN的基本思路：是尽可能避开互联网上有可能影响数据传输速度和稳定性的瓶颈和环节，使内容传输的更快、更稳定。

**如果网站有使用CDN技术,那么我们ping的话就不是源站地址而是cdn地址**

### 3.web

中间件(搭建平台):apache,iis,tomcat,nginx

数据库:access mysql mssql oracle sybass db2 postsql

![c496e75fd96388bd87adfe1f62ba4c91](https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/c496e75fd96388bd87adfe1f62ba4c91.18qhrzfcoo5c.webp)

**多级域名查找有软件**,以后记得下,layer子域名挖掘机

## 第二天-数据包拓展

### 1.http/https数据包

- http特点

`http协议支持客户端/服务端模式，也是一种请求/响应模式的协议。`

`简单快速：客户向服务器请求服务时，只需传送请求方法和路径。请求方法常用的有GET、HEAD、POST。`

`灵活：HTTP允许传输任意类型的数据对象。传输的类型由Content-Type加以标记。`

`无连接：限制每次连接只处理一个请求。服务器处理完请求，并收到客户的应答后，即断开连接，但是却不利于客户端与服务器保持会话连接，为了弥补这种不足，产生了两项记录http状态的技术，一个叫做Cookie,一个叫做Session。`

`无状态：无状态是指协议对于事务处理没有记忆，后续处理需要前面的信息，则必须重传。`

- URI和URL的区别

`URI 是用来标示 一个具体的资源的，我们可以通过 URI 知道一个资源是什么。`

`URL 则是用来定位具体的资源的，标示了一个具体的资源位置。互联网上的每个文件都有一个唯一的URL`

- 常见请求方法

`GET:请求指定的页面信息，并返回实体主体。`
`POST:向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。`
`HEAD:类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头`
`PUT:从客户端向服务器传送的数据取代指定的文档的内容。`
`DELETE:请求服务器删除指定的页面。`

- post和get区别:

`都包含请求头请求行，post多了请求body。`
`get多用来查询，请求参数放在url中，不会对服务器上的内容产生作用。post用来提交，如把账号密码放入body中。`
`GET是直接添加到URL后面的，直接就可以在URL中看到内容，而POST是放在报文内部的`
`GET提交的数据长度是有限制的，因为URL长度有限制，**具体的长度限制视浏览器而定**。而POST没有。`

http响应码:

2xx:成功

3xx:重定向

4xx:客户端错误

5xx:服务器错误

**200存在文件 403存在文件夹 3xx均可能存在 404都不存在 500均可能存在**

http和https使用连接方式不同，默认端口也不一样，http是80，https是443。

## 第三天-搭建安全拓展

- 基于中间件的简要识别
一般可以通过抓包的方式分析出是什么类型的服务器和中间件

- 基于中间件的安全漏洞
可以根据在第一步上面收集到的信息、去找Apache的漏洞和PHP的漏洞

- 基于中间件的靶场使用
https://vulhub.org/#/environments/
这个是用docker搭建的一个靶场非常的方便

x.php.jpeg

```
[root@hdss7-11 ~]# cat x.php.jpeg
<?php
       phpinfo();
?>
```

## 第四天-web源码拓展

**源码功能决定漏洞类型**

<img src="https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/1ea340df6198356a5e4fc705cf33e0f5.364tk09q7yg0.webp" alt="1ea340df6198356a5e4fc705cf33e0f5" style="zoom:50%;" />

**框架或非框架：**如果对方网站采用的是框架开发的话，那么你面对的就是寻找框架的漏洞，如果是非框架的话寻找的漏洞，那么针对的就是代码写出来的漏洞

**CMS识别:**搭建不同类型的网站都有不同的框架源码,这些源码可以用来漏洞分析.CMS识别是指如何判定一个网站是用什么程序搭建的，可以**人工,工具,平台**识别,知道后，就可以在网站上下载源码，进行漏洞分析。也有可能别人发现了这个漏洞，并且发到网上去，那么就可以利用别人发现的漏洞对网站进行攻克.

**源码获取：**1、扫描备份文件，因为他网站可能会数据备份，所以可以扫描它的备份文件并下载从而获取源码。2、通过名字去网上下载。3、违法类网站，不会公开，在小圈子里去交易源码,闲鱼淘宝,第三方源码站菜鸟源码

**得到源码做安全测试会有很大思路**

**数据库的源码结构(文件夹结构)可能没变,直接网址访问admin/system打后台**

有些网站数据库里有特有文件(如*.mdb用easyaccess打开),可以通过此文件确定源码,此为CMS工具识别(指纹识别)  

CMS识别网站

`https://www.yunsee.cn/    企业版收费`

`http://whatweb.bugscaner.com/  广告`

## 第五天-系统及数据库

<img src="https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/c080f636d69b8be5e7de8a0893605139.54xgoepfgss0.webp" alt="c080f636d69b8be5e7de8a0893605139" style="zoom:50%;" />

### 操作系统层面

如果是网站----windows大小写不区分，Linux区分大小写,也就是说,网址的某一个大小写修改后看网页正不正常

IP地址的话:namp扫描,ping命令的ttl值也可以(不建议)

静态网页只有一个界面,没有数据传递,也因此没有漏洞.

通过nmap进行扫描方法：
nmap -O IP地址

`不同的操作系统的默认TTL值是不同的， 所以我们可以通过TTL值来判断主机的操作系统，但是当用户修改了TTL值的时候，就会误导我们的判断，所以这种判断方式也不一定准确。下面是默认操作系统的TTL：`
`1、WINDOWS NT/2000   TTL：128`
`2、WINDOWS 95/98     TTL：32`
`3、UNIX              TTL：255`
`4、LINUX             TTL：64`
`5、WIN7              TTL：64`

### 数据库层面

```
组合类型asp + access/mssql
组合类型php + mysql 
组合类型aspx+mssql
组合类型jsp +mysql/oracle
组合类型Python + MongoDB
```

常见数据库默认端口号

```
关系型数据库
  mysql				3306
  sqlserver		1433
  oracle			1521
  psotgresql	5432
非关系型数据库
	MongoDB			27017
  Redis				6379
  memcached		11211
```

数据库可能存在弱口令,和数据库漏洞,数据库漏洞可以获取数据库权限/网站权限/修改网页内容

### 第三方层面

`nmap -O -sV 10.1.1.130 端口扫描,可知第三方`

`不同的第三方软件或工具存在不同的漏洞、识别到更多的信息对收集到的漏洞也就越多`

弱口令
软件的漏洞攻击

## 第六天-加密编码算法

**burpsuite改包时要尤其注意url编码问题,可能会产生二次转义问题**

1. md5不可逆
   
   解密:https://www.cmd5.com/
2. base64编码的特点：随着编码的文本增加而增加、由大小写和数字组成且字符结尾一般有两个==
一般在代码中为了安全会使用base64进行编码
3. unescape编码:
和URL编码有点像
特点：一般是%U+四个数字对应着两个字符、主要运用于网站web应用
4. AES加密
   aes在逐渐的取代md5值、在解密的过程中一定要知道密码和偏移量不然是借不出来的。
   在线工具：http://tool.chacuo.net/cryptaes
   
   **当base64解码出现乱码是,大概是aes加密后再用base64加密了**
   
   **密码,偏移量必须知道,才可能解出aes解密**
5. DES（类似于base64）
   
   特点：明文的长度和密文成正比，有时会出现加号
   
   网页加密，工具解密---出现乱码（why-不同平台参数不同，用同一平台）
   
   ![bae186cfe2b7046d64fd454616367083](https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/bae186cfe2b7046d64fd454616367083.1u1fh7g4hbgg.webp)

**这一节并没有看完!!!**

## 第七天-CDN相关技术

- **如何判断目标存在 CDN 服务？**
  
  http://ping.chinaz.com/
  http://ping.aizhan.com/
  http://ce.cloud.360.cn/
  
  若IP不一样,则用了CDN

- **目前常见的CDN绕过技术有什么**
  ```
  子域名查询：
  因为有些主站是做了CDN服务而子站是没有做CDN服务
  
  邮件服务查询
  因为邮箱大部分都是内部人在访问、而且访问的量也不是很大，一般是没有做CDN。
  
  国外地址请求
  因为很多的企业没有在国外部署CDN
  要是用国外的地址请求、就容易找到他的真实地址。
  全局VPN访问
  
  遗留文件、扫描全网
  如PHPinfo信息当中会遗留出ip地址
  inurl:phpinfo.php
  搜索全网后自己分析(极不建议)
  
  黑暗引擎搜索//似乎要ico+hash
  fofa、shodan、谛听、zoomeye、censys
  
  特定文件dns历史记录，以前可能没用过cdn.
  https://x.threatbook.cn
  
  以量打量(ddos)
  ddos打完他的cdn流量,然后就是真实的IP地址了(不推荐)
  
  扫全网,以绕过cdn获得IP
  	fackcdn w8fuckcdn	zmap
  ```
  
  武汉的公司一般不会在武汉用CDN
  
  **CDN真实IP地址获取后绑定指向地址
  更改本地HOSTS解析指向文件**

**技巧:**

1. 通常网站管理员将两个地址(*.xiaodi.com和www.xiaodi.com)解析至同一ip，但搭建CDN服务时候，可能存在网站管理员只将其中一个(www.xiaodi.com)设置解析至CDN服务器，也就是说 两种访问方式访问的ip并不相同

   **所以可以通过超级PING查询去掉了www.后的网站IP**,这样操作之后如果IP差不多了,那么就是**真实地址**,他们都是负载均衡.

2. 将www改为m,转化为手机版网站---界面相同，域名不同---通过识别手机版来鉴别真实ip

3. 验证获取到ip是否可信可以采用第三方的ip地址查询工具经行验证。
  https://get-site-ip.com/

4. 有备案地址,验证服务器

   https://tools.ipip.net/cdn.php

openai的key**api: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**

## 第八天-信息收集:架构,搭建,WAF

![58aedb437233f1f1e0b1de6e27ef272d](https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/58aedb437233f1f1e0b1de6e27ef272d.5i8or41hazo0.webp)

** 和大佬的差距从此开始**

GitHub那一项有奇效

***

### 站点搭建习惯分析

1. 目录型站点
   
   简单的理解就是主站上面存在其他的cms程序
   例如：
    学生网站的上面通过后台扫描探针发现有一个bbs的目录一点击发现是一个bbs的论坛网站如：www.xxx.com/bbs
    我们把这个成为目录型网站、可以有两种找到漏洞的思路一个是主站的漏洞另外的一个是bbs上面的漏洞
2. 端口型站点
   
   有的站点不是使用的是默认的站点80而是其他的端口、可以使用shodan这种工具去收集端口
3. 子域名站点
   
   现在的主流网站都是采用的这种模式且子域名和网站之间很有可能是不在同一台的服务器上面。
4. 类似域名的站点
   
   京东的网站是jd.com 那么他就有可能是采用了jd.net jd.cn等域名我们采用社工的方式去尝试获取他的相关域名信息
   1. 根域名的改变，如.cn/.net改为.com
   2. 顶级域名的改变，如www.jingdong.com改为www.jd.com
   3. 查询方法---写脚本爆破根域名，如cn,com,net…;或者改变顶级域名的数字，如date1.com；date2.com等等
5. 旁注,C段站点
   
   旁注：同一个服务器上面存在多个站点,但是你要攻击的是A网站由于各种原因不能完成安全测试。就通过测试B网站进入服务器然后在攻击A网站最终实现目的(内网渗透)。
   
   [同服务器下网站扫描](https://www.webscan.cc/)
   
   C段：不同的服务器上面存在不同的网站,通过扫描发现与你渗透测试的是同一个网段最终拿下服务器、然后通过内网渗透的方式拿下渗透服务器。(没有办法的办法,非常长的渗透手段)

<img src="https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/876cf78fc8adf5e6890d1d6f5fc09312.51glzr4fd4o0.webp" alt="876cf78fc8adf5e6890d1d6f5fc09312" style="zoom:50%;" />

<img src="https://cdn.staticaly.com/gh/shadow-aaa/markdown_photo@main/20230421/e80ca80ec0737af03439aca46b7c9ae0.52ipskkuxbs0.webp" alt="e80ca80ec0737af03439aca46b7c9ae0" style="zoom:50%;" />

6. 搭建软件特征站点

​	PHPstudy、宝塔,WANP等环境这样的集成环境搭建的危害就是泄露了详细的版本信息。

​	抓包可以看出搭建软件(server)

​	~~server:nginx一般自己搭建的环境~~

```
phpstudy软件搭建的数据包
server:apache openssl php
X-forward-by:php
```

## WAF防护分析

Web应用防护系统（也称为：网站应用级入侵防御系统。英文：Web Application Firewall，简称： WAF）。

- 如何快速识别WAF

[wafw00f](https://github.com/EnableSecurity/wafw00f)

在有些网站的请求信息当中有的网站没有做安全信息上面留下了waf的相关信息

使用nmap指纹检测

```c_cpp
nmap --script==http-waf-fingerprint

nmap --script=http-waf-detec
```

- [identYwaf](https://github.com/stamparm/identywaf)

与wafwoof相比**运行速度慢，比较稳定推荐**还是使用这一款工具。

- 识别wAF对于安全测试的意义?

对于一个网站要是使用了waf而渗透人员没有识别直接使用工具进行扫描有可能会导致waf将你的ip地址拉入黑名单而不能访问。而识别waf在于有针对性行的绕过各个厂商的waf可能存在着不同的绕过思路。

## 第九天-APP及其它资产等

写个测试
