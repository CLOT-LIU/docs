## 一、服務器環境說明

1. 寶塔 7.7.0 或更新版本
2. Linux Server（本文用的是 CentOs 7.6 64位）
3. Apache 或者 Nginx（本文用的是 Nginx 1.16.1）
4. MySQL 5.6+
5. PHP 7.1+（本文 PHP-7.3）
6. phpMyAdmin 4.7

## 二、安裝寶塔 Linux 面板

使用 SSH 工具（[查看使用方法](https://clotliu.com/archives/finalshell%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B)），執行命令開始安裝（大約2分鍾完成面板安裝）。

**Centos安裝寶塔面板命令：**

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```


執行安裝命令，詢問是否安裝，回答 “ y ”

![](https://s1.ax1x.com/2020/10/15/0ThQjU.png)

安裝完成會打印這些東西（面板 ip 地址、用戶名、密碼）：

![](https://s1.ax1x.com/2020/10/15/0Th4KS.png)

圖源：寶塔面板


## 三、安裝 LNMP 環境

浏覽器輸入寶塔面板的 ip 地址。登陸賬號，進入面板。

> 首次進入面板，在彈出的“推薦安裝套件”窗口中選擇左側的「**LNMP 極速安裝**」

選擇好 PHP 等環境的版本號，點擊一鍵安裝後，會彈出消息盒子，等待任務執行完畢即可。

![](https://s1.ax1x.com/2020/10/15/0T4uad.png)



進入寶塔面板 – 【軟件商店】 – 【已安裝】，點擊 PHP 設置。

## 四、安裝 Docker

### 准備工作

#### 系統要求

Docker 支持 64 位版本 CentOS 7/8，並且要求內核版本不低于 3.10。 CentOS 7 滿足最低內核的要求，但由于內核版本比較低，部分功能（如 `overlay2` 存儲層驅動）無法使用，並且部分功能可能不太穩定。

#### 卸載舊版本

舊版本的 Docker 稱爲 `docker` 或者 `docker-engine`，使用以下命令卸載舊版本：

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


### 使用 yum 安裝

執行以下命令安裝依賴包：

```
sudo yum install -y yum-utils
```

鑒于國內網絡問題，強烈建議使用國內源，官方源請在注釋中查看。

執行下面的命令添加 `yum` 軟件源：

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

如果需要測試版本的 Docker 請執行以下命令：

```
$ sudo yum-config-manager --enable docker-ce-test
```

### 安裝 Docker

更新 `yum` 軟件源緩存，並安裝 `docker-ce`。

```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

### 啓動 Docker

```
$ sudo systemctl start docker
```

### 驗證Docker引擎是否正確安裝。

```
$ sudo docker run hello-world
```

## 五、安裝 halo

此步驟按照[官方 Docker 部署文檔](https://docs.halo.run/getting-started/install/docker)一步步來就好

### 5.1 新建存放 halo 的網站

前往寶塔面板 – 【網站】 – 【添加站點】。

### 5.2 配置 SSL 證書

打開站點設置，進入 SSL 選項卡頁面，挑選您想要配置的安全證書方式：

* [寶塔一鍵 SSL](https://www.bt.cn/ssl)（一年證書免費申請，需要登錄寶塔賬號並實名認證）
* [Let’s Encrypt 三個月免費證書](https://blog.csdn.net/msllws/article/details/82255078)
* [已有證書文件，上傳至寶塔](https://yq.aliyun.com/articles/705391)

## 六、配置反向代理

> 上面其實就已經安裝好了 halo，但是想要通過域名訪問網站還需要進一步配置才能正確運行。

### 6.1 修改 Nginx 配置

1. 進入寶塔面板，打開站點設置，修改網站配置文件：(可對照下圖修改)

反代腳本
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
別忘記將這一段注釋掉

![5S1Q3B1KTP005O27B.png](https://cdn.lixingyong.com/2021/11/15/5S1Q3B1KTP005O27B.png)

## 七、開始使用你的博客吧！
