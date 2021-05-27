# JS

## Variables: 

可以在浏览器中打开 JS 控制台，在其中输入一些代码。比如定义一些变量进行运算等等。

在命令后面接冒号，可以在后面继续接命令。即在一行中输入多条命令，与 Linux 终端类似。

`prompt()`：弹出一个对话框，其中有文本框，可以向其中输入文本。

`var name = prompt()`弹出对话框之后，在文本框中输入 Will ，关闭对话框。在控制台下一行输入 name 回车，可知将刚刚输入的 Will 赋给了 name 。

`var name = prompt(); alter(name)`：在弹出的对话框中输入 Will，确认之后会弹出一个 Will 的提示框。

`var name = prompt(); var lastname = prompt(); alert(name + ', ' + lastname)`：先输入 name，再输入 lastname ，然后提示将其以字符串的形式连接。

`var name = prompt('What's your name? ')`：在对话框中显示`What's your name? `。

## If Else & Comparison Operators

```js
// 弹出 you can drive! 
var age = 16;
if (age < 16) {
    alert('you can not drive');
}
// 可以使用 else 代替。★
if (age >= 16) {
    alert('you can drive! ');
}

// 改变年龄
age = 15;

// 再次使用上述 if 语句块
// 此时会在浏览器中弹出 you can not drive 。★
```

> 控制台中换行，按 Shift + Enter ( Windows ) 或者 Ctrl + Enter ( MacOS ) 。

```js
// 使用 Escape ( \ ) 转义单引号，或者使用双引号表示字符串，以在字符串内使用单引号。★
alert('you can\'t drive');
```

> 感叹号读作 shout 。★

## Functions: 

在控制台写 JS 代码有点傻屄，我们在文本编辑器上写（Sublime Text）。★

> 建议：一定要把`<script>`标签紧跟在`</body`标签上面，即整个页面代码的最后，否则会先执行 JS 代码，再显示页面。★

从外部导入 JS 文件：

```html
<script src="scripts/main.js"></script>
<!--可以导入多个文件，它们会依次执行。★-->
<script src="scripts/main2.js"></script>
<script src="scripts/main3.js"></script>
<script src="scripts/main4.js"></script>
```

### 定义函数：

```js
// 定义函数：
function go() {
    alert('hi');
    alert('hey there');
}

// 使用函数：
go();
go();
```

### 传递参数：

```js
// 因为 JS 是弱类型语言，所以不需要指定参数类型。★
function go(name, age) {
    alert(name);
    alert(age);
}

go('Will', 34);


// 上述代码等价于：
// 但是不建议那么做，因为编程讲究 DRY Code (Do not Repeat Yourself)，上面那段代码可以传递不同的 name 和 age 。★★
var name = 'Will';
var age = 34;

function go() {
    alert(name);
    alert(age);
}

go();
```

### 有返回值的函数：

> 为什么我们在第一节课讲的`prompt()`可以将输入的值赋给 name ，就是因为它有返回值。★

举例：

```js
function add(first, second) {
    return first + second;
}

// 这里先执行 add() ，因为 JS 知道先要执行内部的函数才能知道要 alert() 什么。★
alert(add(1, 2));
```

### 另一个变量类型 ( undefined ) ：

> 如果定义了一个变量，但是不给他赋值，就使用它，那么该变量的类型就是 undefined ，除非之前定义过。★

```js
var a; 
// 此时浏览器弹窗内容为 undefined 。★
alert(a);
```

> 所有的函数都返回 undefined ，除非定义了返回值。★