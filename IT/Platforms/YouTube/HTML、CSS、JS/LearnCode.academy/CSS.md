# CSS

在 HTML 文件中的 `<head>`标签内，`<style>`标签中。

## Target Tags（用于定位某个具体的标签，便于分开、精细控制。）

可以为标签添加 class 或者 id 属性来指定标签。一般使用 class 就够了。★

标签只能拥有不同的 id ，拥有相同的 id 是不合法的，HTML 不支持。虽然在 chrome 上看似可以，但换个浏览器就不知道会发生什么情况了。★

使用 class 指定标签：`空格`表示指定该标签的子标签；`逗号`表示并列；`点`表示当前标签的某个类，如果该类唯一，标签可以省略；`冒号`可以指定每一个该标签中的某一个子元素等等：

```css
<style>
	/* 指定该标签中的某个子标签 */
	section div {
		. . .
	}
	
	/* 并列 */
	section, header P{
		. . .
	}
	
	/* 指定该标签的某个类 */
	(section).feature-box {
		. . .
	}
	(section).feature-box a {
		. . .
	}
	(section).feature-box b {
		. . .
	}
	
	/* 指定每一个该标签中的某个子元素 */
	div:first-child {
		. . .
	}
	div:last-child {
		. . .
	}
</style>

<header>header</header>
<section class="feature-box a">
	<div>a</div>
	<div>b</div>
	<div>c</div>
</section>
<section class="feature-box b">
	<div>d</div>
	<div>e</div>
</section>
<footer>footer</footer>
```

## 改变该标签的样式

CSS 有太多属性，你不需要全部都记住，有些并不常用。你只需要知道常用的就行了，如果遇到不知道的，并不代表你不是一个开发者。即使是学会了，过个 6 个月，1年不用也会忘记。遇到不知道的，谷歌，了解一下，忘了再谷歌，这就是学习开发的过程。

好的设计师都是从细节出发。

`display`：改变该盒子的类型（ inline、block、inline-block 等 ）。

`flex-direction：row`：flex 的方向。

`background-image`：插入图片：

```css
selector {
	background-image: url("图片路径");
}
```

---

`background-size`：背景大小。（100% 表示永远占 100% 的宽度。）

`background-repeat: no-repeat`：使背景不要重复出现。

`background-position: center;`：一直聚焦在图片中间。

`text-align: center`：将文本居中。

`text-decoration`：调整字体的装饰（下划线、上划线、波浪线及其颜色等）。	

`text-shadow`：为文本设置阴影。

`text-transform: uppercase;`：将字母转换为大写。

`color`：字体颜色。

`font-size`：字体大小。

`width`：宽度。

`height`：高度。

`font-family`：全局字体。

`margin`：边缘。（盒子外部）

`padding`：填充。（盒子内部）

`border`：边界。（盒子边界）

`border-radius: 50%;`：变成圆。

`box-shadow`：给盒子添加阴影。

`positon`：改变位置。

`list-style-type: none;`：将列表中条目的前面表示列表的标记去掉。

### 改变图片：

img 标签中的 srcset 属性：仅改变图片大小。

`<picture> 标签`：可以做一些不同的事情，比如改变图片的形状。

### 使盒子上移：

1. `position: relative;` relative 表示相对的，相对于原来的位置而言。当然还有 absolute、fixed 等等。
2. `top: -40px;` 距离原位置的上方 -40px 。

### 满足一定条件后执行：（用于设计不同设备下访问网页，即在不同的屏幕尺寸下，你的网页也需要有可观性）

```CSS
/* ()中为要满足的条件，满足后执行 {} 中的语句。{} 中为要改变的样式，即 CSS 代码。 */
/* max-width 为当前条件，表示屏幕的最大宽度为800px，如果超过了这个宽度，则不满足条件，不执行 {} 中的语句。 */
/* 同理，min-width: 800px 表示最小宽度为800px，若比该宽度还小，则不满足条件。*/
@media screen and (max-width: 800px) {
	. . .
}

/* 可以在一条语句中使用多个条件 */
@media screen and () and () {
    . . .
}
```

在进行电脑和移动端的不同情况的样式设计时，可以让其中一个模块不显示：

```css
/* 在电脑上访问该页面，将 .mobile 的内容隐藏 */
header .mobile {
	display: none;
}

/* 当屏幕宽度小于 715px 时，展示 .mobile 的内容，隐藏 .desktop 的内容 */
@media screen and (max-width: 715px) {
	header .mobile {
		display: inline-block;
	}
	header .desktop {
		display: none;
	}
}
```

flex 样式可以自动根据屏幕的尺寸收缩或展开：★

```css
flex-warp: warp;
```

## 一些思想

设计网页时你不能去找一些适合手机、平板、电脑阅读的分界点来设计不同尺寸的设备访问你的页面的样式，因为当今社会完全可能会有任何尺寸的设备来访问。所以我们要考虑的应该是在什么尺寸下我们的网页不能正常的显示，然后在此尺寸下进行改进，使其美观。这才是设计网页正确的思想。★

可以打开浏览器的开发者工具来确定在哪些地方需要改进你的网页，它会显示具体的像素值。★













