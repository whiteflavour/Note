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

根据选择的服务器和需求来确定是使用 双亲委托优先模式 还是 子女委托优先模式 。

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



