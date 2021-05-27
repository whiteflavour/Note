# Vim 快捷键 (2021.3.21 —— )

## 插入：

Shift + o （大 o）：从该行的上一行插入。

Shift + i （大 i）：从行首插入。

Shift + a （大 a）：从行尾插入。

## 剪切（删除）：

db ：往后删除一个单词。

cc ：剪切该行，并进入插入模式（与 dd 的区别）。

## 移动：

Ctrl + o ：光标返回上一次的地方。★

Ctrl + i 或 ``：回到 Ctrl + o 的地方。

Shift + h ：将光标移到当前页面的第一行。

Shift + l ：将光标移到当前页面的最后一行。

Shift + m ：将光标移到当前页面的中间。

## 连接：

Shift + j (大 j ）：将下一行移动到本行（连接这两行）。

3 J ：连接下面三行。

## 粘贴

Shift + p ：在该行的上一行或者光标的前面粘贴。★

## 区域控制：

From: 

https://blog.csdn.net/topgun_chenlingyun/article/details/48393277

https://blog.csdn.net/weixin_33788244/article/details/85885645

### 区域删除：

`di"`：删除`"`内的内容 ，i 表示 inside. 

`di{` ：删除`{`内的内容。 

... 

`dta`：从该字符删除到字符`a`位置，t 表示 to 。（不删除 a ）

... 

`dfa`：删除到直到找到 a ，f 表示 find 。（删除 a ）

...

### 区域更改：

`ci"`

...

### 区域复制：

`yi"`

...

### 区域选择：

`vi"`

...

