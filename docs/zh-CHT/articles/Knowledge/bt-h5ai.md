---
id: bt-h5ai
title: h5ai安装教程
---

# 介绍

h5ai可以把对应目录下的文件和文件夹全部显示在web页面上，只需点击即可下载对应的资料

h5ai需要php5.5版本以上环境，可在apache、nginx环境下运行，这里还是直接用宝塔安装就OK

**下载h5ai：[点击下载](https://release.larsjung.de/h5ai/h5ai-0.30.0.zip)**

**Github：~​~​[https://github.com/lrsjng/h5ai](https://github.com/lrsjng/h5ai)**

# 方法：

宝塔后台添加站点，用你自己的域名或IP都可以：

![3226207728.png](https://tupian.clotliu.com/7296252f83fbcfcacb8c88386f6b5567.png)

站点添加完成后将根目录下所有文件删除，并上传解压后的 **_h5ai** 文件夹，如下图

![2869875154.png](https://tupian.clotliu.com/4941743664772b2d48ae6a80ce628967.png)

然后修改 **宝塔后台 - 网站 - 设置 - 默认文档**，全部删除替换成下面的代码然后点击添加：

```
index
index.html
index.php
/_h5ai/public/index.php
```

示例图：

![254645309.png](https://tupian.clotliu.com/ee3ffe00ab011f211be3fb4079069c8e.png)

OK，完成，搭建其实很简单，现在打开域名即可使用账户密码登录

默认用户名：**admin**

默认密码：**admin**

如果要取消登录验证就将 **_h5ai / public / index.php** 里第二行 **include 'login.php'** 删除即可

如果要修改用户名和密码在 **_h5ai / public / login.php**

上传或下载文件到网站根目录就可以在 **web** 页面显示出来，也可以建立新的文件夹

**如果打开网页出现以下错误：**

```
Warning: putenv() has been disabled for security reasons in
```

原因：禁用了部分存在危险的PHP函数

解决方法：

打开PHP配置文件：找到**disable_functions**字符串，将后面的**putenv**删除，然后重启PHP即可；
