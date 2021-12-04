# Paste Queue

## AppleScript 与 正则表达式 的作用：

- **用 AppleScript 提取第一行：**提取第一行文本并且拷贝到剪贴板。AppleScript 也有删除文本的功能，但是它对于换行符号的处理不佳，会造成 Keyboard Maestro 无法对 AppleScript 处理过的文本正确分行，所以我们用下面的方法完成文本删除。
- **用正则表达式删除第一行：**删除的要求是只删用过的第一行，这个需求可以通过表达式 ^.*[nr] 完成，它表示「从文本开头到第一次换行」，也就是第一行，把这个表达式表示的内容替换成空白即是删除。这正则技巧来自 Keyboard Maestro 论坛上的一则讨论（[Remove the top line of a text file or variable](https://sspai.com/post/56648#)）。

参见：https://ljqo.blogspot.com/2020/04/keyboard-maestro.html

