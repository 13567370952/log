
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