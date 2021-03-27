# EL 问题

若 EL 失效，在 JSP Directive page 部分添加`isELIgnored="false"`。

From ： https://blog.csdn.net/weixin_42950079/article/details/102649892?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_baidulandingword-0&spm=1001.2101.3001.4242

---

> 若要使用 EL ，务必添加 `isELIgnored="false"`属性，否则各种报错：NumberFormatException 、for illegally input string ... 等。★