# 安裝 Docker

## 准備工作

### 系統要求

Docker 支持 64 位版本 CentOS 7/8，並且要求內核版本不低于 3.10。 CentOS 7 滿足最低內核的要求，但由于內核版本比較低，部分功能（如 `overlay2` 存儲層驅動）無法使用，並且部分功能可能不太穩定。

### 卸載舊版本

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

## 使用 yum 安裝

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

## 安裝 Docker

更新 `yum` 軟件源緩存，並安裝 `docker-ce`。

```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

## 啓動 Docker

```
$ sudo systemctl start docker
```

## 驗證Docker引擎是否正確安裝。

```
$ sudo docker run hello-world
```
