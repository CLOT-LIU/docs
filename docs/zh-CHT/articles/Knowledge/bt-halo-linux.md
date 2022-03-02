# 一、服务器环境说明

1. 宝塔 7.7.0 或更新版本
2. Linux Server（本文用的是 CentOs 7.6 64位）
3. Apache 或者 Nginx（本文用的是 Nginx 1.16.1）
4. MySQL 5.6+
5. PHP 7.1+（本文 PHP-7.3）
6. phpMyAdmin 4.7

# 二、安装宝塔 Linux 面板

使用 SSH 工具（[查看使用方法](https://clotliu.com/archives/finalshell%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B)），执行命令开始安装（大约2分钟完成面板安装）。

**Centos安装宝塔面板命令：**

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```


执行安装命令，询问是否安装，回答 “ y ”

![](https://s1.ax1x.com/2020/10/15/0ThQjU.png)

安装完成会打印这些东西（面板 ip 地址、用户名、密码）：

![](https://s1.ax1x.com/2020/10/15/0Th4KS.png)

图源：宝塔面板


# 三、安装 LNMP 环境

浏览器输入宝塔面板的 ip 地址。登陆账号，进入面板。

> 首次进入面板，在弹出的“推荐安装套件”窗口中选择左侧的「**LNMP 极速安装**」

选择好 PHP 等环境的版本号，点击一键安装后，会弹出消息盒子，等待任务执行完毕即可。

![](https://s1.ax1x.com/2020/10/15/0T4uad.png)



进入宝塔面板 – 【软件商店】 – 【已安装】，点击 PHP 设置。

# 四、安装 Docker

## 准备工作

### 系统要求

Docker 支持 64 位版本 CentOS 7/8，并且要求内核版本不低于 3.10。 CentOS 7 满足最低内核的要求，但由于内核版本比较低，部分功能（如 `overlay2` 存储层驱动）无法使用，并且部分功能可能不太稳定。

### 卸载旧版本

旧版本的 Docker 称为 `docker` 或者 `docker-engine`，使用以下命令卸载旧版本：

```
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine

```


## 使用 yum 安装

执行以下命令安装依赖包：

```
sudo yum install -y yum-utils
```

鉴于国内网络问题，强烈建议使用国内源，官方源请在注释中查看。

执行下面的命令添加 `yum` 软件源：

```
$ sudo yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

$ sudo sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

# 官方源
# $ sudo yum-config-manager \
#     --add-repo \
#     https://download.docker.com/linux/centos/docker-ce.repo
```

如果需要测试版本的 Docker 请执行以下命令：

```
$ sudo yum-config-manager --enable docker-ce-test
```

## 安装 Docker

更新 `yum` 软件源缓存，并安装 `docker-ce`。

```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

## 启动 Docker

```
$ sudo systemctl start docker
```

## 验证Docker引擎是否正确安装。

```
$ sudo docker run hello-world
```

# 五、安装 halo

此步骤按照[官方 Docker 部署文档](https://docs.halo.run/getting-started/install/docker)一步步来就好

## 5.1 新建存放 halo 的网站

前往宝塔面板 – 【网站】 – 【添加站点】。

## 5.2 配置 SSL 证书

打开站点设置，进入 SSL 选项卡页面，挑选您想要配置的安全证书方式：

* [宝塔一键 SSL](https://www.bt.cn/ssl)（一年证书免费申请，需要登录宝塔账号并实名认证）
* [Let’s Encrypt 三个月免费证书](https://blog.csdn.net/msllws/article/details/82255078)
* [已有证书文件，上传至宝塔](https://yq.aliyun.com/articles/705391)

# 六、配置反向代理

> 上面其实就已经安装好了 halo，但是想要通过域名访问网站还需要进一步配置才能正确运行。

## 6.1 修改 Nginx 配置

1. 进入宝塔面板，打开站点设置，修改网站配置文件：(可对照下图修改)

反代脚本
```
            location / {
    proxy_pass http://127.0.0.1:8090/;
    rewrite ^/(.*)$ /$1 break;
    proxy_redirect off;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Upgrade-Insecure-Requests 1;
    proxy_set_header X-Forwarded-Proto https;
  }
```

![JY0BI_WGDYPF008H1O.png](https://cdn.lixingyong.com/2021/11/15/JY0BI_WGDYPF008H1O.png)
别忘记将这一段注释掉

![5S1Q3B1KTP005O27B.png](https://cdn.lixingyong.com/2021/11/15/5S1Q3B1KTP005O27B.png)

# 七、开始使用你的博客吧！
