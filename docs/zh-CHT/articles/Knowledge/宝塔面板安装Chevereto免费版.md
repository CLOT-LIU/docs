看到很多站長用的Chevereto免費版本的圖床程序，這圖床確實也不錯，顔值不錯，功能上也可以。Chevereto分爲收費版本和免費版本，本篇教程也是安裝的Chevereto最新免費版 ，不過功能上是足夠使用了。

![btchevereto1min.png](https://tupian.clotliu.com/0fe12c93ceec51bd4e9112d960b935a5.png)

其免費版和收費版的區別，在于收費版多了硬盤擴展，社交分享功能和技術支持。所以個人覺得，免費版已經足夠使用了。而且`chevereto`的安裝也非常簡單，並且支持中文。

## 具體的安裝和部署

---

#### 1、前言

github：https://github.com/Chevereto/Chevereto-Free

官網：https://chevereto.com/

演示：https://demo.chevereto.com/

#### 2、環境准備

1. 寶塔面板最新版本（目前7.0.3是最新版本。）
2. PHP7.3
3. MySQL5.6
4. 解析好的域名一個
5. 新建好網站
6. 新建好數據庫
7. Chevereto推薦使用1.4.2的版本，因爲1.4.2之後的免費版去除了多語言支持

#### 3、下載

下載程序到自己的網站根目錄，直接解壓，把文件都移動至網站根目錄。

下載地址：https://github.com/rodber/chevereto-free/releases/download/1.4.2/1.4.2.zip

看圖：

![btchevereto2min.png](https://tupian.clotliu.com/d4d2bae0cec5a0958b968e340506bba6.png)

#### 4、僞靜態

不過安裝之前需要先設置僞靜態，代碼如下：

```
location / {
index index.php;
try_files $uri $uri/ /index.php?$query_string;
}
```

看圖：

![btchevereto3min.png](https://tupian.clotliu.com/656670ddbc9cdc9ffbd982a133e970ab.png)

#### 5、安裝

浏覽器打開你的域名訪問，開始安裝，如圖：

![btchevereto4min.png](https://tupian.clotliu.com/6145959fd0b369c11b242ad9f3af79f2.png)

又有錯誤了，看來程序對PHP7.3支持的不太好，錯誤代碼是一段警告，如下：

```
Warning: "continue" targeting switch is equivalent to "break". Did you mean to use "continue 2"? in /www/wwwroot/xp.daniao.org/lib/G/functions.php on line 254
```

1. 根據提示找到：“`/www/wwwroot/xp.daniao.org/lib/G/functions.php`”
2. 並將第254行的`continue`改爲`continue 2`

看圖：

![btchevereto5min.png](https://tupian.clotliu.com/8c367c13bf117d457a379eadcb744053.png)

保存之後，刷新安裝頁面即可。安裝成功截圖：

![btchevereto6min.png](https://tupian.clotliu.com/85e853d25a609ded2d35ddbe6be00fc0.png)

#### 6、設置爲中文

登錄後台：`dashboard/settings/languages`  然後這位簡體中文即可，如圖：

![btchevereto7min.png](https://tupian.clotliu.com/4b1c288c23836380626f82568ea3304d.png)

#### 7、特色的功能

通過安裝我們的上傳插件，將圖像上傳到您的網站，博客或論壇。 它提供圖像上傳到任何網站，放置一個按鈕，將允許您的用戶直接上傳圖像到我們的服務，它將自動處理插入所需的代碼。 所有功能包括拖放，遠程上傳，圖像調整大小等。

![btchevereto8min.png](https://tupian.clotliu.com/de238f2dddee36dba38bc145df6471a7.png)

#### 8、最後

圖床非常給力，雖然是免費版但是功能上也足夠驚豔了，如果是商業版本還支持第三方直接登錄和硬盤的擴展。但是個人用個免費版本也是足夠了。

**提示**：建議關閉寶塔nginx防火牆，批量上傳時容易觸發cc防禦進而封禁IP  或者把cc的規則設置的更爲寬松一點。
	