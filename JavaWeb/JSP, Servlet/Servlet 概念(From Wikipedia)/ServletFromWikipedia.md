# Servlet（From Wikipedia）

从实现上讲，Servlet 可以响应任何类型的请求，但绝大多数情况下只用来扩展基于 HTTP 协议的 Web 服务器。

## 工作模式：

- 客户端发送请求至服务器
- 服务器启动并调用Servlet，Servlet根据客户端请求生成响应内容并将其传给服务器
- 服务器将响应返回客户端
- 其他

## 生命周期

Servlet 被部署到应用服务器（应用服务器中用于管理Java组件的部分被抽象为**容器**）中以后，由容器控制 Servlet 的生命周期。

除非特殊指定，否则在容器启动的时候，servlet是不会被加载的，servlet只会在第一次请求的时候被加载和实例化。

servlet一旦被加载，一般不会从容器中删除，直至应用服务器关闭或重新启动。但当容器做存储器回收动作时，servlet有可能被删除。也正是因为这个原因，第一次访问servlet所用的时间要大大多于以后访问所用的时间。

![Life of a JSP File](F:\Note\JavaWeb\Servlet\Life of a JSP File.png)

## 与JSP的关系

Java服务器页面（[JSP](https://zh.wikipedia.org/wiki/JSP)）是HttpServlet的扩展。由于HttpServlet大多是用来响应HTTP请求，并返回Web页面（例如[HTML](https://zh.wikipedia.org/wiki/HTML)、[XML](https://zh.wikipedia.org/wiki/XML)），所以不可避免地，在编写servlet时会涉及大量的HTML内容，这给servlet的书写效率和可读性带来很大障碍，JSP便是在这个基础上产生的。

JSP的功能是使用HTML的书写格式，在适当的地方加入Java代码片段，将程序员从复杂的HTML中解放出来，更专注于servlet本身的内容。

JSP在首次被访问的时候被应用服务器转换为servlet，在以后的运行中，容器直接调用这个servlet，而不再访问JSP页面。

JSP的实质仍然是servlet。★





















