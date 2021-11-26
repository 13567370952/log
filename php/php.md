
## 21-11-09
### 移除空值
```php
<?php

$array = [0,1,'','2',''];
$return_array = array_filter($array, function ($value) {
    return $value === '' ? false : true;

});
print_r($return_array);


## 输出Array ( [0] => 0 [1] => 1 [3] => 2 ) 

```


## 21-11-09
### 读取文件内容
```php
<?php

function tail($fp, $n, $base = 5){
    assert($n > 0);
    $pos = $n + 1;
    $lines = array();
    while (count($lines) <= $n) {

        try {
            fseek($fp, -$pos, SEEK_END);
        }catch (Exception $e) {
            fseek(0);
            break;
        }

        $pos *= $base;

        while (!feof($fp)) {
            array_unshift($lines, fgets($fp));
        }

    }

    return array_slice($lines, 0, $n);

}

var_dump(tail(fopen("D:\\txt\\2.txt", "r+"), 10));
```

## 21-11-26
### 发送邮件问题
```php
// 解决filter_var(): explicit use of FILTER_FLAG_SCHEME_REQUIRED is deprecate问题
// 场景：邮箱发送验证码类在php7.3.21 环境中报错：
// 原因：php7.3+弃用了FILTER_FLAG_SCHEME_REQUIRED函数
// 解决方式： PHPMailer.php 3599行 修改url地址的正则验证
    if (filter_var('http://' . $host, FILTER_VALIDATE_URL, FILTER_FLAG_HOST_REQUIRED)) {
            //Is it a syntactically valid hostname?
            return true;
}
修改为
    if (preg_match('/http:\/\/[\w.]+[\w\/]*[\w.]*\??[\w=&\+\%]*/is','http://' . $host)) {
            //Is it a syntactically valid hostname?
            return true;
}
```