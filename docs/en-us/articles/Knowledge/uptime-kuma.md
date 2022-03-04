这篇文章还是基于[宝塔面板](https://www.bt.cn/?invite_code=MV96YnVvdHU=)搭建这个程序，宝塔服务器面板，一键全能部署及管理，送你3188元礼包，[点我领取](https://www.bt.cn/?invite_code=MV96YnVvdHU=)

![uptimekuma12.png](https://tupian.clotliu.com/a3d67768b1c56a1a54e390820717f4a6.png)

## 1、简介

项目：https://github.com/louislam/uptime-kuma

演示：https://stats.clotliu.com

## 2、准备

1. 准备好vps
2. 按照[宝塔官方文档](https://www.bt.cn)安装好宝塔面板
3. 安装好docker管理器([Docker安装教程](https://clotliu.com/archives/docker-install))
4. 安装好nginx1.20或其他版本
5. 准备好域名

## 3、部署

因为作者提供了docker方式的安装，这里我们也推荐这个方式，本教程也是基于docker安装。

1. 安装代码如下（ssh工具连接到服务器，然后无脑复制命令输入即可）

```
docker volume create uptime-kuma
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

**2）注意：**

部署完毕后，浏览器输入`http://你服务器IP:3001`来访问uptime-kuma，如不能访问需要在安全中放行端口。如果提示3001端口冲突，可以自行修改为其他端口！！

## 4、使用

1. 初始化设置，首次访问需要设置管理员账号、密码，根据提示完成即可。

![uptimekuma1.png](https://tupian.clotliu.com/f33c1ccfe81bf7a8faa669451980bf79.png)

2. 完成初始话就可以进入后台，可以根据需要创建TCP/PING/HTTP/DNS监控等等。

![uptimekuma2.png](https://tupian.clotliu.com/991c0d5c0d2f640d83f99bfab9b40def.png)

3. 简单设置一个ping监控，具体看图：至于这个ping的频率可以根据需要来修改！

![uptimekuma3.png](https://tupian.clotliu.com/b8a5c3a2466a80b2660729514b0f3c0c.png)

4. ping监控设置好后，稍等片刻就可以看到图表显示了。

![uptimekuma4.png](https://tupian.clotliu.com/b651ea0c2d2b8f003d8fae9c548ddfff.png)

## 5、域名访问

1. 宝塔设置域名访问，看图：

![uptimekuma6.png](https://tupian.clotliu.com/02b1b22f0e84c10db3f918e3755880e8.png)

2. 错误：Cannot connect to the socket server. [Error: websocket error] Reconnecting...

![uptimekuma5.png](https://tupian.clotliu.com/6d7f969e761de47a86a701ffeac54c9e.png)

2. 修改默认的代码，把默认的代码修改为如下：（修改后，刷新即可看到可以正常访问了！）

```
location / {
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_pass http://127.0.0.1:3001/;
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
}
```

不知道放哪里看图：

![uptimekuma7.png](https://tupian.clotliu.com/74c20fc4c993cee40aa578baacf7cdbd.png)

## 6、添加通知

支持通知的种类很多，比如smtp，webhook，tg等等！选择一个自己熟悉的来添加！！

![uptimekuma8.png](https://tupian.clotliu.com/a4335c81b6c82b918920428b9b3c8885.png)

## 7、禁用身份验证

1)这是可选的，如果不禁用游客访问需要用户名和密码，但是你关掉后，就可以自由访问了。（后台后上角的设置，然后拉到最下面即可看到！）

![uptimekuma9.png](https://tupian.clotliu.com/72bc8f88ce8b1d47ac9a1b4a8c5138d9.png)

2. 禁用身份验证后，游客都可以随意修改你的后台设置，所以这里建议还是开启！

## 8、设置Status Page

这个功能还是很重要的，可以把新建的监控服务放置到这个监控页面，这样就可以随时随地的看到每个系统的状态了。

1. 点击右上角的Status Page，开始编辑，具体看图：

![uptimekuma10.png](https://tupian.clotliu.com/5325ed18e3026f4ae88045f90873ccee.png)

2. 效果

![uptimekuma12.png](https://tupian.clotliu.com/a3d67768b1c56a1a54e390820717f4a6.png)

## 9、最后

uptime-kuma虽然没有商业程序的强大功能，但是对于个人用户来说，已经足够使用了。如果你正在考虑自建一个[监控程序](https://clotliu.com/archives/uptime-kuma)，那么可以折腾试试！！

