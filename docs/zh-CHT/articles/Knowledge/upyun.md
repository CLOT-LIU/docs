# 注冊又拍雲賬號

點擊 <a href="https://console.upyun.com/register/?invite=B1K7kNtvt"  target="_blank">這裏</a> 即可注冊又拍雲賬號。

> 已有賬號可忽略。另外，建議加入 <a href="https://www.upyun.com/league"  target="_blank">又拍雲聯盟</a>，申請通過後每年都有代金券發放，個人使用完全足夠，不然使用前請注意余額。
> 
> 因爲關于又拍雲存儲設置的文章只有一篇幾年前的，所以在此教程基于 <a href="https://bbs.halo.run/u/ryanwang"  target="_blank">@Ryan Wang</a> 大佬的文章 <a href="https://bbs.halo.run/d/150"  target="_blank">又拍雲存儲設置教程</a> 進行的了修改和更新。(按本教程基本上是沒有啥問題的......大概吧:🧐:)

# 新建雲存儲

![1636542462](https://tupian.clotliu.com/0354560ac6154ee18570ae2bc8aa2ff2.jpg)

![1636539766-650163-apb09zgiysq7uydhzvo](https://tupian.clotliu.com/fb6cf308e80bcc4f4c376f182e345ea7.png)
> 注意：第一次使用需要新建一個操作員，權限全勾上。應用場景選擇網頁圖片即可。

# 綁定域名

![Snipaste_2019-07-20_12-21-11.jpg](https://i.loli.net/2019/07/20/5d3296c6a654743117.jpg)

![Snipaste_2019-07-20_12-22-06.jpg](https://i.loli.net/2019/07/20/5d3296fca0f5f83331.jpg)

> 綁定之後還不能用，還需要在服務器添加解析

![1636540297-512652-image](https://tupian.clotliu.com/00b2e77d18424820c7d37f17024635fc.png)

![1636540342-689871-image](https://tupian.clotliu.com/822aa86438ba381789f339914b55c6cf.png)

# 縮略圖策略

我們需要新建一個縮略圖策略以供博客後台展示所用。

![1636540810-274621-image](https://tupian.clotliu.com/0caaa97a401d89e883c4390b936cd3b2.png)

> 記住這個間隔標識符，這是用于標識處理後的圖片的，在圖片鏈接末尾加上間隔標識符+圖片處理版本名即可。

![1636540910-245473-image](https://tupian.clotliu.com/f9e2372f79ff942978af69fd069379e8.png)

> 新建圖片處理 - 自定義版本

![1636540986-893655-image](https://tupian.clotliu.com/9dff32715067df9c92f3c57f6010f0f1.png)

> 版本名稱自己設置就好，縮略方式建議限定寬度和高度。完了保存即可。

# Halo 後台設置

![1636541922-154535-m-at-htf4sza3fja-at-705l](https://tupian.clotliu.com/8d7281743f28b00730c120bd17bddf3e.png)

1. 存儲位置選擇又拍雲
2. 域名填寫自己在又拍雲綁定的域名即可，主要有沒有 https，如果需要 https，自己去又拍雲申請一個綁定到這個域名就行了。

![1636541100-864849-image](https://tupian.clotliu.com/cd6da8d752d304fcce67b447ee8d2ef3.png)

![1636541144-112295-image](https://tupian.clotliu.com/3fce0155d67bdc5fd5b81cf3247077e1.png)

![1636541172-646532-image](https://tupian.clotliu.com/3ba592bba4853f56290234d5d1673be9.png)

會跳到以下界面(大概吧:🧐:)，如果不對就打開這個網站`https://console.upyun.com/toolbox/ssl/`

![1636541336-323111-image](https://tupian.clotliu.com/f29176e3ca5304d139511053db3c3873.png)

申請好或是上傳好自己的證書之後可以在下面的位置查看

![1636541565-788120-image](https://tupian.clotliu.com/2b39f2c27b1c8d91cba65025b4735567.png)

![1636541587-575611-image](https://tupian.clotliu.com/e63fe4c99fb5d56d152a46cf9d63ae4a.png)

可以在這裏打開打開 `HTTPS 訪問`和 `強制 HTTPS`

3. 空間名稱即你新建的存儲空間名稱。
4. 操作員名稱和密碼選擇新建雲存儲空間的時候的即可。
5. 文件目錄自定義。
6. 縮略圖處理策略即 `間隔標識符+圖片處理版本名稱`。

# 最後

去附件管理上傳圖片試試吧！
