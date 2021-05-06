# JS（from MDN）

## JS 第一步：

## 脚本调用策略

为了避免在加载 html 完成之前 JS 就加载完毕（会导致错误），使用如下方法：

```javascript
// 内部 JS
<script>
    document.addEventListener("DOMContentLoaded", function() {
    . . .
    });
</script>

//外部 JS
<script src="script.js" async></script>
```

建议使用 async 属性，即使用外部 JS 的方法。这样既简洁，性能也高。如果使用传统的将 `<script>`标签方在`<body>`标签之前，或者使用`DOMContentLoaded`的方法，会在所有的 html DOM 加载完毕之后才加载 JS，这对于有些有大量 JS 代码的网站效率低下。★

### async 和 defer

（在`<script>`标签中）如果脚本执行不需要顺序，且不相互依赖，使用 async；否则使用 defer 。

## 注释

注释可以为`/**/`，也可为`//`：

```js
// 这是单行注释

/*
  这是
  多行注释
*/
```

## 像程序员一样思考

学习编程，难的不是语法，而是如何应用它来解决现实世界的问题。像程序员一样思考，包括了解你程序运行的目的，为达到该目的应选定的代码类型，以及如何使这些代码协同运行。为达成这一点，我们需要努力学习编程，获取语法经验，注重实践，再加一点创造力，几项缺一不可。代码写的越多，就会完成的越优秀。

## 常用方法

`Number();`：确保方法中的值是一个数字。

`.focus();`：将表单中（`<label>标签`）文本域的值清空，并将光标放置在该位置。

## 一些属性

`disabled`：可以将 disabled 属性设置为 true 来禁用一些标签，设置为 false 来解禁。

## 函数

可以在控制台（浏览器中按 F12 或者右键，检查）运行函数。

## 运算符

JavaScript 中的比较运算符（等于与不等于）与其他语言不大相同：★

| 运算符 |              名称              | 其他语言（Java, C, C++等） |
| :----: | :----------------------------: | :------------------------: |
|  ===   | 严格等于（它们是否完全一样？） |             ==             |
|  !==   |  不等于（它们究竟哪里不一样）  |             !=             |

## 常量与变量

使用关键字 let （旧版中为 var ）来创建变量；const 创建常量，常量可以用来保存对界面元素的引用，界面元素的文字可能会改变，但引用是不变的。★

### 关于 let 关键字

从其他语言中借用，在数学中，习惯说 `let x be 10`，即 `let x = 10;`。

#### let 与 var

let 为块作用域，只在声明块或子块中可用。而 var 作用域是整个封闭函数：

```js
function varTest() {
    var x = 1;
    {
        var x = 2; // 同样的变量！
        console.log(x); // 2
    }
    console.log(x); // 2
}

function letTest() {
    let x = 1;
    {
        let x = 2; // 不同的变量
        console.log(x); // 2
    }
    console.log(x); // 1
}
```

在程序和方法的最顶端，var 声明会给全局对象新增属性，而 let 不会：

```js
var x = 'global';
let y = 'global';
console.log(this.x); // "global"
console.log(this.y); // undefined
```

建议多使用 let 。

### 变量提升

变量声明或其他声明总在任意代码执行之前进行处理，所以即使将声明写在赋值后面，也是可以的。

```js
bla = 2;
var bla;
// ...

// 可以隐式地（implicitly）将以上代码理解为：

var bla;
bla = 2;
```

重要的是，提升将影响变量声明，而不影响其值的初始化。★

```js
function do_something() {
	console.log(bar); // undefined
	var bar = 111;
	console.log(bar); // 111
}

// is implicitly understood as:
function do_something() {
	var bar;
	console.log(bar); // undefined
	bar = 111;
	console.log(bar); // 111
}
```

## 事件

浏览器中发生的事，如：点击按钮、加载页面、播放视频等。

### 事件监听器（Event Listener）：

侦听事件发生的结构。

### 事件处理器（Event Handler）：

响应事件触发而运行的代码块。

---

注意，addEventListener() 中作为参数的函数名不加括号：★

```js
// checkGuess() 函数不加括号
guessSubmit.addEventListener('click', checkGuess);
```

## 浅谈对象

JS 中一切都是对象，对象是存储在单个分组中的相关功能的集合。

可以自定义对象，那是比较高级的内容。现在浏览器内置的对象就差不多够用了。

```js
// 在页面加载完成后自动将光标放置到 input 输入框中，提高游戏体验。
guessField.focus();
```

向`querySelector()`方法传入选择器，选中需要引用的元素，可以访问一系列属性和方法。（存储于对象内部的基础变量与函数。）

## 操作浏览器对象

1. 在控制台中打开你的程序。
2. 打开浏览器开发工具，切换到 JS 控制台标签页。
3. 输入一些代码。

页面上每个元素都有一个 style 属性，它本身包含一个对象，其属性包含应用于该元素的所有内联 CSS 样式，让我们可以用 JS 在元素上动态设置新的 CSS 样式。
