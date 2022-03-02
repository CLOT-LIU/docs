## 前言

网上有很多随机图片 AIP，这些接口随时都有可能挂掉，所以，我们可以自建一个属于自己的随机图片 API

## 教程

新建一个 api.php 文件，在该文件内加入以下内容：

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


然后创建一个 picture.txt 文件，将图片外链丢进去
最后，访问 http://你的域名/api.php 测试 API 是否正常
