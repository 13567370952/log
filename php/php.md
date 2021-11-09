
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
