# Java Web —— 开始时间 2021.2

## 第一章： Java EE

### 新特性：

#### Java 7 新特性：

try-with-resources (带资源的 try 语句) 。

multi-catch (捕获多个异常) (使用 | 隔开) 。（但是不能捕获相互之间有继承关系的异常，因为这样的话直接捕获 父异常 即可）。

字节码 和 整数 的 二进制字面量 可以使用下划线分割。

字符串 可以作 swich 的参数了。

#### Java SE 8 ：

lambda 表达式：本质为 匿名函数 。★

lambda 表达式是非常有用的，尤其是在实现 单方法接口 时。★

```java
// 未使用 lambda 的写法
Thread thread = new Thread(new Runable() {
    @Override
    public void run() {
        // do something
    }
});

// 使用 lambda 表达式
Thread thread  = new Thread(() -> {
    // do something
});

// 与上面两个方法等价的方法
Thread thread = new Thread(this::doSomething);

public void doSomething() {
    // do something
}
```

### Web 应用程序的结构

#### Servlet、过滤器、与 JSP 的作用：

Servlet: 接受 和 响应 HTTP 请求的 Java 类。

过滤器: 用于 拦截 发送给 Servlet 的请求。（数据格式化、对返回的数据进行压缩、认证和授权）

JSP: Java EE 中最强大的工具。

#### 目录结构和 WAR 文件

**定义**：

JAR 文件：一个简单的 ZIP 格式 归档文件，其中包含了可被 JVM 识别的标准目录结构。

WAR 文件（Web 应用程序归档）：是 Java EE Web 应用程序对应的归档文件。★

---

没有专门的 JAR 文件格式，任何 ZIP 归档应用程序都可以创建和读取 JAR 文件。

---

**类文件 的存储位置**：

JAR 文件：应用程序根目录的相对路径。

WAR 文件：/WEB-INF/classes 。

---

WAR 文件的 根级别 的 /META-INF 目录并不在应用程序类路径上，所以 不能 使用 ClassLoader 获得该目录中的资源。

在不使用 过滤器 或 安全规则 时，Web 应用程序 中的资源几乎都可以使用 URL 访问，除了 /WEB-INF 和 /META-INF 中的文件，因为它们是 受到保护 的。★

#### 类加载器的架构

根据选择的服务器和需求来确定是使用 双亲委托优先模式（委托给上级）还是 子女委托优先模式（自己的满足需求就用自己的）。

你总是应该阅读已选择服务器的 文档，并决定改服务器的类加载架构是否符合要求。★

## 第二章：Web 容器

### 选择 Web 容器：

根据自己的组织项目的需求，来选择合适的容器。还必须考虑预算，因为通常商业应用服务器的价格很高。★

## 第三章：Servlet

### Servlet

Servlet 的协议是 HTTP （是目前 Java EE 7 支持的唯一协议）。

Servlet 中的各种 HTTP 方法详情：https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html （RFC-2616 规范）

一般不用主动去关闭 Web 容器创建的资源，如从 response 中获得的 PrintWriter 对象。我们只需要关闭自己创建的资源即可。★

### init() 与 destroy()

`init()`方法在 Servlet 构造完成之后调用，但在响应第一个请求之前。可以让该方法在 Web 服务器启动时就调用，即：使用`<load-on-startup>1</load-on-startup>`，1 表示第一个启动。

总是应该使用`destroy()`方法清理 Servlet 持有的资源，而不用等垃圾回收，垃圾回收在后来清理，并且如果提前使用垃圾回收，再使用`destroy()`方法的话，可能导致应用程序部分卸载或无法卸载。

### 学习方法

你应该从 Java EE 7 Oracle 官网上的 API 文档中查询可用的方法和它们的目的。★

### doGet、doPost 等方法

HTTP 协议的 RFC 规范不禁止在任何 HTTP 方法中查询参数，不过许多 Web 服务器都忽略通过 DELETE、TRACE 和 OPTIONS 传入的查询参数，在这些请求中使用查询参数是值得商榷的，所以最好不要在这些类型的请求中依赖于查询参数。

post 请求中的 post 变量 和 查询参数 尽管在 传输方式 上不同，但事实上是一样的，也表达了相同的信息。Servlet API 没有区分这两种类型的参数。无论参数是作为 查询参数 还是 post 变量 传入，都可以调用请求对象中与参数相关的方法来获取它们。

#### HttpServletRequest

##### 获取请求参数

`getParameterMap()`和`getParameterNames()`方法在遍历所有的请求参数时非常有用。★

在使用含有 post 变量的请求时，最好只使用参数方法，不要使用`getInputStream()`和`getReader()`方法。★

因为第一次调用请求对象的`getParameter()`、`getParameterMap()`、`getParameterNames()`或`getParameterValues()`方法时，Web 容器会判断该请求是否包含 post 变量，若包含，它将读取请求的 InputStream 并解析这些 post 变量（使用 InputStream 来读取参数），请求的 InputStream 只能被读取一次（InputStream 对象在使用后会关闭）。如果在调用了一个含有 post 变量的请求的`getInputStream()`或`getReader()`之后，再尝试获取请求的参数时，会触发 IllegalStateException（此时 InputStream 资源已经关闭）；同理，获取了一个含有 post 变量的请求的参数之后，再次调用 `getInputStream()`或`getReader()`时，也会触发此异常。

##### 确定与请求内容相关的信息

帮助决定 HTTP请求内容的 类型、长度 和 编码 的一些方法：

`getContentType()`

`getContentLength()`和`getContentLengthLong()`（Servlet 3.1 之前的版本：`getHeader("Content-Length")`，并将返回类型转换为 long）：以字节为单位，后一个用于内容长度超过 2GB 的请求（不常见，但不代表不可能）。

尽管很多情况下它们非常方便看，但如果需要使用参数方法从请求正文中获得 post 变量，就不需要使用它们。★

##### 读取请求的内容

`getInputStream()`：二进制格式

`getReader()`：基于字符编码格式

永远不要在同一个请求上同时使用这两个方法，调用一个后，再调用另一个会触发 IllegalStateException 。★

记住之前的警告，不要在含有 post 变量的请求上使用它们。★

#### HttpServletResponse

##### 编写响应正文

如果计划在`getWriter()`时调用`setContentType()`和`setCharacterEncoding()`，必须在`getWriter()`之前调用它们。★

还可以使用`setContentLength()`与`setContentLengthLong()`（Servlet 3.1 之前：

`SetHeader("Content-Length", Long.toString(length))`)，但大多时候都不需要使用它们，因为 Web 容器在响应完成后，会设置 Content-Length 头，由它完成更安全。★

##### 设置头和其他响应属性

可以使用`addHeader()`、`addIntHeader()`或`addDateHeader()`来避免同名的头的覆盖。★

### 使用初始化参数配置应用程序

上下文初始化参数（ServletContext）和 Servlet 初始化参数（ServletConfig）。

用途：有很多，如：定义关系型数据库的连接信息、提供发送订单警告的邮件地址等。

它们在应用程序启动时定义，只有在重启应用程序时才可以被修改。★

##### 上下文初始化参数

虽然在 Servlet 3.0 中添加了注解，但有些配置必须通过部署描述符才能完成。★

上下文初始化参数就是之一。

定义 ( web.xml 中) ：

```xml
<context-param>
    <param-name>settingOne</param-name>
    <param-value>foo</param-value>
</context-param>
<context-param>
    <param-name>settingTwo</param-name>
    <param-value>bar</param-value>
</context-param>
```

获取 ( Servlet 中) ：

```java
ServletContext servletContext = this.getServletContext();
servletContext.getInitParameter("settingOne");
servletContext.getInitParameter("settingTwo");
```

除了在 web.xml 中定义，还可以调用 ServletContext 的`setInitParameter()`，不过，它只能在 javax.servlet.ServletContextListener 的`contextInitialized()`或 javax.servlet.ServletContainerInitializer 的`onStartup()`中调用。

改变初始化参数的值也要求 重新编译 程序，所以 XML 通常是定义上下文初始化参数的最好方式。★

##### Servlet 初始化参数

定义 ( web.xml 中) ：

```xml
<!-- 在 servlet 标签中 -->
<init-param>
    <param-name>database</param-name>
    <param-value>CustomerSupport</param-value>
</init-param>
<init-param>
    <param-name>server</param-name>
    <param-value>10.0.12.5</param-value>
</init-param>
```

获取 ( Servlet 中) ：

```java
ServletConfig servletConfig = this.getServletConfig();
servletConfig.getInitParameter("database");
servletConfig.getInitParameter("server");
```

在这里使用部署描述符的优点：服务器管理员只需改变数行 XML 代码并重启应用即可使新的配置生效。★

---

等价于使用注解：（若使用注释，需要删掉 web.xml 中除`<display-name>`以外的内容 ★）

```java
@WebServlet(
    name = "servletParameterServlet",
    urlPatterns = {"/servletParameters"},
    initParams = {
        @WebInitParam(name = "databaser", value = "CustomerSupport"),
        @WebInitParam(name = "server", value = "10.0.12.5")
    }
)
```

在这里使用注解的缺点：修改了 Servlet 初始化参数之后必须重新编译应用程序。★

---

Web 应用程序中注解的 优势：简洁。

缺点：

1. 在创建单个 Servlet 的多个实例时，注解无法完成，只能通过 配置 XML 或 编程式 Java 配置完成。
2. 过滤器需要按特定的顺序执行，可以通过 配置 XML 或 编程式 Java 配置实现，而使用 @WebFilter 则不可能实现。除非应用程序只有一个过滤器，否则 @WebFilter 实际上时无用的。★
3. 还有许多小功能需要使用 XML 配置，如：定义错误处理页面、配置 JPS 设置 和 提供欢迎页面列表。

幸亏，我们可以混合使用三种配置，选择合适的即可。★

### 通过表单上传

将文件上传到 Servlet 比较复杂，Appache Commons 还单独为它创建了一个项目 —— Commons FileUpload 。

Servlet 3.0 为 Servlet 添加了 multipart 配置选项，并为 HttpServletRequest 添加了`getPath()`和`getParts()`，来改变现状。

##### 配置 Servlet 支持文件上传

POJO —— 普通 Java 对象。

通过 @MultipartConfig 实现。

---

重点属性：

location：告诉浏览器应该在哪里存储临时文件。（大多数情况都可以忽略，让应用服务器使用默认临时目录即可。）

fileSizeThreshold：告诉 Web 容器文件必须要达到多大才能写到临时目录中（请求完成后容器自动从磁盘中将其删除）。（小于这个大小的文件直接保存在内存中，直到请求完成，然后由垃圾回收器回收。）

其他属性：

maxFileSize：上传文件的大小最大值。

maxRequestSize：最大请求大小。

---

注解中的配置参数修改之后仍需重新编译。

部署描述符配置：

`<multipart-config>`，其中可以使用的标签有：`<location>`、`<file-size-threshold>`、`<max-file-size>`

和`<max-request-size>` 。

```java
// 强制浏览器询问客户是保存还是下载文件，而不是在浏览器中在线打开该文件
response.setHeader("Context-Disposition", "attachment; filename=" + attachment.getName());
// 通用的、二进制内容类型，使容器不使用字符编码处理该数据（更正确的方式应该是使用附件真正的 MIME 内容类型，但改任务超出了本书的范围）。
response.setContentType("application/octet-stream");

// 如果希望实现大文件下载，则不应该将文件存在内存中，而应将数据从文件的 InputStream 复制到 ResponseOutputStream，并经常刷新 ResponseOutputStream，这样数据才能不断被发送到用户浏览器中，而不是全部存在内存中。
ServletOutputStream stream = response.getOutputStream();
stream.write(attachment.getContents());
```

##### 接受文件上传

Servlet 3.1 中增加`getSubmittedFileName()`，用于识别文件在上传之前的原始名称。

### 编写多线程安全的应用程序

Web 容器通常有某种类型的线程池。其中 Tomcat 定义了一个 acceptCount 来指定最大线程数。

操作多线程，始终考虑到最糟糕的一点，许多线程可能同时在同一实例上执行相同的方法。★

Servlet 3.0 添加了异步请求上下文，可以使用 ServletRequest 的`startAsync()`方法，从 AsyncContext 中获取响应对象。通常长轮询 (long polling) 会使用这种方式。

##### 保护共享资源

volatile （可变的，不稳定的，易挥发的）关键字：保证其他线程始终能读到变量修改后的最终值。★

---

在写 Servlet 时，永远不要在 静态 或 实例变量 中存储请求或响应对象，这一定会引起问题。任何属于请求的对象和资源都只应该被用作本地变量和方法参数。★

## 第四章：JSP

