---
id: chevereto-free
title: 宝塔面板安装Chevereto免费版
---

看到很多站长用的Chevereto免费版本的图床程序，这图床确实也不错，颜值不错，功能上也可以。Chevereto分为收费版本和免费版本，本篇教程也是安装的Chevereto最新免费版 ，不过功能上是足够使用了。

![btchevereto1min.png](https://tupian.clotliu.com/0fe12c93ceec51bd4e9112d960b935a5.png)

其免费版和收费版的区别，在于收费版多了硬盘扩展，社交分享功能和技术支持。所以个人觉得，免费版已经足够使用了。而且`chevereto`的安装也非常简单，并且支持中文。

## 具体的安装和部署

---

#### 1、前言

github：https://github.com/Chevereto/Chevereto-Free

官网：https://chevereto.com/

演示：https://demo.chevereto.com/

#### 2、环境准备

1. 宝塔面板最新版本（目前7.0.3是最新版本。）
2. PHP7.3
3. MySQL5.6
4. 解析好的域名一个
5. 新建好网站
6. 新建好数据库
7. Chevereto推荐使用1.4.2的版本，因为1.4.2之后的免费版去除了多语言支持

#### 3、下载

下载程序到自己的网站根目录，直接解压，把文件都移动至网站根目录。

下载地址：https://github.com/rodber/chevereto-free/releases/download/1.4.2/1.4.2.zip

看图：

![btchevereto2min.png](https://tupian.clotliu.com/d4d2bae0cec5a0958b968e340506bba6.png)

#### 4、伪静态

不过安装之前需要先设置伪静态，代码如下：

```
location / {
index index.php;
try_files $uri $uri/ /index.php?$query_string;
}
```

看图：

![btchevereto3min.png](https://tupian.clotliu.com/656670ddbc9cdc9ffbd982a133e970ab.png)

#### 5、安装

浏览器打开你的域名访问，开始安装，如图：

![btchevereto4min.png](https://tupian.clotliu.com/6145959fd0b369c11b242ad9f3af79f2.png)

又有错误了，看来程序对PHP7.3支持的不太好，错误代码是一段警告，如下：

```
Warning: "continue" targeting switch is equivalent to "break". Did you mean to use "continue 2"? in /www/wwwroot/xp.daniao.org/lib/G/functions.php on line 254
```

1. 根据提示找到：“`/www/wwwroot/xp.daniao.org/lib/G/functions.php`”
2. 并将第254行的`continue`改为`continue 2`

看图：

![btchevereto5min.png](https://tupian.clotliu.com/8c367c13bf117d457a379eadcb744053.png)

保存之后，刷新安装页面即可。安装成功截图：

![btchevereto6min.png](https://tupian.clotliu.com/85e853d25a609ded2d35ddbe6be00fc0.png)

#### 6、设置为中文

登录后台：`dashboard/settings/languages`  然后这位简体中文即可，如图：

![btchevereto7min.png](https://tupian.clotliu.com/4b1c288c23836380626f82568ea3304d.png)

#### 7、特色的功能

通过安装我们的上传插件，将图像上传到您的网站，博客或论坛。 它提供图像上传到任何网站，放置一个按钮，将允许您的用户直接上传图像到我们的服务，它将自动处理插入所需的代码。 所有功能包括拖放，远程上传，图像调整大小等。

![btchevereto8min.png](https://tupian.clotliu.com/de238f2dddee36dba38bc145df6471a7.png)

#### 8、最后

图床非常给力，虽然是免费版但是功能上也足够惊艳了，如果是商业版本还支持第三方直接登录和硬盘的扩展。但是个人用个免费版本也是足够了。

**提示**：建议关闭宝塔nginx防火墙，批量上传时容易触发cc防御进而封禁IP  或者把cc的规则设置的更为宽松一点。
	