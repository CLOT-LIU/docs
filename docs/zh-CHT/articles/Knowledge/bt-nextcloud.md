# 前言

当我们使用宝塔面板部署好后，可以直接使用，如果你还没有部署Nextcloud，可以参考：

* [如何使用腾讯云轻量服务器快速给自己搭建Nextcloud私人网盘？](https://cloud.tencent.com/developer/article/1787399?from=10680)

但是**管理员-设置-概览**内，检测一般会存在一些警告和错误，这些我们如何解决呢？

![j24e94yp7n.png](https://tupian.clotliu.com/e2e602aa260e1c3a4c7e1da060b34178.png)<center>管理员-设置-概览</center>


![c3tk8feorv.png](https://tupian.clotliu.com/c80ab1efc200b4c5eea7a1dcef6459ab.png)<center>部分警告和错误</center>

# 通过HTTP访问网站不安全。强烈建议您将服务器设置成要求使用HTTPS协议

这个问题最好解决，同时也可能是无法解决问题：

**服务器绑定域名，并配置**[**SSL证书**](https://cloud.tencent.com/product/ssl?from=10680)**，域名解析到服务器即可**

但是：

**国内服务器需要绑定备案的域名，若无备案域名，则只能使用IP访问Nextcloud，那么该条警告无法去除。**

# 一些文件没有通过完整性检查. 了解如何解决该问题请查看我们的文档. (无效的文件列表… / 重新扫描…)

![t5880m76pp.png](https://tupian.clotliu.com/ac3c0d017803cb4406ae69b92a0f2b28.png)<center>“无效文件列表”错误</center>

![4u9yi6crqx.png](https://tupian.clotliu.com/c2f63e6c19d3d53f198d1e3005956fa0.png)<center>提示的无效文件</center>

你的无效的文件列表和我的可能不一样，但是方法是一样的：

1. 开nextcloud的安装地址，也就是Nginx所代理的网站根目录
2. 删除“提示的无效文件“

![trcv85b1gj.png](https://tupian.clotliu.com/45fa318da17d89393cfe7b07080f0a8d.png)<center>Nextcloud目录列表</center>

**如果你使用宝塔面板，可以进入宝塔面板后台，然后使用宝塔的图形界面删除无效文件**。如果你熟悉Linux命令，可以使用`rm`命令删除：

![uwguxp4atr.png](https://tupian.clotliu.com/d1644ef9feb7d1baa18d0f66df610280.png)<center>rm命令删除</center>

# PHP configuration option output_buffering must be disabled

其实这个很好解决，PHP默认是有4096字节缓冲的。但是Nextcloud希望你关闭。如果你是自己安装的PHP，在你安装PHP的路径下，打开PHP配置文件（`php.ini`），将要
```
output_buffering = 4096
```
改为：

```
; output_buffering = 4096
```

`;`为PHP的注释符号

如果你是宝塔安装配置的php，更简单了。在宝塔面板，依次打开：`软件商店`-`已安装`-`PHP7.3设置`-`配置文件`

查找文本`output_buffering`，并在前面加上`;`注释

![s89meyztt9.png](https://tupian.clotliu.com/8adc1a8224bab3f5436e926accffaca9.png)<center>加上注释</center>

之后，可能需要重载PHP配置或者重启PHP服务才能生效。再次查看Nextcloud**概述**，就没有这条警告了。

# 您的数据目录和文件可以从互联网直接访问。.htaccess 文件不起作用。强烈建议您配置 Web 服务器，以便数据目录不再可访问，或者您可以将数据目录移动到 Web 服务器文档根目录。

这个其实是Nginx的问题，为了进一步提升安全性，我们打开Nginx网站设置

![mbj35fwywf.png](https://tupian.clotliu.com/96432e200026a2812aa95fe63ae925b5.png)<center>宝塔内网站Nginx设置</center>

**在location内的禁止访问目录内，加入data目录。**

![l3a2yj5pnw.png](https://tupian.clotliu.com/5b4d392fdc9b949cbcfcd054ca8b5923.png)<center>加入data目录</center>

# PHP 的安装似乎不正确，无法访问系统环境变量。getenv(“PATH”) 函数测试返回了一个空值

这个处理方法很简单；如果你是自己安装配置的PHP，一般不会出现这个问题，当时如果是使用宝塔安装，一般都会有这个问题，解决方法很简单：

在宝塔面板，依次打开：`软件商店`-`已安装`-`PHP7.3设置`-`FPM配置文件`

在文末添加：

```
env[PATH] = /usr/local/bin:/usr/bin:/bin:/usr/local/php/bin
```

![rcfwzicphp.png](https://tupian.clotliu.com/42a1f64a9a6c38d07659ebfe9375a793.png)<center>添加配置</center>

之后，可能需要重载PHP配置或者重启PHP服务才能生效。

# 您的网页服务器未正确设置以解析****。更多信息请参见文档

这个处理方法很简单，简单地说，设置Nginx即可。如果你的Nginx是宝塔安装的，那么打开网站的Nginx：

![](https://tupian.clotliu.com/96432e200026a2812aa95fe63ae925b5.png)<center>打开Nginx设置</center>

之后追加以下内容：

```
rewrite /.well-known/carddav /remote.php/dav permanent;
rewrite /.well-known/caldav /remote.php/dav permanent;
```

![dkdmjhm1ne.png](https://tupian.clotliu.com/5b79ebb315cc080f520855e07cb8917c.png)<center>追加内容</center>

之后保存即可

# PHP模块问题

PHP模块问题包括：

1. 未找到PHP的"fileinfo"模块。强烈推荐启用该模块，从而获得更好的MIME类型探测结果。
2. **内存缓存未配置，为了提升使用体验，请尽量配置内存缓存。更多信息请参见文档。**
3. PHP的OPcache模块未载入。推荐开启获得更好的性能。

![xkgeob7hn8.png](https://tupian.clotliu.com/67e4c85f529a6e2abdf1bd02c0560ed1.png)<center>!PHP模块问题</center>

安装如下模块：

![e71iy40d5f.png](https://tupian.clotliu.com/ea8b5955a52b74717ae1b11b36884317.png)<center>装的模块-01</center>安

![8rhu405as1.png](https://tupian.clotliu.com/965d1618c650ad6f82f776a9ebd16e13.png)<center>安装的模块-02</center>

同时，因为使用`apcu`作为缓冲，所以我们需要打开Nextcloud的配置文件，追加以下内容：


```
'memcache.local' => '\OC\Memcache\Redis',
  'redis' => array(
    'host' => 'localhost',
    'port' => 6379,
    ),
```