這篇文章還是基于[寶塔面板](https://www.bt.cn/?invite_code=MV96YnVvdHU=)搭建這個程序，寶塔服務器面板，一鍵全能部署及管理，送你3188元禮包，[點我領取](https://www.bt.cn/?invite_code=MV96YnVvdHU=)

![uptimekuma12.png](https://tupian.clotliu.com/a3d67768b1c56a1a54e390820717f4a6.png)

#### 1、簡介

項目：https://github.com/louislam/uptime-kuma

演示：https://stats.clotliu.com

#### 2、准備

1. 准備好vps
2. 按照[寶塔官方文檔](https://www.bt.cn)安裝好寶塔面板
3. 安裝好docker管理器([Docker安裝教程](https://clotliu.com/archives/docker-install))
4. 安裝好nginx1.20或其他版本
5. 准備好域名

#### 3、部署

因爲作者提供了docker方式的安裝，這裏我們也推薦這個方式，本教程也是基于docker安裝。

1. 安裝代碼如下（ssh工具連接到服務器，然後無腦複制命令輸入即可）

```
docker volume create uptime-kuma
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

**2）注意：**

部署完畢後，浏覽器輸入`http://你服務器IP:3001`來訪問uptime-kuma，如不能訪問需要在安全中放行端口。如果提示3001端口衝突，可以自行修改爲其他端口！！

#### 4、使用

1. 初始化設置，首次訪問需要設置管理員賬號、密碼，根據提示完成即可。

![uptimekuma1.png](https://tupian.clotliu.com/f33c1ccfe81bf7a8faa669451980bf79.png)

2. 完成初始話就可以進入後台，可以根據需要創建TCP/PING/HTTP/DNS監控等等。

![uptimekuma2.png](https://tupian.clotliu.com/991c0d5c0d2f640d83f99bfab9b40def.png)

3. 簡單設置一個ping監控，具體看圖：至于這個ping的頻率可以根據需要來修改！

![uptimekuma3.png](https://tupian.clotliu.com/b8a5c3a2466a80b2660729514b0f3c0c.png)

4. ping監控設置好後，稍等片刻就可以看到圖表顯示了。

![uptimekuma4.png](https://tupian.clotliu.com/b651ea0c2d2b8f003d8fae9c548ddfff.png)

#### 5、域名訪問

1. 寶塔設置域名訪問，看圖：

![uptimekuma6.png](https://tupian.clotliu.com/02b1b22f0e84c10db3f918e3755880e8.png)

2. 錯誤：Cannot connect to the socket server. [Error: websocket error] Reconnecting...

![uptimekuma5.png](https://tupian.clotliu.com/6d7f969e761de47a86a701ffeac54c9e.png)

2. 修改默認的代碼，把默認的代碼修改爲如下：（修改後，刷新即可看到可以正常訪問了！）

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

不知道放哪裏看圖：

![uptimekuma7.png](https://tupian.clotliu.com/74c20fc4c993cee40aa578baacf7cdbd.png)

#### 6、添加通知

支持通知的種類很多，比如smtp，webhook，tg等等！選擇一個自己熟悉的來添加！！

![uptimekuma8.png](https://tupian.clotliu.com/a4335c81b6c82b918920428b9b3c8885.png)

#### 7、禁用身份驗證

1)這是可選的，如果不禁用遊客訪問需要用戶名和密碼，但是你關掉後，就可以自由訪問了。（後台後上角的設置，然後拉到最下面即可看到！）

![uptimekuma9.png](https://tupian.clotliu.com/72bc8f88ce8b1d47ac9a1b4a8c5138d9.png)

2. 禁用身份驗證後，遊客都可以隨意修改你的後台設置，所以這裏建議還是開啓！

#### 8、設置Status Page

這個功能還是很重要的，可以把新建的監控服務放置到這個監控頁面，這樣就可以隨時隨地的看到每個系統的狀態了。

1. 點擊右上角的Status Page，開始編輯，具體看圖：

![uptimekuma10.png](https://tupian.clotliu.com/5325ed18e3026f4ae88045f90873ccee.png)

2. 效果

![uptimekuma12.png](https://tupian.clotliu.com/a3d67768b1c56a1a54e390820717f4a6.png)

#### 9、最後

uptime-kuma雖然沒有商業程序的強大功能，但是對于個人用戶來說，已經足夠使用了。如果你正在考慮自建一個[監控程序](https://clotliu.com/archives/uptime-kuma)，那麽可以折騰試試！！

