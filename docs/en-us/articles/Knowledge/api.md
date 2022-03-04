## Preface

There are a lot of random image AIPs on the web, these interfaces may hang at any time, so we can build a random image API of our own

## Tutorial

Create a new api.php file and add the following content to it: 

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


Then create a picture.txt file and drop the image external link into it
Finally, visit http:// your domain name /api.php to test if the API works
