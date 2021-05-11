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

### JSP: 

JSP 实际上是一个精心设计的 Servlet，是语法糖。

JSP 编译后的类最终取决于它在其中运行的 Web 容器。

JSP 默认内容类型：text/html；字符编码：ISO-8859-1 。

Scriplet (`<%%>`) 的缩进形式可能会影响 IDE （IDEA）对其语法的判断：★

```jsp
<%
	... 
%> ... <%
...
%>
```

### Directive: 

属性：

有很多属性，可以通过禁用 session 和 buffer 来提高性能，其中 buffer 有些缺点。

永远不要修改 isThreadSafe 属性：如果你的 JSP 不是线程安全的，它就是错误的。★

### Web App 的根目录：

Web 。★

相对路径：从该 JSP 或者 Servlet 存在的路径开始。★

### `<jsp>`标签

`<jsp:forward page="">`：不是重定向，此标签之后的代码将被忽略。（重定向不会）★

`<jsp:useBean>`：在页面中声明一个 JavaBean。

`<jsp:getProperty>`：从上述标签中声明的 bean 中获取属性值（通过 getter 方法）。

`<jsp:setProperty>`：设置属性（通过 setter 方法）。

### JSP  response 对象的限制

JSP 中有许多隐式对象。

不应该调用 getWriter 和 getOutputStream 方法，不应该设置内容类型或字符编码、刷新或重置缓存或者修改缓存大小。这些工作 JSP 已经完成了，重复执行它们会引起问题。★

更多信息，阅读 JavaServer Pages 2.3 规范文档：http://download.oracle.com/otndocs/jcp/jsp-2_3-mrel2-spec/ 。

### WEB-INF 目录：

该目录中的文件禁止通过 Web 访问（URL）。

### 常见模式：

有 Servlet 接受请求，实现业务逻辑及必须的数据存储或读取，创建可由 JSP 轻松处理的数据模型，最终将请求转发给 JSP。★

## 第五章、会话

可以使用网络嗅探工具追踪（如：Fiddler 或 Wireshark） HTTP 请求和响应的信息。

HttpServletResponse 中两个重写 URL 的方法：encodeURL 、encodeRedirectURL 。

### 会话的漏洞：

开发者应该一直保持对安全事件的关注。★

在执行重要任务、含有敏感数据的应用程序中，使用某些商业扫描器检测应用丑程序中的漏洞是明智的选择。

关于 Web app 和会话的更多信息，以及如何检测和解决它们，访问 OWASP 网站：https://www.owasp.org 。

---

不要与不信任的应用程序共享域名。★

会话 ID cookie 中总是应该包含 HttpOnly 特性。★

---

关于 SSL 会话 ID 工作方式的更多信息，查看： RFC 2246 "The TLS Protocol" 。

SSL 配置的更多细节，查看 Tomcat 文档。★

### 测试会话是否创建：

getSession() 实际调用的是 getSession(true)，可以调用 getSession(false) 来测试是否已经创建会话。

---

在浏览器中很难找回之前的会话。★

### HttpSession 的方法：

有许多方法，最重要的之一：invalidate()：销毁会话并解除所有绑定到会话的数据。即使客户浏览器使用相同的会话 ID 发起了另一个请求，已经无效的会话也不能再使用。新的会话将被创建，并响应中将包含新的会话 ID 。★

---

必须考虑存储数据的大小。

Vector 对于 ArrayList 是线程安全的。

在 urlPatterns 中使用通配符：/do/* ：任何 /do/... 都能访问。★

### 迁移会话应付会话攻击（修改会话 ID）：

changeSessionId() 。

### 会话最有用的特性之一 —— 会话事件：

用于检测会话发生变化的工具——监听器。

**几种监听器**：

javax.servlet.annotation.WebListener 。

javax.servlet.annotation.BindingListener ：特别有趣，不需要添加注解或部署描述符配置。若某类实现该接口，它将把自己的状态当作会话特性。

记录会话创建和销毁的信息，是监听器的常用方式，管理员可能会保存这些信息。★

---

Tomcat 关闭时，它将把会话持久到文件系统中，大多数情况可以禁止该行为，具体参考容器官方文档。

### 将使用会话的应用程序群集化：

各个容器的配置不同，具体参考容器官方文档。

## 第六章、EL

> 不鼓励使用声明、脚本和表达式。★

分为立即执行和延迟执行两种：

1. 立即执行：`${}`
2. 延迟执行：`#{}`，很少使用，通常不会出现在 JSP 中。★

### 禁止将 #{} 当作延迟执行表达式执行：

web.xml:

```xml
<jsp-config>
	<jsp-property-group>
    	<deferred-syntax-allowed-as-literal>true</deferred-syntax-allowed-as-literal>
    </jsp-property-group>
</jsp-config>
```

或

xxx.jsp:

```jsp
<%@ page ... deferredSyntaxAllowedAsLiteral="true" %>
```

### EL 的位置：

不能在 Directive, Decleration, Scriptlet and Expression 中使用。

**原因：**

Directive 等在编译时执行，而 EL 在渲染 JSP 时执行。

**结果：**

EL 被忽略，甚至导致语法错误。★

### EL 语法：

弱类型，不能在 EL 中声明变量、执行赋值语句或者不产生结果的操作。

### EL 的作用：

提供一种创建 JSP 的工具，从而避免在 JSP 中使用 Java 。

### 在 EL 中使用多个表达式：

只有最后一个表达式的值被保留下来。★

### 字面量：

使用单引号和双引号都可以。

### EL 默认数据类型：

与 Java 的不同点：

|                                      |     Java     |  EL   |
| :----------------------------------- | :----------: | :---: |
| **默认小数数据类型**                 |    double    | float |
| **数字进制**                         | 2, 8, 10, 16 |  10   |
| **是否允许数字中插入下划线进行连接** |      是      |  否   |

### EL 函数：

`${fn:escapeXml(String)}`：在防止跨站脚本 (XSS) 攻击时起重要作用。★

更多函数：http://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/fn/tld-summary.html ，这是 Java EE5 JSTL 1.1 的文档，6 和 7 中没有为 JSTL 1.2 准备轻松可用的 HTML 文档。★

### 字段访问：

#### 访问类成员变量：

1. `${shirt.size}`：需要 Getter and Setter 。
2. `${shirt["size"]}`：需要 Getter and Setter 。
3. `${shirt.getSize()}`：不需要 Getter and Setter 。EL 2.1 添加。

#### 访问 Map ：

1. 键：`${map["username"]}`，值：`${map["userId"]}`。
2. 键：`${map.username}`，值：`${map.userId}`。限制：键名必须是 Java 标识符。

> 谨慎起见，推荐使用第一种。★

#### 访问 List ：

1. `${list[0]}`, `${list[1]}`, `${list[2]}`
2. `${list["0"]}`, `${list['1']}`, `${list[2]}`

> 推荐使用第一种，第二种可能被误认为 Map 。★