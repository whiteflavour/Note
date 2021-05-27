# 平时练习中遇到的问题及解决方案

在`alert();`函数中使用加法运算时，需要先将两个加数在`alert()`方法外面相加，在调用`alert()`方法，否则会以字符串的形式相加：

```js
// JS 控制台中的命令，在一行输入，这里换行方便观看。

/**
 *  在 alert() 方法内部相加
 */
 
// 这里输入 5
var string_a = prompt('Enter a number');
// 这里输入 6
var string_b = prompt('Enter another number'); 
var number_a = parseInt(string_a); 
var number_b = parseInt(string_b); 
// 这里的结果为 56
alert('The sum of them is ' + number_a + number_b);

/**
 *  在 alert() 方法外部相加
 */
 
 var string_a = prompt('Enter a number'); 
 var string_b = prompt('Enter another number'); 
 var number_a = parseInt(string_a); 
 var number_b = parseInt(string_b); 
 var number = number_a + number_b; 
 // 这里结果为 11
 alert('The sum of them is ' + number);
```

