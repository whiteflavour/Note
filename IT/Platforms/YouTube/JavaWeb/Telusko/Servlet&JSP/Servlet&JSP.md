# Servlet&JSP (From [Telusko](https://www.youtube.com/channel/UC59K-uG2A5ogwIrHw4bmlEg)) —— 完成时间：2021.2

## How Servlet works with Tomcat

### 动态网页：

动态网页是可以随时间变化的。客户端向服务器请求访问一个网页，但这个网页还没有加工出来，此时需要一个 Web 容器（如，Tomcat）来即时对请求访问的页面加工，然后在发送到客户端。此时需要用 Java 来写一个网页，故需要创建一个类，这就是你的 Servlet 。在 Web Container 中还有一个部署描述器（Deployment Descriptor），文件名为`web.xml`，每一块`<servlet></servlet>`标签映射一个 Servlet 。

我们是做 Java 的，所以为了避免使用 xml 文件，可以在 Servlet 上添加注解来代替。

![How Servlet works with Tomcat](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\How Servlet works with Tomcat.png)

## IDEs to Build JavaEE

最好的 IDE 是 IDEA，但是因为收费，所以在大学可能是用的 NetBeans，而公司中用来练习的 IDE 大多数人都是用的 Eclipse 。(  In India ? )

JavaEE 的项目要跑起来，需要 Tomcat Server 。★

## Download Tomcat

搜索 Tomcat，进入官网，下载 Tomcat 8 core 和 Source Code Distributions（documention）：

![Tomcat Download](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Tomcat Download.png)

## 在 Eclipse 中配置 Tomcat：

1. 弄出 Eclipse 底部的 Servers 窗口：

![Config Tomcat in Eclipse](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Config Tomcat in Eclipse.png)

2. 点击 Servers 窗口中的蓝字，连接 Tomcat Server：

![Connect to the Tomcat Server](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Connect to the Tomcat Server.png)

3. 选择 Tomcat 8 ：

![Select a Tomcat Server](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Select a Tomcat Server.png)

4. 选择你刚刚压缩包的路径（Tomcat Core，不用管那个 Tomcat Source）：

![Select the Location of Your Tomcat](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Select the Location of Your Tomcat.png)

5. 右击 Server 窗口中的 Server，点击 Start：

![Start Tomcat Server](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Start Tomcat Server.png)

6. 如果运行成功，则变为 Started ；如果运行失败，可能是端口被占用。单击这句话，可以查看 Tomcat 的端口（端口名为HTTP/1.1 的那个，双击端口号可以将其改为其他的，这里加 1（如果端口被占用的话） ）：

![Tomcat's port](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Tomcat's port.png)

7. 浏览器搜索框输入`localhost:8080`即可访问。（`localhost:port`）
8. 出现 Tomcat 相关的一些文字，即访问成功：

![Tomcat Web Page](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Tomcat Web Page.png)

9. 修改 Home Page of Tomcat Web Page：在 Overview 界面的 Server Locations 中，选择 Tomcat Installation 选项（可以用那个页面来部署 Server，但我们一般都用 Eclipse 来部署。）：

![Change the Home Page of Tomcat Web Page](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Change the Home Page of Tomcat Web Page.png)

## Eclipse 中创建项目并输出 Hello World：

在 WebContent 目录中创建 Index.html 文件：

![创建 Index.html 文件输出 Hello World](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\创建 Index.html 文件输出 Hello World.png)

将显示的浏览器从内置浏览器改为其他浏览器：

![自定义输出浏览器](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\自定义输出浏览器.png)

## 什么是 Servlet ？

我们写一段代码来解释：

```html
<html>
  <head>
    <title>草</title>
  </head>
  <body>
  	
  	<!-- 此时点击 submit 按钮没有反应，因为 action 那里什么都没有写 -->
  	<!-- 我们在 action 处加上 add，此时点击 submit 按钮会跳转到 add 页面，此时是 Tomcat Server 的默认界面，因为我们还没有编写它。而这个 add 页面，就是 Servlet -->
  	
  	<form action="add">
  		Enter 1st number: <input type="text" name="num1"><br>
  		Enter 2nd number: <input type="text" name="num2"><br>
  		<input type="submit">
  	</form>
  
  </body>
</html>
```

## Create Servlet and web.xml Config

那个 add 页面，可以用 JS 编写，但是我们想用 Java，想用 Servlet，于是我们创建一个 Servlet：

只需要创建一个 Java 类，然后使它继承`HttpServlet`，这个类就变成了 Servlet 。★

我们需要使用 service() 方法，来使该类接收请求，并处理请求：

```java
public class AddServlet extends HttpServlet {
	public void service(HttpServletRequest req, HttpServletResponse res) {
		int i = Integer.parseInt(req.getParameter("num1"));
		int j = Integer.parseInt(req.getParameter("num2"));
		
		int k = i + j;
        
        // 在控制台输出的语句。
		// System.out.println("The result is " + k);
        
        // 我们需要使它在页面上输出，所以需要使用下面的语句。
        PrintWriter out = res.getWriter();
        out.println("The result is " + k);
	}
}
```

地址栏上的末尾那一串叫做 Query String，它是一个可以使你的数据从*客户端*发送到*服务器*的部分。

web.xml 又叫做 Deployment Descriptor，该文件中有所有的告诉 Tomcat 哪个动作该使用哪个 Servlet 来响应客户端的配置。★

web.xml 文件中 Tomcat 自动生成的那些配置可以删去了（welcome page），那些是 Tomcat 的默认页面：

![Delete Welcom Page Config From web.xml](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\Delete Welcom Page Config From web.xml.png)

---

### 配置自己的 Servlet

每个 Servlet 需要在 web.xml 文件中使用两个标签来配置（`<servlet></servlet>`和`<servlet-mapping></servlet-mapping>`，其中每个含有两个子标签）：

```xml
<!-- 两个标签中的 servlet-name 要相同，servlet-name 相当于一个标志，一个代号，一个告诉 Tomcat 的编号，必须唯一。可以随意取。 -->
<!-- class-name 需要使用全名，即包括包名。 -->

<servlet>
	<servlet-name>abc</servlet-name>
	<servlet-class>com.google.AddServlet</servlet-class>
</servlet>

<servlet-mapping>
	<servlet-name>abc</servlet-name>
    
    <!-- 记住有个 slash，即 / -->
	<url-pattern>/add</url-pattern>
</servlet-mapping>
```

配置完成后需要重启 Tomcat Server 。

此时点击 Submit 按钮后，加载出的新页面不会报错了，但是不显示结果，而结果显示在控制台，这是因为`System.out.println`语句。★

我们使用下面的语句来使其打印在浏览器页面上：★

```java
PrintWriter out = res.getWriter();
out.println("The result is " + k);
```

## Get and Post

我们使用的是 HTTP 协议，它有 7 个方法，其中有 5 个是常用的：

1. Get
2. Post
3. Put
4. Delete
5. Options

在网页中我们不会用到全部。向服务器发送数据使用 Post request；从服务器获得数据使用 Get request 。

这里默认是使用的 Get request 。使用 Get 数据的值会显示在地址栏上。

可以使其默认使用 Post，这样地址栏上就不会显示数据的值了：★

```jsp
<!-- 使用 post 方法，默认使用 get -->
<form action="add" method="post">
      Enter a number: <input type="text" name="num1"><br>
      Enter another number: <input type="text" name="num2"><br>
      <input type="submit">
</form>
```

可以使用与 Post 对应的 Servlet 中的 doPost() 方法，但 doPost() 只对应使用 post，而不能使用 get：★

```java
public class AddServlet extends HttpServlet {
	// 使用 doPost() 方法来限定，使其只能使用 post request
    public void doPost(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int numberA = Integer.parseInt(req.getParameter("num1"));
        int numberB = Integer.parseInt(req.getParameter("num2"));
        int sum = numberA + numberB;

        PrintWriter out = res.getWriter();
        out.println("The result is " + sum);
    }
}
```

使用 doPost() 或者 doGet() 相当于也是使用了 service() 方法，因为 HttpServlet 父类中本来就有 service() 方法，而它会选择调用 doPost() 还是 doGet()，或者是其他的 HTTP 方法。

## 如何通过 Servlet 调用 Servlet：

使用 Request Dispatcher 或者 Redirect 。

### 使用 Request Dispatcher：

```java
/**
 *  第一个 Servlet 
 */
public class AddServlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException, ServletException {
		int i = Integer.parseInt(req.getParameter("num1"));
		int j = Integer.parseInt(req.getParameter("num2"));
		
		int k = i + j;
        
		RequestDispatcher rd = req.getRequestDispatcher("sq");
         rd.forward(req, res);
	}
}

/**
 *  第二个 Servlet 
 */
public class SqServlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
		PrintWriter out = res.getWriter();
         out.println("Hello to Sq");
	}
}
```

还需要配置 web.xml 文件：

```xml
<!-- 第一个 Servlet 的配置 -->
<servlet>
	<servlet-name>abc</servlet-name>
	<servlet-class>com.google.AddServlet</servlet-class>
</servlet>

<servlet-mapping>
	<servlet-name>abc</servlet-name>
    
    <!-- 记住有个 slash，即 / -->
	<url-pattern>/add</url-pattern>
</servlet-mapping>

<!-- 第二个 Servlet 的配置 -->
<servlet>
	<servlet-name>pqr</servlet-name>
	<servlet-class>com.google.SqServlet</servlet-class>
</servlet>

<servlet-mapping>
	<servlet-name>pqr</servlet-name>
    
    <!-- 记住有个 slash，即 / -->
	<url-pattern>/sq</url-pattern>
</servlet-mapping>
```

### 从一个 Servlet 向另一个 Servlet 发送或分享数据：

使用 Session Management 。

这里我们使用`setAttribute()`和`getAttribute()`方法：

```java
/* 
   在上述第一个 Servlet 中添加：
       req.setAttribute("k", k);
*/
public class AddServlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException, ServletException {
		int i = Integer.parseInt(req.getParameter("num1"));
		int j = Integer.parseInt(req.getParameter("num2"));
		
		int k = i + j;
        
         req.setAttribute("k", k);
         
		RequestDispatcher rd = req.getRequestDispatcher("sq");
         rd.forward(req, res);
	}
}

/* 
   在上述第二个 Servlet 中添加：
       int k = (int) req.getAttribute("k");
       k = k * k;
*/
/* 
   将输出改为：
       out.println("Result is " + k);
*/
public class SqServlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int k = (int) req.getAttribute("k");
        k = k * k;
        
        PrintWriter out = res.getWriter();
        out.println("Result is " + k);
	}
}
```

## HttpServletRequest and HttpServletResponse Theory

客户端向服务器（Servlet），必须要发送数据和信息（比如：传送的值是什么，用的什么浏览器，及 ip 地址等等），要传送这些信息，就需要一定的格式（`.txt .md .html`等等）。而我们使用 Java，我们就可以使用一个对象来传送它们，即将它们封装入对象中。

### Request

我们将客户端发送的数据封装入一个对象中，这就叫做你的 Request Object，它封装了这些数据。

### Response

服务器收到一个请求之后就需要相应的响应。服务器可以发送许多信息，如：一张图片、一个视频、数据、HTML 标签等。这些发送的信息可以封装入一个对象中，这个对象就是你的 Response Object 。

在 Response Object 的帮助下，我们可以指定一个发送的格式。一般在 Web 服务中我们不会返回一个页面或是文本，而是返回一个 JSON 值，于是我们可以指定其格式为 JSON。★

---

### HttpServletRequest and HttpServletResponse

这两个对象不需要自己创建，我们只需要引用它们就行了，Tomcat 已经帮我们创建好了。

这两个都是接口，然后 Tomcat 会帮你创建它们的实现类并给你其实现类的对象。这就是为什么 Run Web Application 时我们需要 Tomcat Server 。

## RequestDispatcher and sendRedirect Theory

### RequestDispatcher

使用这个类时，从 Servlet1 调用 Servlet2，然后 Servlet2 返回给客户端响应，与客户端给Servlet1发送请求和Servlet1给客户端响应使用的 request 和 response 是相同的对象。★

![RequestDispatcher](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\RequestDispatcher.png)

使用 RequestDispatcher 时，客户端不知道响应是从 S1 还是 S2 发送过来的，因为 URL 指向的是 S1 。

### sendRedirect

RequestDispatcher 只在这两个 Servlet 在同一网站上才有用。★

如果这两个 Servlet 不在同一个网站，则客户端需要知道当 S1 调用 S2 时，进行了重定向。想象一下你在亚马逊下单的时候，跳转到支付页面，你是知道的。

这时 S1 就要使用`sendRedirect()`方法，来使客户端知道进行了重定向。★

![sendRedirect()](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\sendRedirect() Different Website.png)

---

使用重定向是 S1 告诉客户端你要去对 S2 发送请求，然后 S2 又对客户端响应，这与客户端和 S1 之间的通信使用的 Request 和 Response 的对象不同：★

![sendRedirect](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\sendRedirect.png)

---

使用重定向时如果要传送同一个数据（对象），则需要使用 sessionManagement 。★

## sendRedirect

`sendRedirect()`是使用 response 对象调用的，因为是 Servlet 告诉客户端，你要去找另一个 Servlet 。★

```java
// 
public class AddServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int numberA = Integer.parseInt(req.getParameter("num1"));
        int numberB = Integer.parseInt(req.getParameter("num2"));
        int k = numberA + numberB;

        // sendRedirect
        res.sendRedirect("sq");
        // 赋值版，不用在浏览器的地址栏给 k 赋值。
        // 这个技术是 Session Management 下的一种，叫做：URL Rewriting 。★
        res.sendRedirect("sq?k=" + k);
    }
}

//
public class SqServlet extends HttpServlet {
    public void service(HttpServletRequest req, HttpServletResponse res) throws IOException {
        /* 
        获取参数，因为是 doGet，所以可以直接在地址栏后面（http://localhost:8080/xxx/sq）添加参数：?k=12，给 k 赋值。doGet 方法是在 URL 中获取参数的值的。★
        即完整的 URL 为：http://localhost:8080/xxx/sq?k=12 
        若有两个参数，地址栏的最后为：/sq?a=1&b=2 ★
         */
        
        /*
        也可以不在地址栏后面添加参数，直接在 sendRedirect() 方法中传递参数的值，即将上方那个 Servlet 的 
        res.sendRedirect("sq") 改为 res.sendRedirect("sq?k=" + k) ★
        */
        int k = Integer.parseInt(req.getParameter("k"));
        
        PrintWriter out = res.getWriter();
        out.println("The Result is " + (k * k));
    }
}
```

### URL Rewriting, One of the Three Concepts under Session Management

上面第一个 Servlet 中的 `res.sendRedirect("sq?k=" + k)`语句，即为 URL Rewriting 。★

另外两个技术是 Session 和 Cookie 。

### HttpSession

每次浏览一个 Web Application 时 Tomcat 都会创造出一个 Session，如果我们把数据放入这个 Session，另一个 Servlet 也可以使用它：使用 HttpSession 类，它是一个接口：

```java
/*
在 AddServlet 中添加：
	HttpSession session = req.getSession();
	int k = session.setAttribute("k", k);
*/
public class AddServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int numberA = Integer.parseInt(req.getParameter("num1"));
        int numberB = Integer.parseInt(req.getParameter("num2"));
        int k = numberA + numberB;
		
        // 使用 Session
	    HttpSession session = req.getSession();
	    session.setAttribute("k", k);
	    
        res.sendRedirect("sq");
    }
}

/*
在 SqServlet 中添加：
	HttpSession session = req.getSession();
	int k = (int) session.getAttribute("k", k);
*/
public class SqServlet extends HttpServlet {    
    public void service(HttpServletRequest req, HttpServletResponse res) throws IOException {   
         // 使用 Session
		HttpSession session = req.getSession();        
		int k = (int) session.getAttribute("k");
         
		k = k * k;
        
		PrintWriter out = res.getWriter();
		out.println("The Result is " + k);
        
         System.out.println("sq called");
    }    
}

// 删除属性
public class SqServlet extends HttpServlet {    
    public void service(HttpServletRequest req, HttpServletResponse res) throws IOException {   
         // 使用 Session
		HttpSession session = req.getSession();
        
         // 从 Session 中删除属性，这样就后面的 getAtrribute() 就不能获取属性了。
         // 只有当属性在 Session 中时，才能获取该属性。★
         session.removeAttribute("k"); 
        
         // 此时这条语句无法获取 k 这个属性。
		int k = (int) session.getAttribute("k");
         
		k = k * k;
        
		PrintWriter out = res.getWriter();
		out.println("The Result is " + k);
        
         System.out.println("sq called");
    }    
}
```

只要你不关闭这个 Web Application，Session 就是有效的。

### Cookie

每次客户端向服务器发送一个请求，服务器都会给你一个响应，而那个 Response Object 中就有 Cookie 。重定向之后，你可以再次发送这个 Cookie ，将它放在你的 Request Object 中，向另一个 Servlet 发送请求。

就像你去超市买东西时，你买了 50 元的东西，但付了 100 元，超市无法找零了，他们让你等半小时再过来，然后就需要给你一个 Token；如果不给 Token，半小时后鬼知道你是谁，凭什么要找你 50 元。

这个 Token 就相当于我们的 Cookie 。

```java
/*
在 AddServlet 中添加：
	Cookie cookie = new Cookie("k", k + "");
	req.addCookie(cookie);
*/
public class AddServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int numberA = Integer.parseInt(req.getParameter("num1"));
        int numberB = Integer.parseInt(req.getParameter("num2"));
        int k = numberA + numberB;
		
	    // 使用 Cookie
        // 这里使用 k + "" 将整型的 k 转换为 String ★
	    Cookie cookie = new Cookie("k", k + "");
        // 将 cookie 添加进 Server 的 Response Object，当 Response Object 发送到客户端之后，客户端又能将同样的 Cookie 放入它的 Request Object 发送给另一个 Servlet 。
	    res.addCookie(cookie);
	    
        res.sendRedirect("sq");
    }
}

/*
在 SqServlet 中添加：
	int k = 0;
	Cookie cookies[] = req.getCookies(); 
	
	for (Cookie c : cookies) {
		if (c.getName().equals("k")) {
			k = Integer.parseInt(c.getValue());
		}
	}
*/
public class SqServlet extends HttpServlet {    
    public void service(HttpServletRequest req, HttpServletResponse res) throws IOException {   
         int k = 0;
         // 客户端不知道你需要的是哪个 Cookie ，所以它会发送所有的 Cookie ，于是我们需要一个数组来接受这些 Cookie
         Cookie cookies[] = req.getCookies(); 

         // 查找我们需要的 Cookie 的值
         for (Cookie c : cookies) {
             if (c.getName().equals("k")) {
                 k = Integer.parseInt(c.getValue());
             }
         }
         
		k = k * k;
        
		PrintWriter out = res.getWriter();
		out.println("The Result is " + k);
        
         System.out.println("sq called");
    }    
}
```

建议多练习，把几个方式都练习一下，不止是两个数相加，还可以试试其他的操作，如：登录等等。

## ServletConfig and ServletContext

我们使用它们来给 Servlet 或者 应用 赋初值。你可以指定一些东西，如：该文件的路径。我们在可以在 web.xml 文件中配置，然后在 Java 源文件中使用它们。

ServletConfig 的优先级比 ServletContext 高。★

`ServletCOntext context = getServletContext();`语句中的`getServletContext()`方法调用父类 HttpServlet 的这个方法，因为 HttpServlet 继承 GenericServlet 。最终我们会获得 ServletContext 的对象，这是一个抽象类，Tomcat 会帮我们构造它的对象。相当于调用`super.getServletContext()`。★

### ServletContext

在 web.xml 文件中配置：

```xml
<!-- 直接为 web-app 标签的子标签 -->
<context-param>
	<param-name>name</param-name>
	<param-value>Liao</param-value>
</context-param>

<context-param>
	<param-name>Phone</param-name>
	<param-value>Samsung</param-value>
</context-param>
```

在 Java 文件中使用：

```java
public class MyServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        
        // 使 <br> 在浏览器中显示 HTML 中的换行
        res.setContentType("text/html");
        
        PrintWriter out = res.getWriter();
        out.print("Hi<br>");
        
        // 从 web.xml 中获取 Servlet Context
        ServletContext context = getServletContext();
        // 或者
        ServletContext context = req.getServletContext();
        
        // 从 web.xml 中获取的 Servlet Context 中获取 参数名 为 name 的 参数值 。
        String str = context.getInitParameter("name");
        
        out.println(str);
    }
}
```

最常用的是使用它们来给出默认的文件路径、数据库位置、或者数据库中用户名和密码的位置等。★

### ServletConfig

它和 ServletContext 一样，也是用来给一些参数赋初始值的。

但它们有一些 **不同点** ：

ServletContext 会使你的所有的 Servlet 都共用这些参数的名字及其对应的值；而 ServletConfig 则能够指定哪一个 Servlet 使用不同的值。★

---

在 web.xml 中的 Servlet 标签中使用 ServletConfig ：

```xml
<servlet>
	<servlet-name>abc</servlet-name>
	<servlet-class>com.google.AddServlet</servlet-class>
	
	<!-- 使用 ServletConfig 初始化参数 -->
	<init-param>
		<param-name>name</param-name>
		<param-value>Jack</param-value>
	</init-param>
</servlet>

<servlet-mapping>
	<servlet-name>abc</servlet-name>
    
    <!-- 记住有个 slash，即 / -->
	<url-pattern>/add</url-pattern>
</servlet-mapping>
```

在 Java 文件中获取 ServletConfig ：

```java
public class MyServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        PrintWriter out = res.getWriter();
        out.print("Hi<br>");
        
        // 从 web.xml 中获取 Servlet Config
        ServletConfig config = getServletConfig();
        // 此时就不能使用下面这句话了。★
        ServletConfig config = req.getServletConfig();
        
        // 从 web.xml 中获取的 Servlet Context 中获取 参数名 为 name 的 参数值 。
        String str = config.getInitParameter("name");
        
        out.println(str);
    }
}
```

## Servlet Annotation Configuration

不是所有的人都喜欢用 web.xml 来配置，因为注释简单多了。

```java
// 先将 web.xml 中的配置注释掉
// 然后在 Java 代码中使用注解

// 注解，等价于 web.xml 中对应的那段配置
// 再次提醒，别忘了 slash （/），否则 Tomcat Server 启动错误。★
@WebServlet("/add")
public class AddServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int numberA = Integer.parseInt(req.getParameter("num1"));
        int numberB = Integer.parseInt(req.getParameter("num2"));
        int k = numberA + numberB;
		
        // 使用 Session
	    HttpSession session = req.getSession();
	    session.setAttribute("k", k);
	    
        res.sendRedirect("sq");
    }
}

@WebServlet("/sq")
public class SqServlet extends HttpServlet {    
    public void service(HttpServletRequest req, HttpServletResponse res) throws IOException {   
         // 使用 Session
		HttpSession session = req.getSession();        
		int k = (int) session.getAttribute("k");
         
		k = k * k;
        
		PrintWriter out = res.getWriter();
		out.println("The Result is " + k);
        
         System.out.println("sq called");
    }    
}
```

以后我们在使用 Hibernate 或者是 Spring Framework 的时候，都是使用注解来配置的。★

## Why JSP?

如果你想制作一个网页，只需将 Response 的类型指定为 HTML ，而不需要写任何 HTML 标签。★

使用 Servlet 来写 HTML 标签：( AddServlet )

```java
@WebServlet("/add")
public class AddServlet extends HttpServlet {
    public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
        int numberA = Integer.parseInt(req.getParameter("num1"));
        int numberB = Integer.parseInt(req.getParameter("num2"));
        
        int k = numberA + numberB;
		
        PrintWriter out = res.getWriter();
        
        // 在 Servlet 中使用 HTML 标签来制作网页，这里使返回结果页面的颜色变为深蓝色。
        // 不推荐使用，因为一个好看的网页需要的标签太多，全在 out.print() 中写，不太靠谱。★
        out.println("<html><body bgcolor='cyan'>")
        out.println("Output: " + k);
        out.print("</body></html>");
    }
}
```

这样做是不妥的。设计是设计师来完成，后端是开发者来完成，而一般设计师不喜欢开发，开发者不喜欢设计。并且一个好的网页需要的标签太多，全在`out.print()`中来写不太靠谱，我们不应该在 Java 代码中来写 HTML 。★

此时就有了 JSP ，它是反过来的，它是在 HTML 中写 Java。 ★

JSP：( add.jsp )

```jsp
<body bgcolor='cyan'>
  // 分割符，在它们之间写 Java 代码。★
  <%
    // JSP 中默认提供 request 对象，这种默认提供的对象叫做 JSP 的隐式对象。★
    int numberA = Integer.parseInt(request.getParameter("num1"));
    int numberB = Integer.parseInt(request.getParameter("num2"));

    int k = numberA + numberB;

    // out 对象也是 JSP 默认提供的，我们不需要自己去创建。★
    out.println("Output: " + k);
  %>
</body>
```

JSP 会默认提供 request 、out 等对象，这种 JSP 默认提供的对象叫做隐式对象，我们不用自己去创建它们。★

index.jsp：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title></title>
  </head>
  <body>
  
  <!-- 此时将 action 属性的值改为 JSP 文件的名字，这里为 add.jsp -->
  <form action="add.jsp" method="get">
    Enter a number: <input type="text" name="num1"><br>
    Enter another number: <input type="text" name="num2"><br>
    <input type="submit">
  </form>

  </body>
</html>
```

此时打开页面，我们可以看到地址栏上最后端从`/add`变成了`/add.jsp`，这表明我们在调用 JSP 。★

我们都讨厌红色，因为它会对眼睛造成伤害；深蓝色就好多了。？？？？★

#### JSP 相对于 Servlet 的优势

Servlet 非常复杂，我们要在里面写很多东西才能做一件事情，什么创建对象啊、继承 HttpServlet 呀、创建一个有两个参数的方法啊 等等。重要的是，我们要写 HTML ，需要在`out.println()`中来写，非常蛋疼。

JSP 就简单多了，在 HTML 中写 Java，它们是分开的，开发者可以将精力集中在 Java 上。

## How JSP translated into Servlets?

JSP 是个很好的选择，但为什么我们还要学 Servlet 呢？它们能否一起工作？

Tomcat 叫做 Servlet Container ，所以通过 Tomcat 只能运行 Servlet ，不能运行 JSP，所以我们不能只学 JSP，还要学 Servlet 。运行JSP 时，它会转换成 Servlet 。★

JSP 唯一的优势就是它能使开发者更易开发。★

JSP 转换为 Servlet ，会转换成那部分框架代码，即无论使用 Servlet 做什么工作，都需要写的那部分代码：创建一个 Servlet 继承 HttpServlet 类，创建一个`service()`方法，里面有 request 、response 两个参数，创建一个 PrintWriter 类的 out 对象，用于在页面上显示一些内容。然后你在 JSP Scriptlet 中写的代码会被复制到 Servlet 中的 service 方法对应的部分中。

在 JSP 中所有这些可以在 Servlet 里面使用的 Tomcat 创建的对象都在 JSP 中自动创建了，这些叫做隐式对象。★

![JSP translate into Servlet](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\JSP translate into Servlet.png)

### Four types of tags in JSP：

#### Scriptlet：

JSP 中写 Java 代码之间的那两个符号叫做 scriptlet 。

```jsp
<!-- 其间的代码会被复制到 Servlet 中 service() 方法对应的部分中 -->
<%
	...
%>
```

#### Declaration：

如果希望在`service()`方法外部，Servlet 类中声明变量，可以将其写在`<%! %>`符号中，这个符号叫做 declaration ：★

```jsp
<%!
	int value = 1;
%>
```

#### Directive：

在 JSP 中导包：使用 directive

```jsp
<!-- 这个符号叫做 directive -->
<!-- 这个 import 是属性 -->
<%@ page import="java.util.Date" %>

<!-- 若要导很多包，只需使用逗号隔开 -->
<%@ page import="java.util.Set, java.util.HashSet" %>
```

#### Expression：

除了直接在 scriptlet 中写`out.print()`方法，也可以在 expression 中写，即`<%= %>`：

```jsp
<!-- 等价于在 Servlet 的 service 方法中写 out.print() -->
<!-- 这个符号叫做 expression -->
<%= k %>
```

### 使用哪个更好？

这看需求，如果你的目的是创建一个网页，在网页上显示一些数据，则使用 JSP；如果只是想加工（process），则使用 Servlet 。在下节课中我们详细来探讨。★

## JSP to Servlet Conversion

当你写一些逻辑的时候 (logic)，使用 Servlet 更加合适。

这节课使用 Netbeans 来讲，因为它有比 Eclipse 更好用的 JSP 项目构建工具。这里使用 Tomcat 或者 GlassFish 都是一样的。

在 Netbeans IDE 中，可以右击 JSP 文件，然后点击 view servlet ，即可查看对应的转换成的 Servlet ，并且可以在里面查看关于你的 JSP 文件转换为 Servlet 的一切信息。★

### IDEA 中 JSP 转换成的 Servlet 对应的文件路径：★

`C:\Users\Fuck\AppData\Local\JetBrains\IntelliJIdea2020.1\tomcat\Tomcat_8_5_61_FourTypesOfTags\work\Catalina\localhost\FourTypesOfTags_war_exploded\org\apache\jsp` 。

注意观察控制台 server 部分的日志信息：★

![JSP 转换成的 Servlet 的文件路径](F:\Note\YouTube\Javaweb\Telusko\Servlet&JSP\JSP 转换成的 Servlet 的文件路径.png)

---

## The Four JSP Tags: 

一种标签不一定只写一次，可以在不同的地方写多次同一种标签。★

`import`在 Directive 中变成了属性，所以需要用 = 号。

在输出一个变量时，只需在 Expression 中捕获它即可，不需要再在 Scriptlet 中使用`out.println()`方法来输出：

```jsp
The output is : <%= k%>
<%--等价于--%>
The output is : <% out.println(k); %>
```

## JSP Directive

Directive tag has 3 types：

1. page：对于本页面要做的事情，可用于 导包、规定使用的语言及异常处理等等。有一些常用的属性：

    ```jsp
    <%--语法--%>
    <%@ page attribute="value" attribute="value" ... %>
    
    <%--常用属性--%>
    language="scripting language"
    extends="classname"				因为 JSP 会转换成 Servlet，所以这里是 Servlet 中要继承的类，可以继承自己的其他 									   Servlet。
    import="importList"
    session="true|false"
    autoFlush="true|false"			如果有缓冲，且如果关闭，则只会在缓冲区满时才发送数据。
    contentType="ctinfo"
    errorPage="error_url"
    isErrorPage="true|false"
    info="information"
    isELIgnored="true|false"         EL 表示 Expression Language 。
    isThreadSafe="true|false"
    ```

    将所有的导包写在一行看起来并不雅观，所以可能需要写多行。只有 import 属性才能多次使用，其他的都只能使用一次。★

    ---

2. include：导入其他页面，如：我们喜欢将一个页面的 Header 和 Footer 等内容分开写如其他 JSP 文件中，于是就可以将它们导入：

    ```jsp
    <%--语法--%>
    <%@ include file="filename" %>
    
    <%--举例--%>
    <%@ include file="header.jsp" %>
    ```

3. taglib：导入外部的标签：

    ```jsp
    <%--语法--%>
    <%@ taglib uri="uri" prefix="fx" %>
    
    <%--举例--%>
    这里有一个标签：
    <navin>				浏览器并不知道这个标签是什么，于是报错。
    
    于是可以加上前缀：
    <fx:navin>			浏览器就知道这个标签属于 fx ，属于 uri 这个 Library。
        				前缀名可以随便取。
    <fx:h1>				自定义 h1 标签，而不使用 HTML 中的 h1 标签。
    ```

    
    
## Implicit Objects in JSP

### Built-In Object (can be used in Scriptlet and Expression)：

1. request (HttServletRequest)
2. response (HttpServletResponse)
3. pageContext (PageContext)
4. out (JspWriter) ~ PrintWriter object  
5. session (HttpSession)
6. application (ServletContext)
7. config (ServletConfig)

一个比较好的地方是 JSP 中不用实例化这些隐式对象。★

---

### pageContext

如果不指定范围，那么它不会像 session 那样，在任何页面都可用，它仅在此页面有效。但是可以指定一个范围（SESSION_SCOPE），使其范围与 session 一样，即在任何页面都有效：★
```jsp
<%--仅在此页面有效--%>
pageContext.setAttribute("name", "navin");
<%--获取属性--%>
pageContext.getAttribute("name");

<%--在所有页面有效--%>
pageContext.setAttribute("name", "navin", PageContext.SESSION_SCOPE);
<%--获取属性--%>
pageContext.getAttribute("name", PageContext.SESSION_SCOPE);
```

有很多 scope ，可以使用 pageContext 来设置。

这些隐式的对象直接使用即可，不需要实例化。

## Exception Handling in JSP

JSP 中也能使用 try/catch 来进行错误处理：

```jsp
<%
	try {
		int k = 9/0;
	} catch (Exception e) {
		out.println("Error: " + e.getMessage());
	}
%>
```

但这样使用`out.print()`方法来输出错误这种方式在 Web 中并不太好，虽然在 Core Java SE 中这样处理是非常好的。★

---

在 Web 中，我们最好使用一个单独的页面来展示错误，并使用不同的颜色等等与普通页面不同的元素：★

创建一个新的 JSP 文件：error.jsp

在遇到错误时要调用这个 error.jsp ，需要使用`<%@ page errorPage="error.jsp" %>`。★

如果 error.jsp 需要捕获出现的异常，即使用 exception 隐式对象，则需要在 Directive 中写：`<%@ page isErrorPage="true" %>`。★

exception 这个内置对象只能在 ErrorPage 中使用：★

```jsp
<body bgcolor="red">
	Error: <%= exception.getMessage() %>
</body>
```

## MVC using Servlet and JSP

Servlet 运行比 JSP 快，因为 JSP 要先转换成 Servlet 。★

不要将你的商业逻辑写在 JSP 中，不要将真正的 Java code 写在 JSP 中，如果你要添加一些东西，写在 Servlet 中即可。★

JSP 应该只能用来展示页面上的东西（view）。但是为什么不用 HTML 呢，因为它做的是静态网页，而 JSP 展示的则是动态网页。★

动态网页：当你浏览 facebook 时，有些内容是静态的，你能看到 设置，他也看到的是一样的，但是 个性化新闻 就不一样了，每个人登录都是不一样的新闻，这就是动态内容。

JSP 可以创建一个 Layout ，有一个页面专门是 layout ，没有其他内容。

MVC 分层：Client 需要的仅仅是那个 view，于是 JSP 只需要像它发送一个 view ，但是此时其中没有任何数据 (data) ，所以就有了 MVC 分层。这里 Client 像一个中间层 Controller 发送请求（如：/getPage 等，这个请求可以是任何请求，可以自定义），然后 Controller 收到请求后像 JSP 发送一个请求，并且其中包含 JSP 需要的数据（data），JSP 收到请求后，向 Clinet 发送 view 和 data 。

比如：我们在 JSP 中设计了一个 StudentProfile，但是没有数据，此时 Controller 通过发送一个 Student 对象来告诉 JSP 该向 Client 发送 view 了，并且 Controller 发送的那个对象中包含了 学生的信息 。那个对象叫做 model 。JSP 收到 model 后会将其中的数据（data）填充到该填充的空白部分。

那个 Controller 是你的 Servlet ，而 view 则是你的 JSP 。那个 model 是 POJO ：简单来说就是 Plain Old Java Object （原生的 Java 类？）。

如果要发送数据，只需通过 POJO 对象来发送数据即可，如：创建一个 Student 类。

如果要写商业逻辑 (bussiness logic) ，写在 controller 中，不要写在 JSP 中，JSP 应该只用来写 view 。★

那个 model 只是用来 容纳数据，并不做任何操作。★

如果要从 数据库 获取信息，在 controller 中与 数据库 建立连接，即在 controller 中写 JDBC 是不好的，因为 controller 的功能仅接收 Client 的请求并发送请求使 JSP 发送 view 给 client 。所以我们新建一个类，即你的 service 类，controller 去调用它来是 model 获取数据库中的数据。

service 类是一个普通的类，只是在`service()`方法中进行了一些操作，但我不会这样做。★

使用 service 类来连接数据库，将来数据库进行了一些改动，就不需要改动 controller ，只需改动 service class 即可。

但实际上使用 数据库 我们还要多一个层级，即 DAO (Data Access Obejct) 。你 (client) 向 contorller 发送请求，controller 调用 service class ，service class 调用 DAO 。DAO class 来向 数据库 进行数据的访问。

MVC 不包括 service class 和 DAO 。★

![MVC1](F:\Note\YouTube\JavaWeb\Telusko\Servlet&JSP\MVC1.png)

![MVC2](F:\Note\YouTube\JavaWeb\Telusko\Servlet&JSP\MVC2.png)

### 为什么要有 MVC 等 分层？

因为可以使代码独立出来，增加 可读性 和 可复用性 。

并且可以避免不同文件下 相同 变量名 的冲突。★★

## JSTL (JSP Standered Tag Library) part 1 EL

### 为什么会有 JSTL？

如果能将 Java 代码转换成 HTML 代码，更方便设计师去工作。

在 Servlet 的`doGet()`方法中：

Servlet 前面的注解 @Webapp("/xxx") 为该 Servlet 的路径，在浏览器地址栏后面添加 /xxx 地址即可访问，这里直接访问其调用的 JSP 文件中的内容。★

我们应该在 JSP 文件中的`<form action="MyServlet">`的 action 中不加`/`而在`@WebServlet("/MyServlet")`中加上`/`，否则会找不到资源。★★

```java
String name = "Navin";

request.setAttribute("label", name);
// 函数的参数为 JSP 文件的路径。
RequestDispatcher rd = request.getRequestDispatcher("display.jsp");
rd.forward(request, response);
```

这样就能够通过 Servlet 来调用 JSP 了。

display.jsp: 

```jsp
<%
	String name = request.getAttribute("label").toString();
	out.println(name);
%>
```

这是一种方法，但是当设计师看到 JSP 里面的 Java 代码时也会感到不爽。所以我们可以使用 Expression Language ：

```jsp
<%--格式--%>
<%--它会获取 Servlet 中的 label--%>
<%--它可以替代上面那段 Java 代码--%>
<%--它可以获取任意 JSP 中对象范围的 label ，比如：request scope, session scope, page scope, page context 等--%>
${label}
```

要使用 JSTL，我们必须在 Directive 中使用 <%@ taglib %>，因为 JSTL 是自定义标签。

## Part 2 Core Tags

引入 JSTL 标签：`<%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>`，jstl/ 后面还有许多，我们主要使用的是 core, functions 和 sql 。★

使用 JSTL ：

要使用 JSTL 必须要导入它的 jar 包，JSTL 1.2 。导入 jar 包后，如果是 IDEA，点击 File -> Project Structure -> Artifacts -> Output Layout 下的 Available Elements 下看看有没有刚刚添加的 jar 包，如果有，即 jar 包未导入成功，右击 jar 包 -> Put into Output Root 。★

要把它放在 Web App Library，并拷贝在 WEB-INF 目录下的 lib 目录下。★

```jsp
<%--JSTL 的 out 标签--%>
<%--输出 Hello World--%>
<c:out value="Hello World" />

<%--输出 label 对应的 name--%>
<c:out value="${label}" />
```

JSTL 中有许多标签，c:catch 使用来进行 异常处理的、c:import 导入其他网页。

### 使用 JSP 接收一个对象（Object）

Student 类：

```java
public class Student() {
    int rollno;
    String name;
    
    public Student(int rollno, String name) {
        super();
        this.rollno = rollno;
        this.name = name;
    }
}
```

Servlet : 

```java
Student student = new Student(1, "Fuck");
request.setAttribute("stu", student);

ReqestDispatcher requestDispatcher = request.getRequestDispatcher("display.jsp");
requestDispatcher.forward(request, response);
```

JSP 中：

```jsp
<%--这会报错--%>
<%--因为在 JSP 中接收 对象 需要 beans ，即需要 getter and setter ★--%>
${stu.name}
```

如果需要输出对象，那么需要在 Student 类中实现`toString()`方法。★

使用`<c:forEach></c:forEach>`循环：

```
<%--传递一个 List--%>
ArrayList<Student> students = new ArrayList<>();
students.add(new Student(1, "Rose"));
students.add(new Student(2, "Tom"));
students.add(new Student(3, "Jerry"));

request.setAttribute("stus", students);

<%--在 JSP 中使用 c:forEach--%>
<%--items 是要循环的对象，var 是每一次循环中的对象--%>
<c:forEach items="${stus}" var="stu">
	${stu} <br/>
	${stu.name} <br/>
</c:forEach>
```

## SQL tags Part 1

JSP 文件中：

```jsp
<%--连接数据库--%>
<%--连接完成后会得到 数据源，并将其存储在 db 中 ★--%>
<sql:setDataSource var="db" driver="com.mysql.jdbc.Driver" url="jdbc:mysql://localhost:3306/jdbc_start" user="root" password="134679" />

<%--查询--%>
<%--返回的结果集会存储在 resultSet 中 ★--%>
<sql:query var"resultSet" dataSource="${db}">select * from info</sql:query>

<%--要打印整个结果集，需要 MySQL connector/J 的 jar 包 ★--%>

<%--要使用 forEach ，需先 taglib 引入--%>
<c:forEach items="${reslutSet.rows}" var="row">
<br/>	<c:out value="${row.id}"></c:out> : <c:out value="${row.name}"></c:out> : <c:out value="${row.age}"></c:out>
</c:forEach>
```

JSTL 很强大，因为任何写 HTML 的人都能看懂它，没有任何 Java 代码。

## JDBC 数据库查询 浏览器 显示数据乱码问题 (From CSDN, ——氵青-风)

保持所有客户端编码一致。

将 IDEA 的字符编码该为 utf8 。

将数据库的很多东西改为 utf8 ：

```cmd
# 在 cmd 中，连接数据库后
show variables like "%char%";

# 然后将上面的一些东西改为 utf8
set character_set_client=utf8; set character_set_...=utf8; set ... ; ... ;
```

在用 JDBC 连接数据库的时候，在驱动语句后面加上：`?useUnicode=true&characterEncoding=UTF-8`，即：

```
jdbc:mysql://localhost:3306/jdbc_start?useUnicode=true&characterEncoding=UTF-8
```

在每个 JSP 页面头中添加以下三句话：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%request.setCharacterEncoding("UTF-8");%> 
    <meta charset="UTF-8">
```

## Function Tags

如果想知道字符串的长度、匹配字符串中的几个字符、或者是做一些操作，就可以使用 Function Tags 。

`prefix="fn"`。

```jsp
<c:set var="str" value="Navin Reddy is a Java Trainer" ></c:set>

${str}

Length : ${fn:length(str)}

<%--根据空格分割--%>
<c:forEach items="${fn:split(str,' ')}" var="s">
	<br/>
    ${s}
</c:forEach>

<%--根据 a 分割--%>
<c:forEach items="${fn:split(str,'a')}" var="s">
	<br/>
    ${s}
</c:forEach>

index : ${fn:indexOf(str,"is")}

is there : ${fn:contains(str,"Java")}

<c:if test="${fn:contains(str,'JSP')}">
	JSP is Der
</c:if>

<c:if test="${fn:endsWith(str,'Trainer')}">
	you are right buddy
</c:if>
```

function 有很多函数。

## Filter Theory

Filter 是经常别忽略的一个部分。

在 Servlet 中写 Filter 并不重要，但是某些情况下可以使用它。

每个 Servlet 可能都有一定的功能，比如：log, transaction, security。于是需要在需要这些功能的 Servlet 中写某个特定功能的代码，这样并不好扩展。于是我们可以将这些功能的代码 分离 出来，然后 client 根据这个分离出来的东西，即 Filter 去找某个需要该功能的 Servlet ，这样就有了扩展性。★

任意的 Filter 如果接受到的 request 不符合要求，就可以将其返回给 client 。

这些 Filter 和 Servlet 之间都是独立的，他们都不知道那个请求是从哪里来的。比如一个 Servlet 前面是一个 Filter，Servlet 并不知道 Filter 向它发送的 request 是 Filter 发来的。★

但是 Tomcat 会将他们连接起来 (叫做 filterchain) 。根据配置 web.xml ，可以决定请求的下一步走向。★

### 创建 Filter

创建一个类，来实现 Filter 接口，然后需要重写`init()`、`doFilter(req, res)`、`doDestroy()`三个方法。一般我们不用`init()`和`doDestroy()`，除非你要自己配置 Filter 。

---

Filter 可以像 Servlet 那样工作，但那不是它的主要目，它是用来 截取 (intercept) 请求的。★

我们也可以自己配置 Filter，跟 Servlet 一样：Servlet 有 ServletConfig，Filter 也有 FilterConfig 。★

![Filters Theory](F:\Note\YouTube\JavaWeb\Telusko\Servlet&JSP\Filters Theory.png)

## Filter Practical

我们可以在 Filter 中添加一些限制条件，如：登录时输入 id，我们可以让 输入的 id 不为 负。

在与 Servlet 同一个包中，创建一个 Filter 后，Filter 中：

```java
@WebFilter("/addAlien")
public class IdFilter implements Filter {
    public void doFilter(ServletRequets request, ServletResponse response, FilterChain chain) {
        PrintWriter out = request.getWriter();
        
        // 运行，如果控制台中出现 in Filter ，则说明该语句被调用，Filter 顺利工作。
        System.out.println("in Filter");
        
        // 我们需要的是 HttpServletRequest
        HttpServletRequest req = (HttpServletRequest) request;
        int aid = Integer.parseInt(request.getParameter("aid"));
        
        if (aid > 1) {
            // 这个 chain 是来调用下一个 Filter 的，如果下面没有 Filter 了，就调用 Servlet。★
            chain.doFilter(reuqest, response);
        } else {
            out.print("Invalid Input");
        }
    }
}
```

如果还需要对此 Servlet 创建 Filter，保证这些 Fitler 的 URL（ @WebFilter() ）里面的东西要一致。★

## Login using Servlet and JSP (Theory)

使用 Session management 来做。

这需要一些页面。有 login page, welcome page, videos page and about us page. 有些页面不需要登录也能访问，比如：about us page 和 login page (它本来就是用来登录的) ，但是其他的页面：welcome page 和 videos page 就必须要登录才能访问。

但是如果有人直接输入 videos page  的 URL ，他就可以跳过登录页面。怎样阻止他不登录就访问 videos page 呢？有两种方案，第一种是 Session，第二种是 Cookies 。★

使用 Cookies 并不安全，因为 Server 发送一个 Cookie 给 Client ，Client 就有权限访问它，甚至修改它，这样就能黑掉你的 Server，想怎么搞就怎么搞。★

所以我们使用 Session，它只保存在 Server 端，是比较安全的。★

但在 电子商务 (ecommerce) 上，Cookies 可以好过 Session 。★

---

我们在 login.jsp 中输入 用户名 和 密码，点击 登录 后，会跳转到 Servlet，在这个 Servlet 中将输入的 用户名 和 密码 保存在 HttpSession 中，然后跳转到 welcom.jsp 。在 welcom.jsp 中我们需要先使用`if()`语句验证 是否登录 ，即`session.getAttribute()`方法是否为 null ，如果为 null，则跳转到 login.jsp 。★

如果在 videos.jsp 中点击了 登出 按钮，跳转到一个 Servlet，在此 Servlet 中要将 Session 中的值 删除 ，即调用`session.removeAttribute()`方法。

在每个需要验证的安全页面都需要进行上述两句话中的 操作。★

---

在登出后我们还需要清除浏览器的缓存，因为登出后，如果有人在你电脑上点了 返回 按钮，他就可以随便使用你的帐号访问网页了，你就被黑了。这不安全。我们将在下节课来讲如何实现这部分。★

![Login Theory](F:\Note\YouTube\JavaWeb\Telusko\Servlet&JSP\Login Theory.png)

## Login practical Part 1

login.jsp: 

```jsp
<form action="Login">
    Enter username: <input type="text" name="uname"> <br/>
    
    <%-- type 使用 password ，这样输入密码显示的就是星号。★ --%>
    Enter password: <input type="password" name="pass"> <br/>
    <input type="submit" value="login">
</form>
```

login.java: 

```java
@WebServlet("/Login")
public class Login extends HttpServet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        String uname = request.getParameter("uname");
        String pass = request.getParameter("pass");
        
        if (uname.equals("telusko") && pass.equals("leanrings")) {
            HttpSession session = request.getSession();
            session.setAttribute("username", uname);
            response.sendRedirect("welcome.jsp");
        } else {
            response.sendRedirect("login.jsp");
        }
    }
}
```

welcom.jsp: 

```jsp
<%
	if (session.getAttribute("username") == null) {
        response.sendRedirect("login.jsp");
    }
%>

Welcome ${username}

<a href="videos.jsp">Videos here</a>

<form action="Logout">
    <input type="submit" value="Logout">
</form>
```

videos.jsp: 

```jsp
<%
	if (session.getAttribute("username") == null) {
        response.sendRedirect("login.jsp");
    }
%>

Videos
```

logout.java: 

```java
@WebServlet("/Logout")
public class Logout extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        HttpSession session = request.getSession();
        // login 的时候 set 了的 Attribute, logout 时就要删掉。★
        session.removeAttribute("username");
        // 删除所有数据 (data)
        session.invalidate();
        response.sendRedirect("login.jsp");
    }
}
```

## Login Part 2

当我们从 client 向 server 发送数据时，需要使用`doPost()`方法；如果从 server 获取数据，则需使用`doGet()`方法。★

将`doGet()`方法改为`doPost()`时，需要在`<form></form>`标签中将 method 属性的值改为 post ，因为此属性默认值为 get 。★

### 在 网页 中显示视频：

YouTube 任意一个视频点击 share -> Embed -> 将下面那段代码拷贝到 video.jsp 文件中。★

---

Http 协议会提供很多东西，如：Session, Cookies, 和最重要的 Cache 。因为 Cache，我们才可以迅速的访问网页。所以当我们登录后，登出，然后在点击浏览器的返回键，还是会回到登录后的页面，这样的页面叫做 (cached pages) ，这样就不安全。

我们可以告诉浏览器这是一个 secure page，使其不 cache ：

在 welcome.jsp 页面中 setHeader ：

```jsp
<%
	<%-- 第一个参数是 Label，浏览器知道 Cache-Control 是什么；第二个参数是 Instructions，也是浏览器知道的。 --%>
	<%-- must-revalidate 就是说每次请求访问该页面时都需要 重新验证 是否登录。★ --%>
	<%-- 这种方式 只对 Http 1.1 及更新的版本有效 --%>
	response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate"); // HTTP 1.1
%>
```

老版本的 HTTP 解决办法：在后面再添加一句话：

```jsp
<%
	response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate"); // HTTP 1.1
	response.setHeader("Pragma", "no-cache"); // HTTP 1.0
	<%-- 第二个参数表示时间， 0 second 或者 0 minute --%>
	response.setHeader("Expires", "0"); // Proxies
%>
```

video.jsp 中也是一样。

还有一种方式，就是使浏览器的 返回键 失效，但这并不靠谱，没有人希望自己的 返回键 被封，这样没人用你的网页。★

所以使用 setHeader 的方法是比较好的。

不同的浏览器使用的是不同的 Session Object，如：在 Chrome 登录后，打开 Safari 访问 video.jsp，它不会是登录了的状态。★

## Login JDBC Part 3

我们要保证所有的数据都来自数据库中。★

先建一个表，里面有 用户名 和 密码 两个字段，插入几条数据。

要用数据库，就要将 java 文件起名为 DAO ，这里为 LoginDao，包也在 com.google.dao 中。★

使用 JDBC 可以引入 jar 包，也可以将 项目 转换为 Maven Project，然后通过一段代码引入。

LoginDao.java: 

```java
public class LoginDao {
    String sql = "select * from info where uname=? and pass=?";
    String url = "jdbc:mysql://localhost:3306/login";
    String username = "root";
    String password = "...";
    public boolean check(String uname, String pass) {
        try {
            Class.forName("com.mysql.jdbc.Driver");
            Connection connection = DriverManager.getConnection(url, username, password);
            PreparedStatement preparedStatement = connection.preparedStatement(sql);
            preparedStatement.setString(1, uname);
            preparedStatement.setString(2, pass);
            
            ResultSet resultSet = preparedStatement.executeQuery();
            
            if (resultSet.next()) {
                return true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Login.java: 

```java
...
LoginDao dao = new LoginDao();
if (dao.check(uname, pass)) {
    HttpSession ...
    ...
} else {
    ...
}
...
```

## Servlet JSP JDBC Maven Example

Maven 是自动构建工具，帮你构建你需要的东西的配件，如：JDBC, Spring, JUnit 等等。★

### 创建 Maven Project

选择版本 -> webapp 1.0 -> Group Id: com.company , Artifact Id: ProjectName

与 Maven 交互，即 Maven 的配置文件：pom.xml (pom: project object model) , 里面是项目的依赖项，即 maven repository 中下面那段 maven 依赖代码，将其添加到 pom.xml 中即可。

MVC: model-view-controller

`doGet()`方法 fetch data from server ; `doPost()`方法 submit data . 

在 com.google.controller 中创建一个 Servlet，名叫 GetAlienController ；在 com.google.model 中创建一个 Alien 类。

model 只用来 接收请求 和 发送响应，处理数据库需要使用 DAO Layer ，所以我们在 com.google.dao 中创建一个 AlienDao 类 。★

创建一个 showAlien.jsp，这是 view 层。

建议使用 RequestDispatcher ，因为 sendRedirect 会改变网页的 URL ，我们并不希望这样来困惑用户。这背后发生的事情他们不需要知道。★

如果使用`sendRedirect()`，就不能使用`request.setAttribute()`来设置属性了，因为`sendRedirect()`之后，是一个新页面，客户端 也会重新向该页面发送一个 request object ，所以要使用 Session, Cookie 或者 URL Rewriting 。我感觉 Session 最好。——Navin ★

`forward()`方法是把 request 和 response 传给 jsp 文件。

### java.lang.NoClassDefFoundError: Could not initialize class com.google.util.JDBCUtils 问题解决

```java
// 将下面这句话改为最下面那句话
InputStream inputStream = JDBCUtils.class.getClassLoader().getSystemResourceAsStream("db.properties");
InputStream inputStream = JDBCUtils.class.getClassLoader().getResourceAsStream("db.properties");
```

错误原因：（ from stackoverflow : https://stackoverflow.com/questions/7615040/difference-between-classloader-getsystemresourceasstream-and-getclass-getresou ）

因为在 webapp 中，是一个 目录层级 （classpath hierarchies），而不是简单的一个目录，这个 目录层级 会在各个 webapp 之间共享。`getSystemResourceAsStream()`只能访问 顶层 层级，所以 在运行 的时候会找不到 db.properties 文件，而在 编译 的时候却能找到。★

一般来说，使用`getResourceAsStream()`是更好的选择，因为它将使用与代码所属的Class相同的类加载器，即它 包含了 `getSystemResourceAsStream()`。★