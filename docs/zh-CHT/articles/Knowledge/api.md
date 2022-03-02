# 前言

網上有很多隨機圖片 AIP，這些接口隨時都有可能挂掉，所以，我們可以自建一個屬于自己的隨機圖片 API

# 教程

新建一個 api.php 文件，在該文件內加入以下內容：

```php
<?php
$arr=file('picture.txt');
$n=count($arr)-1;
for ($i=1;$i<=1;$i++){
  $x=rand(0,$n);
  header("Location:".$arr[$x],"\n");
}
?> 
```


然後創建一個 picture.txt 文件，將圖片外鏈丟進去
最後，訪問 http://你的域名/api.php 測試 API 是否正常
