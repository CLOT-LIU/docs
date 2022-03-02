#### 1、購買

官網：[https://chevereto.com/](https://chevereto.com/)

打開官網即可看見活動，目前的活動是20% OFF，0.8折的優惠還是值得入手的。

#### 2、登錄下載

控制台：https://chevereto.com/panel

![chevereto3network1.png](https://tupian.clotliu.com/76e1b6d0ae287fd38677d774a294262a.png)

#### 3、下載最新版

這裏簡單說下，安裝分兩種，一種就是你下載（installer）一個單PHP文件，因爲我沒試過，可能需要你輸入序列號，是通過github下載程序，國內安裝速度很慢。

也可以直接下載最新版本的程序包，安裝速度快，不需要輸入序列號，默認就已經是商業版本了。

![chevereto3network2.png](https://tupian.clotliu.com/7eb336343d18cdf5d9f297db29e1fafb.png)

#### 4、安裝准備

大鳥搭建的環境是用寶塔面板，具體如下：

（1）寶塔面板（寶塔服務器面板，一鍵全能部署及管理，送你3188元禮包，[點我領取](https://www.bt.cn/?invite_code=MV96YnVvdHU=)）

（2）nginx1.18

（3）mysql5.7

（4）phpmyadmin4.7

（5）PHP7.4

#### 5、下載以及安裝前的設置

**（1）程序下載**

你購買之後登錄控制台下載最新程序，這裏可以看第三步。

**（2）新建站點**

寶塔新建站點，不在贅述。

**（3）上傳程序**

把下載好的程序包上傳到你網站根目錄，之後解壓，寶塔是支持在線解壓的，你上傳程序包即可，不需要解壓好用ftp工具上傳。

**（4）設置nginx規則**

把程序包自帶的已經被你放置到網站根目錄中的nginx.txt內的配置規則添加到網站的配置文件 server {} 裏面，保存並重啓nginx。

如果你是apache那麽請找Apache.txt，並複制裏面的內容，到網站配置中。既然是放置在server {} 那麽，你可以直接把nginx.txt裏面的內容都放在僞靜態設置中，也是可以的。看圖：

![chevereto3network30.png](https://tupian.clotliu.com/b8e22d4a229ee0a171c6a463880bc395.png)

#### 5、安裝

浏覽器打開域名開始安裝。

**（1）連接數據庫**

![chevereto3network4.png](https://tupian.clotliu.com/b9c6118112cd888e5b2ee018dbb43a42.png)

**（2）設置管理員等**

![chevereto3network5.png](https://tupian.clotliu.com/93d3ce662561172124d5b4a1e3969989.png)

提交後即可完成安裝。

#### 6、簡單設置

**（1）設網站tdk**

![chevereto3network6.png](https://tupian.clotliu.com/c4774e867cc1e9cd9b4c3c31ba5864f1.png)

**（2）設置webp圖片上傳**

寶塔面板用戶，直接開啓即可支持webp格式上傳，無需其他設置。

![chevereto3network7.png](https://tupian.clotliu.com/d4534f03cfbf88fdd150934a9b94c9db.png)

![chevereto3network8.png](https://tupian.clotliu.com/83457605f3e27277948ee5e96a3be6e9.png)

**（3）啓用郵件驗證**

如果你要注冊啓用郵件驗證，具體看圖設置：

![chevereto3network9.png](https://tupian.clotliu.com/2d55066a2fe197bdaf30af6f0f29e715.png)

注意：SMTP密碼寫api密碼，不是你的登錄密碼。

**（4）外部存儲**

![chevereto3network31.png](https://tupian.clotliu.com/c9dba29aadcc89768f65e1346d04aa9a.png)

#### 7、最後

用寶塔面板來部署還是很簡單的，而且webp開啓也很容易，不會有多余的設置。

圖片需要開啓鑒黃，不然，後果你懂的。

收費版支持wepb格式圖片上傳，支持外部存儲等。

chevereto圖床的顔值是真的不錯的，看起來賞心悅目。
