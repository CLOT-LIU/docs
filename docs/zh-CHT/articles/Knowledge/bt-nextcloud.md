# 前言

當我們使用寶塔面板部署好後，可以直接使用，如果你還沒有部署Nextcloud，可以參考：

* [如何使用騰訊雲輕量服務器快速給自己搭建Nextcloud私人網盤？](https://cloud.tencent.com/developer/article/1787399?from=10680)

但是**管理員-設置-概覽**內，檢測一般會存在一些警告和錯誤，這些我們如何解決呢？

![j24e94yp7n.png](https://tupian.clotliu.com/e2e602aa260e1c3a4c7e1da060b34178.png)<center>管理員-設置-概覽</center>


![c3tk8feorv.png](https://tupian.clotliu.com/c80ab1efc200b4c5eea7a1dcef6459ab.png)<center>部分警告和錯誤</center>

# 通過HTTP訪問網站不安全。強烈建議您將服務器設置成要求使用HTTPS協議

這個問題最好解決，同時也可能是無法解決問題：

**服務器綁定域名，並配置**[**SSL證書**](https://cloud.tencent.com/product/ssl?from=10680)**，域名解析到服務器即可**

但是：

**國內服務器需要綁定備案的域名，若無備案域名，則只能使用IP訪問Nextcloud，那麽該條警告無法去除。**

# 一些文件沒有通過完整性檢查. 了解如何解決該問題請查看我們的文檔. (無效的文件列表… / 重新掃描…)

![t5880m76pp.png](https://tupian.clotliu.com/ac3c0d017803cb4406ae69b92a0f2b28.png)<center>“無效文件列表”錯誤</center>

![4u9yi6crqx.png](https://tupian.clotliu.com/c2f63e6c19d3d53f198d1e3005956fa0.png)<center>提示的無效文件</center>

你的無效的文件列表和我的可能不一樣，但是方法是一樣的：

1. 開nextcloud的安裝地址，也就是Nginx所代理的網站根目錄
2. 刪除“提示的無效文件“

![trcv85b1gj.png](https://tupian.clotliu.com/45fa318da17d89393cfe7b07080f0a8d.png)<center>Nextcloud目錄列表</center>

**如果你使用寶塔面板，可以進入寶塔面板後台，然後使用寶塔的圖形界面刪除無效文件**。如果你熟悉Linux命令，可以使用`rm`命令刪除：

![uwguxp4atr.png](https://tupian.clotliu.com/d1644ef9feb7d1baa18d0f66df610280.png)<center>rm命令刪除</center>

# PHP configuration option output_buffering must be disabled

其實這個很好解決，PHP默認是有4096字節緩衝的。但是Nextcloud希望你關閉。如果你是自己安裝的PHP，在你安裝PHP的路徑下，打開PHP配置文件（`php.ini`），將要
```
output_buffering = 4096
```
改爲：

```
; output_buffering = 4096
```

`;`爲PHP的注釋符號

如果你是寶塔安裝配置的php，更簡單了。在寶塔面板，依次打開：`軟件商店`-`已安裝`-`PHP7.3設置`-`配置文件`

查找文本`output_buffering`，並在前面加上`;`注釋

![s89meyztt9.png](https://tupian.clotliu.com/8adc1a8224bab3f5436e926accffaca9.png)<center>加上注釋</center>

之後，可能需要重載PHP配置或者重啓PHP服務才能生效。再次查看Nextcloud**概述**，就沒有這條警告了。

# 您的數據目錄和文件可以從互聯網直接訪問。.htaccess 文件不起作用。強烈建議您配置 Web 服務器，以便數據目錄不再可訪問，或者您可以將數據目錄移動到 Web 服務器文檔根目錄。

這個其實是Nginx的問題，爲了進一步提升安全性，我們打開Nginx網站設置

![mbj35fwywf.png](https://tupian.clotliu.com/96432e200026a2812aa95fe63ae925b5.png)<center>寶塔內網站Nginx設置</center>

**在location內的禁止訪問目錄內，加入data目錄。**

![l3a2yj5pnw.png](https://tupian.clotliu.com/5b4d392fdc9b949cbcfcd054ca8b5923.png)<center>加入data目錄</center>

# PHP 的安裝似乎不正確，無法訪問系統環境變量。getenv(“PATH”) 函數測試返回了一個空值

這個處理方法很簡單；如果你是自己安裝配置的PHP，一般不會出現這個問題，當時如果是使用寶塔安裝，一般都會有這個問題，解決方法很簡單：

在寶塔面板，依次打開：`軟件商店`-`已安裝`-`PHP7.3設置`-`FPM配置文件`

在文末添加：

```
env[PATH] = /usr/local/bin:/usr/bin:/bin:/usr/local/php/bin
```

![rcfwzicphp.png](https://tupian.clotliu.com/42a1f64a9a6c38d07659ebfe9375a793.png)<center>添加配置</center>

之後，可能需要重載PHP配置或者重啓PHP服務才能生效。

# 您的網頁服務器未正確設置以解析****。更多信息請參見文檔

這個處理方法很簡單，簡單地說，設置Nginx即可。如果你的Nginx是寶塔安裝的，那麽打開網站的Nginx：

![](https://tupian.clotliu.com/96432e200026a2812aa95fe63ae925b5.png)<center>打開Nginx設置</center>

之後追加以下內容：

```
rewrite /.well-known/carddav /remote.php/dav permanent;
rewrite /.well-known/caldav /remote.php/dav permanent;
```

![dkdmjhm1ne.png](https://tupian.clotliu.com/5b79ebb315cc080f520855e07cb8917c.png)<center>追加內容</center>

之後保存即可

# PHP模塊問題

PHP模塊問題包括：

1. 未找到PHP的"fileinfo"模塊。強烈推薦啓用該模塊，從而獲得更好的MIME類型探測結果。
2. **內存緩存未配置，爲了提升使用體驗，請盡量配置內存緩存。更多信息請參見文檔。**
3. PHP的OPcache模塊未載入。推薦開啓獲得更好的性能。

![xkgeob7hn8.png](https://tupian.clotliu.com/67e4c85f529a6e2abdf1bd02c0560ed1.png)<center>!PHP模塊問題</center>

安裝如下模塊：

![e71iy40d5f.png](https://tupian.clotliu.com/ea8b5955a52b74717ae1b11b36884317.png)<center>裝的模塊-01</center>安

![8rhu405as1.png](https://tupian.clotliu.com/965d1618c650ad6f82f776a9ebd16e13.png)<center>安裝的模塊-02</center>

同時，因爲使用`apcu`作爲緩衝，所以我們需要打開Nextcloud的配置文件，追加以下內容：


```
'memcache.local' => '\OC\Memcache\Redis',
  'redis' => array(
    'host' => 'localhost',
    'port' => 6379,
    ),
```