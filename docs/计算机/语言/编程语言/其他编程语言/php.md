# PHP

PHP（Hypertext Preprocessor）超文本预处理器,是一种通用开源脚本语言。  

PHP 文件可包含文本、HTML、JavaScript代码和 PHP 代码
PHP 代码在服务器上执行，结果以纯 HTML 形式返回给浏览器
PHP 文件的默认文件扩展名是 ".php"

PHP 脚本可以放在文档中的任何位置。
PHP 脚本以 <?php 开始，以 ?> 结束

```php
<?php
//php代码

//单行注释

/*多行
注释
*/

?>
```

---

## PHP 变量

命名规则：

- 变量以 $ 符号开始，后面跟着变量的名称
- 变量名必须以字母或者下划线字符开始
- 变量名只能包含字母、数字以及下划线（A-z、0-9 和 _ ）
- 变量名不能包含空格
- 变量名是区分大小写的（$y 和 $Y 是两个不同的变量）

### 申明变量

PHP 没有声明变量的命令。*变量在您第一次赋值给它的时候被创建。*

```php
<?php
$txt="Hello world!";
$x=5;
$y=10.5;
?>
```

PHP 是一门弱类型语言，不必向 PHP 声明该变量的数据类型。PHP 会根据变量的值，自动把变量转换为正确的数据类型。

### PHP 变量作用域

变量的作用域是脚本中变量可被引用/使用的部分。

PHP 有四种不同的变量作用域：

1. local
2. global
3. static
4. parameter

@在所有函数外部定义的变量，拥有全局作用域。除了函数外，全局变量可以被脚本中的任何部分访问，要在一个函数中访问一个全局变量，需要使用 global 关键字。
当一个函数完成时，它的所有变量通常都会被删除。然而，有时候您希望某个局部变量不要被删除。要做到这一点，请在您第一次声明变量时使用 static 关键字@

---

## PHP 输出语句

### PHP echo语句

可以输出一个或多个字符串，没有返回值，echo 输出的速度比 print 快

字符串可以包含 HTML 标签

### PHP print 语句

只允许输出一个字符串，返回值总为 1

### PHP EOF(heredoc)

PHP是一个Web编程语言，在编程过程中难免会遇到用echo来输出大段的html和javascript脚本的情况，如果按字符串输出的话，肯定要有大量的转义符来对字符串中的引号等特殊字符进行转义，以免出现语法错误。

1.PHP定界符的作用就是按照原样，包括换行格式什么的，输出在其内部的东西；
2.在PHP定界符中的任何特殊字符都不需要转义；
3.PHP定界符中的PHP变量会被正常的用其值来替换。

1. 必须后接分号，否则编译通不过。
2. EOF 可以用任意其它字符代替，只需保证结束标识与开始标识一致。
3. 结束标识必须顶格独自占一行(即必须从行首开始，前后不能衔接任何空白和字符)。
4. 开始标识可以不带引号或带单双引号，不带引号与带双引号效果一致，解释内嵌的变量和转义符号，带单引号则不解释内嵌的变量和转义符号。
5. 当内容需要内嵌引号（单引号或双引号）时，不需要加转义符，本身对单双引号转义，此处相当与q和qq的用法。

1.以 <<<EOF 开始标记开始，以 EOF 结束标记结束，结束标记必须顶头写，不能有缩进和空格，且在结束标记末尾要有分号 。

2.开始标记和结束标记相同，比如常用大写的 EOT、EOD、EOF 来表示，但是不只限于那几个(也可以用：JSON、HTML等)，只要保证开始标记和结束标记不在正文中出现即可。

3.位于开始标记和结束标记之间的变量可以被正常解析，但是函数则不可以。在 heredoc 中，变量不需要用连接符 . 或 , 来拼接，如下：

```php
<?php
$name="runoob";
$a= <<<EOF
        "abc"$name
        "123"
EOF;
// 结束需要独立一行且前后不能空格
echo $a;
?>
```

## PHP 表单

PHP 中的 `$_GET` 和 `$_POST` 变量用于检索表单中的信息

> `$_GET` 变量接受所有以get方式发送的请求，及浏览器地址栏中的 ? 之后的内容。
> `$_POST` 变量接受所有以post方式发送的请求，例如，一个form以method=post提交，提交后php会处理post过来的全部变量。
> `$_REQUEST` 支持两种方式发送过来的请求，即post和get它都可以接受，显示不显示要看传递方法,get会显示在url中（有字符数限制）post不会在url中显示，可以传递任意多的数据（只要服务器支持）。

### PHP 表单处理

当处理 HTML 表单时，PHP 能把来自 HTML 页面中的表单元素自动变成可供 PHP 脚本使用

html表单：

```html
<html>
<head>
<meta charset="utf-8">
<title>表单</title>
</head>
<body>
 
<form action="welcome.php" method="post">
名字: <input type="text" name="fname">
年龄: <input type="text" name="age">
<input type="submit" value="提交">
</form>
 
</body>
</html>
```

php文件：

```php
欢迎<?php echo $_POST["fname"]; ?>!<br>
你的年龄是 <?php echo $_POST["age"]; ?>  岁。
```

### 表单验证

应该尽可能的对用户的输入进行验证（通过客户端脚本）。浏览器验证速度更快，并且可以减轻服务器的压力。

如果用户输入需要插入数据库，应该考虑使用服务器验证。在服务器验证表单的一种好的方式是，把表单的数据传给当前页面（异步提交的方式更好），而不是跳转到不同的页面。这样用户就可以在同一张表单页面得到错误信息。用户也就更容易发现错误了。

---

## PHP 数据库

通过 PHP，您可以连接和操作数据库，MySQL 是跟 PHP 配套使用的最流行的开源数据库系统。