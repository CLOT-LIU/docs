#### 1、购买

官网：[https://chevereto.com/](https://chevereto.com/)

打开官网即可看见活动，目前的活动是20% OFF，0.8折的优惠还是值得入手的。

#### 2、登录下载

控制台：https://chevereto.com/panel

![chevereto3network1.png](https://tupian.clotliu.com/76e1b6d0ae287fd38677d774a294262a.png)

#### 3、下载最新版

这里简单说下，安装分两种，一种就是你下载（installer）一个单PHP文件，因为我没试过，可能需要你输入序列号，是通过github下载程序，国内安装速度很慢。

也可以直接下载最新版本的程序包，安装速度快，不需要输入序列号，默认就已经是商业版本了。

![chevereto3network2.png](https://tupian.clotliu.com/7eb336343d18cdf5d9f297db29e1fafb.png)

#### 4、安装准备

大鸟搭建的环境是用宝塔面板，具体如下：

（1）宝塔面板（宝塔服务器面板，一键全能部署及管理，送你3188元礼包，[点我领取](https://www.bt.cn/?invite_code=MV96YnVvdHU=)）

（2）nginx1.18

（3）mysql5.7

（4）phpmyadmin4.7

（5）PHP7.4

#### 5、下载以及安装前的设置

**（1）程序下载**

你购买之后登录控制台下载最新程序，这里可以看第三步。

**（2）新建站点**

宝塔新建站点，不在赘述。

**（3）上传程序**

把下载好的程序包上传到你网站根目录，之后解压，宝塔是支持在线解压的，你上传程序包即可，不需要解压好用ftp工具上传。

**（4）设置nginx规则**

把程序包自带的已经被你放置到网站根目录中的nginx.txt内的配置规则添加到网站的配置文件 server {} 里面，保存并重启nginx。

如果你是apache那么请找Apache.txt，并复制里面的内容，到网站配置中。既然是放置在server {} 那么，你可以直接把nginx.txt里面的内容都放在伪静态设置中，也是可以的。看图：

![chevereto3network30.png](https://tupian.clotliu.com/b8e22d4a229ee0a171c6a463880bc395.png)

#### 5、安装

浏览器打开域名开始安装。

**（1）连接数据库**

![chevereto3network4.png](https://tupian.clotliu.com/b9c6118112cd888e5b2ee018dbb43a42.png)

**（2）设置管理员等**

![chevereto3network5.png](https://tupian.clotliu.com/93d3ce662561172124d5b4a1e3969989.png)

提交后即可完成安装。

#### 6、简单设置

**（1）设网站tdk**

![chevereto3network6.png](https://tupian.clotliu.com/c4774e867cc1e9cd9b4c3c31ba5864f1.png)

**（2）设置webp图片上传**

宝塔面板用户，直接开启即可支持webp格式上传，无需其他设置。

![chevereto3network7.png](https://tupian.clotliu.com/d4534f03cfbf88fdd150934a9b94c9db.png)

![chevereto3network8.png](https://tupian.clotliu.com/83457605f3e27277948ee5e96a3be6e9.png)

**（3）启用邮件验证**

如果你要注册启用邮件验证，具体看图设置：

![chevereto3network9.png](https://tupian.clotliu.com/2d55066a2fe197bdaf30af6f0f29e715.png)

注意：SMTP密码写api密码，不是你的登录密码。

**（4）外部存储**

![chevereto3network31.png](https://tupian.clotliu.com/c9dba29aadcc89768f65e1346d04aa9a.png)

#### 7、最后

用宝塔面板来部署还是很简单的，而且webp开启也很容易，不会有多余的设置。

图片需要开启鉴黄，不然，后果你懂的。

收费版支持wepb格式图片上传，支持外部存储等。

chevereto图床的颜值是真的不错的，看起来赏心悦目。
