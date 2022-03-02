# 介紹

h5ai可以把對應目錄下的文件和文件夾全部顯示在web頁面上，只需點擊即可下載對應的資料

h5ai需要php5.5版本以上環境，可在apache、nginx環境下運行，這裏還是直接用寶塔安裝就OK

**下載h5ai：[點擊下載](https://release.larsjung.de/h5ai/h5ai-0.30.0.zip)**

**Github：~​~​[https://github.com/lrsjng/h5ai](https://github.com/lrsjng/h5ai)**

# 方法：

寶塔後台添加站點，用你自己的域名或IP都可以：

![3226207728.png](https://tupian.clotliu.com/7296252f83fbcfcacb8c88386f6b5567.png)

站點添加完成後將根目錄下所有文件刪除，並上傳解壓後的 **_h5ai** 文件夾，如下圖

![2869875154.png](https://tupian.clotliu.com/4941743664772b2d48ae6a80ce628967.png)

然後修改 **寶塔後台 - 網站 - 設置 - 默認文檔**，全部刪除替換成下面的代碼然後點擊添加：

```
index
index.html
index.php
/_h5ai/public/index.php
```

示例圖：

![254645309.png](https://tupian.clotliu.com/ee3ffe00ab011f211be3fb4079069c8e.png)

OK，完成，搭建其實很簡單，現在打開域名即可使用賬戶密碼登錄

默認用戶名：**admin**

默認密碼：**admin**

如果要取消登錄驗證就將 **_h5ai / public / index.php** 裏第二行 **include 'login.php'** 刪除即可

如果要修改用戶名和密碼在 **_h5ai / public / login.php**

上傳或下載文件到網站根目錄就可以在 **web** 頁面顯示出來，也可以建立新的文件夾

**如果打開網頁出現以下錯誤：**

```
Warning: putenv() has been disabled for security reasons in
```

原因：禁用了部分存在危險的PHP函數

解決方法：

打開PHP配置文件：找到**disable_functions**字符串，將後面的**putenv**刪除，然後重啓PHP即可；
