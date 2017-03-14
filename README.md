# PHP-Guide
PHP 学习笔记

## 语法说明
1. 作用域灵活，整个方法内随便用，会有覆盖
2. `empty` 方法，包含空值，无值以及0值的检测。 需要注意0值的判断，0值也认为是 `true`

0值包含以下这些：

```
"" (an empty string)
0 (0 as an integer)
0.0 (0 as a float)
"0" (0 as a string)
NULL
FALSE
array() (an empty array)
$var; (a variable declared, but without a value)
```

### 谨慎使用PHP的引用
<http://www.cnblogs.com/ider/archive/2012/09/06/php_reference_issue.html>
需要翻墙：<http://schlueters.de/blog/archives/141-References-and-foreach.html>

官方文档

> foreach

> (PHP 4, PHP 5, PHP 7)
> The foreach construct provides an easy way to iterate over arrays. foreach works only on arrays and objects, and will issue an error when you try to use it on a variable with a different data type or an uninitialized variable. There are two syntaxes:

> foreach (array_expression as $value)
>     statement
> foreach (array_expression as $key => $value)
>     statement
> The first form loops over the array given by array_expression. On each iteration, the value of the current element is assigned to $value and the internal array pointer is advanced by one (so on the next iteration, you'll be looking at the next element).

> The second form will additionally assign the current element's key to the $key variable on each iteration.

> It is possible to customize object iteration.

> Note:
> In PHP 5, when foreach first starts executing, the internal array pointer is automatically reset to the first element of the array. This means that you do not need to call reset() before a foreach loop.
> As foreach relies on the internal array pointer in PHP 5, changing it within the loop may lead to unexpected behavior.
> In PHP 7, foreach does not use the internal array pointer.
> In order to be able to directly modify array elements within the loop precede $value with &. In that case the value will be assigned by reference.

> <?php
> $arr = array(1, 2, 3, 4);
> foreach ($arr as &$value) {
>     $value = $value * 2;
> }
> // $arr is now array(2, 4, 6, 8)
> unset($value); // break the reference with the last element
> ?>
> Warning
> Reference of a $value and the last array element remain even after the foreach loop. It is recommended to destroy it by unset(). Otherwise you will experience the following behavior:
> <?php
> $arr = array(1, 2, 3, 4);
> foreach ($arr as &$value) {
>     $value = $value * 2;
> }
> // $arr is now array(2, 4, 6, 8)

> // without an unset($value), $value is still a reference to the last item: $arr[3]

> foreach ($arr as $key => $value) {
>     // $arr[3] will be updated with each value from $arr...
>     echo "{$key} => {$value} ";
>     print_r($arr);
> }
> // ...until ultimately the second-to-last value is copied onto the last value

> // output:
> // 0 => 2 Array ( [0] => 2, [1] => 4, [2] => 6, [3] => 2 )
> // 1 => 4 Array ( [0] => 2, [1] => 4, [2] => 6, [3] => 4 )
> // 2 => 6 Array ( [0] => 2, [1] => 4, [2] => 6, [3] => 6 )
> // 3 => 6 Array ( [0] => 2, [1] => 4, [2] => 6, [3] => 6 )
> ?>

### PHP文件上传
<http://www.w3school.com.cn/php/php_file_upload.asp>
<http://blog.csdn.net/niushuai666/article/details/6672808>

### PHP empty 使用（Can't use method return value in write context）
<http://blog.csdn.net/ggh19/article/details/27081147>

## Common

[PsySH](psysh.org)
REPL工具，实用。


