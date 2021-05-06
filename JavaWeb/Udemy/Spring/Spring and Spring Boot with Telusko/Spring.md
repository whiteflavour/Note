# Spring and Spring boot

## 1. Getting Started

### 1. Introduction to Spring

有许多很好的框架：Struts、EJB、和关于数据库的 JPA。但是 Spring 包含了这所有的一切。★

> Spring 关注点在 POJO。

EJB 关注 Entity。

### 2. Spring Documentation

官网有很权威的文档，当然也可以买一些书籍。

> 推荐官方文档。还有电子书版本。

### 3. Prerequisites

有一些前置知识，不了解到时候暂停视频去看看，再回来都没有关系。

### 4. Software Requirement

任何主流 IDE 都行，但是 Spring 官方有个 IDE ，Google spring tool suite 。

需要 JDK 。这里使用 JDK 8，Spring 5 运行在 JDK8 上，当然也支持 9 。★

### 5. Spring Tool Suite (STS)

> 使用 Spring Framework 需要 Spring 依赖。

不知道 Maven 可以 Google How Maven Works 。★

也可以使用 Gradle ，很多人都在用。

> 去 mvn repository 搜索 Spring ，使用 Spring Context 依赖。

点依赖一下他就自动复制了。★

### 6. Dependency Injection (后面用 IoC 代替  (Inversion of Control) )

面向对象编程，需要对象的属性，可能需要调用其他类（如：一个笔记本电脑类需要 CPU 、RAM 和 硬盘，这些类都需要自己定义），可能需要自己构造一个 Singleton 类，或者 工厂类，但是通过 Dependency Injection，我们不需要管他，Spring Core 会给你（直接注入 CPU 对象，RAM 对象和硬盘对象）。但是并不是不需要干任何事，我们需要做一些配置。★

## 2. Spring Boot

### 7. Getting Spring Starter Project

New 一个 Spring Starter Project，这即是 Spring Boot 。★

有很多选项，如果要连 JDBC 就选择 JDBC，需要 Security 就选择 Security 。★

版本这里使用的是 2.1.2 。

创建好项目之后你会发现 Spring Boot 给你提供了很多依赖。

### 8. Dependency Injection in Spring

创建一个 Spring 项目，什么都不选（JDBC、Web、Security 。。。），直接 Next 。

StartApplication.java 中添加：

```java
// 老方法，不使用它。
// Alien alien = new Alien();


// 新方法：

// 点开 run 方法的 ConfigurableApplicationContext，可以发现它继承了 ApplicationContext 类。
ApplicationContext context = SpringApplication.run(StartApplication.class, args);
Alien alien = context.getBean(Alien.class);
alien.code();
```

### 9. Spring Boot Autowire

类中调用对象：@Autowired

StartApplication.java：

```java
ApplicationContext context = SpringApplication.run(StartApplication.class, args);
Alien alien = context.getBean(Alien.class);
alien.code();
```

Alien.java:

```java
@Component
public class Alien {
    @Autowired
    Laptop lap;

    public void code() {
        lap.complile();
    }
}
```

Laptop.java:

```java
@Component
public class Laptop {
    public void compile() {
        System.out.println("Compiling ... ");
    }
}
```

## 3. Spring Core -IoC

### 10. BeanFactory

这里不使用 Spring Boot，所以可以自己控制一些东西，因为我们要了解 Spring Boot 背后的原理。

于是我们创建一个普通的 Maven 项目（使用 quick start 骨架）。

Inversion of Control (IoC) ：它来帮你实例化对象，而不用自己 new 。★

**添加依赖**：Spring Context 。

App.java:

```java
public class App {
    public static void main(String[] args) {
        // 造手机有手机厂，造电脑有电脑厂 。。。 
        // 这种方法已经过时了，但是需要从头学起，还是得知道。
        // 因为没有使用 Spring Boot ，所以需要多一些配置，这就是为什么很多人喜欢 Spring Boot
        BeanFactory factory = new XmlBeanFactory(new FileSystemResource("spring.xml"));
        Alien alien = (Alien)factory.getBean("alien");
        alien.code();
    }
}
```

需要创建一个 spring.xml 文件，可以点击 New -> Spring Bean Configuration File (Eclipse) 。

spring.xml:

```xml
<bean id="alien" class="com.google.Alien"></bean>
```

这么少的类，还感觉不出来它的优势，当有几十个类的时候，你不需要了管理它们，Spring Framework 帮你管理。

### 11. ApplicationContext

改进：

App.java: 

```java
// 将上面那个工厂那句改为词句，因为上面那句工厂过时了。
ApplicationContext factory = new ClassPathXmlApplicationContext("spring.xml");
```

此时会报错，找不到 spring.xml 。

原因：因为是 new 的 是一个 ClassPath ... 类，**ClassPath** ，（解决方法：）所以需要将 spring.xml 移到 **java** 目录。

#### 路径问题：

Class Path 默认跟目录为 webapp 。

若要使用 classpath，可以在路径前增加前缀 ：`classpath:spring.xml` ；若不是 webapp，使用 file: 前缀：`file:spring.xml`（这里的默认根目录为 src ）。

From ：https://blog.csdn.net/rnzhiw/article/details/84199036 

### 12. Spring Container

Alien.java: 

```java
public class Alien {
    /**
     * 构造方法，用于确定 Alien 对象是否被创建。
    */
    public Alien() {
        System.out.println("Alien Object Created ... ");
    }
    
    public void code() {
        System.out.println("Coding ... ");
    }
}
```

App.java: 

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext factory = new ClassPathXmlApplicationContext("spring.xml");
        
        // 如果我们注释掉下面这两句，运行程序，发现会输出 Alien Object Created ... ，说明无论我们是否获取 Alien 的对象，它都会被创建。★
        // 原因：JVM 里有一个 Spring Container，里面存放一些 Java Beans 。只要上面那句话执行，就会创建其对象。
        
        /*Alien alien = (Alien)factory.getBean("alien");
        alien.code();*/
    }
}
```

#### Singleton Beans: 

再创建一个 Alien 对象：App.java: 

```java
alien.age = 15;
// result is 15
System.out.println(alien.age);

Alien alien2 = (Alien)factory.getBean("alien");
// result is also 15
System.out.println(alien2.age);
```

> 当我们创建第一个对象时，Spring Container 中已经有了 Alien 对象，直接使用它；创建第二个的时候也一样，不会再创建一个对象，它们（alien 、alien2）引用同一个对象。这就是为什么这些 Beans 叫做 Singleton Beans 。★

### 13. Singleton Vs. Prototype

spring.xml: 

```xml
<bean id="alien" class="com.google.Alien" scope="prototype"/>
```

#### 默认值：

scope 属性的默认值是 singleton ，可以设置为 prototype 。还有一些其他值，但不是 Spring Core 的，是其他模块的。★

#### 区别：

singleton ：只会创建一个实例（使用的单例设计模式 (Singleton Design Pattern) ）。并且即使不使用`getBean()`获取对象，只要有工厂，就会创建对象。

prototype ：创建多个实例。如果不使用`getBean()`，就不会创建实例。

### 14. Setter Injection

spring.xml : 

**值注入**：

```xml
<bean id="alien" class="com.google.Alien">
    
  <!--设置属性，从 setter 中获取，这样可以使其 age 的默认值为 10，而不是 0 ★-->
  <!--注意：property 中的 name 必须和 setter 的方法名一致，如：此处 name 为 age，则对应的 setter 为 setAge() ；若 name 为 age1 ，则 setter 为 setAge1 ★-->
  <property name="age" value="10"/>
</bean>
```

### 15. Ref Attribute

spring.xml: 

**引用注入**:

```xml
<bean id="alien" class="com.google.Alien">
  <property name="age" value="10"/>
  <property name="laptop" ref="laptop"/>
</bean>

<bean id="laptop" class="com.google.Laptop"/>
```

#### Bean 与 Property

Bean 即为类，像豌豆荚一样，里面夹着属性；Property 即为属性，就是类的成员。很形象，哈哈。

### 16. Constructor Injection

spring.xml: 

**指定构造器**: 

```xml
<bean id="alien" class="com.google.Alien">
  <!--指定构造器，若构造器参数是类，则把 value 改为 ref 即可★-->
  <!--此时使用的指定构造器（有参的，非默认构造器）-->
  <constructor-arg value="12"/>
  <property name="laptop" ref="laptop"/>
</bean>
```

Alien.java: 

```java
public class Alien {
    private int age;
    private Laptop laptop;

    public Alien(int age) {
        this.age = age;
    }
}
```

#### 怎么选择？

当类成员的值不是必须的，是可以选择的，则使用 setter （此时是使用默认的（无参）构造器），此时不要使用 constructor ，会出错（因为若使用 constructor，则必须使用有参数的那个，而不能使用默认的构造器，所以此时必须传值，若不传，则肯定报错）。★★

### 17. Autowire

当你的 spring.xml 文件中有许多 bean 时，你想使用任意一个，可以使用 autowire 属性来让 Spring 帮你自动搜索。

Alien.java: 

```java
public class Alien {
    private int age;
    private Computer computer;
}
```

spring.xml: 

**Autowire byName**: 

```xml
<!--此处的 autowire 是按名字搜索，还有一些其他的方式-->
<!--注意：这里的名字是 Alien 类中的除年龄成员之外的那个成员的名字，搜索与其名字相匹配的 bean-->
<!--上述成员的名字为 computer -->
<bean id="alien" class="com.google.Alien" autowire="byName">
  <property name="age" value="10"/>
</bean>

<!--此时匹配的是第一个 bean-->
<bean id="computer" class="com.google.Laptop"/>
<bean id="desktop" class="com.google.Desktop"/>
```

**Autowire byType**: 

```xml
<bean id="alien" class="com.google.Alien" autowire="byType">
  <property name="age" value="10"/>
</bean>

<!--下面两个 bean 类型都一样，都是继承 Computer ，并且 Alien 中另一个成员的类型为 Computer -->
<!--此时 Spring Framework 会产生冲突。解决方法：收看下一节-->
<bean id="laptop" class="com.google.Laptop"/>
<bean id="desktop" class="com.google.Desktop"/>
```

### 18. Primary Bean

#### autowire=byType 冲突的三种解决方法：

**1. autowire="byName"**

**2. 指定 property ：（IDEA 貌似推荐使用此方法）★**

```xml
<!--此时使用 laptop -->
<property id="computer" ref="laptop"/>
```

**3. Primary Bean：**

```xml
<!--指定 laptop 为 primary (默认) bean -->
<bean id="laptop" class="com.google.Laptop" primary="true"/>
<bean id="desktop" class="com.google.Desktop"/>
```

## 4. Spring MVC

### 19. Spring MVC Theory

目前有两种方式创建 Spring MVC 项目：

1. 配置（以前只有这一种）
2. Spring Boot （Spring Boot 的目的：Make things easy）

#### What is MVC ?

在以前，我们访问一个网页，如：FaceBook，每个账户的页面 Layout 是一样的，网页的设计是一样的，但是每个账户的数据是不同的。

> 现在讲究前后端分离，即每个部分只做该做的事情：Controller (Servlet) 处理请求并返回响应；Model (POJO) 传递数据；View (JSP) 返回页面。★

一个项目可能有多个 Servlet，而每个 Servlet 只处理一个请求。我们需要一个前置 Servlet ( May be a Filter? ) ，先让所有的请求通过它，然后在去寻找处理该请求对应的 Servlet 。而 Spring MVC 会给你这个前置 Servlet，它叫做：Dispatcher Servlet ，但其他的用于处理单个请求的 Servlet 需要自己创建。

**如何控制 Dispatcher Servlet 使其找到需要处理请求的那个 Servlet ? **

需要创建一个配置文件来配置，操作相对简单。

### 20. Spring MVC Getting Started

这里先使用 Spring Boot MVC，会做更少的配置，后面我们再使用普通的 Spring MVC 。

#### 创建 Spring MVC 项目：

创建一个 Spring Starter Project ，选择 Web 。

#### 重要的依赖：

spring-boot-starter-web ：此依赖包含了 MVC 。

**关于 Spring Boot：**

查看依赖，发现里面有 Tomcat 的 jar 包。Spring Boot 内嵌了 Tomcat，我们无需再配置 Tomcat 。

#### 运行 Web 项目：

main 目录中创建一个 webapp 目录，里面创建一个 index.jsp ，随便写点，然后通过 Spring Boot App 启动，发现开启了 8080 端口。

浏览器访问 localhost:8080 ，发现 Spring MVC 返回了一个错误页面。很好，不是 404 Page Not Found 。

**但是为什么没有返回我们的 JSP 页面？**

因为请求先要传给 Dispatcher Servlet ，然后再传给一个 Controller 进行处理，但是我们并没有 Controller 。

### 21. Creating Controller

创建一个类，不需要继承和实现任何类，只需要在前面添加`@Controller`注解，它即可成为 Controller 。

因为有 Spring Boot ，也不需要做太多的配置，如果需要做额外的配置，则需要创建一个配置文件。

HomeController.java: 

```java
/**
 * 此时并不会返回 JSP 页面，但是控制台能够输出了。
 */
@Controller
public class HomeController {
    @RequestMapping("/")
    public void home() {
        System.out.println("Home Page");
    }
}
```

HomeController.java: 

```java
@Controller
public class HomeController {
    @RequestMapping("/")
    public String home() {
        // 直接在此处 return jsp 页面即可。
        // 原理：因为是 Dispatcher Servlet 在管理请求，所以此处返回 jsp 页面，让 Dispatcher Servlet 来将请求转发给 JSP 页面。★
        return "index.jsp";
    }
}
```

但是还是会报错，但是此处产生了一个下载文件，我们的 JSP 文件的代码在此处，我们下载了该 JSP 文件。

解决方法：请看下一节。

### 22. Tomcat Jasper

要将 JSP 转换成 Servlet，需要一个依赖，Tomcat Jasper。注意：版本需要与 Tomcat 版本对应。

这样就能显示 JSP 页面了，而不是下载它。

### 23. Accepting User Input

做两个数相加：

index.jsp: 

```jsp
<form action="add" method="get">
  Enter a number: <input type="text" name="number-a"/>
  Enter another number: <input type="text" name="number-b"/>
  <input type="submit" value="Add"/>
</form>
```

HomeController.java: 

```java
@Controller
public class HomeController {
    @RequestMapping("/")
    public String home() {
        return "index.jsp";
    }

    // 可以在此方法中处理逻辑，也可以另外创建一个 Calculator 类来进行。
    @RequestMapping("add")
    public String add() {
        return "result.jsp";
    }
}
```

result.jsp: 

```jsp
Result is : 
```

此时提交后会显示 result.jsp 页面，但是不会显示结果，因为我们并未做任何其他处理，只是构造了一个页面。

**显示结果：**

改造 HomeController.java 中的`add()`方法：

HomeController.java: 

```java
@RequestMapping("add")
public String add(HttpServletReqeust request) {
    int num1 = Integer.parseInt(request.getParameter("num1"));
    int num2 = Integer.parseInt(request.getParameter("num2"));

    int sum = num1 + num2;

    // 2. Session: 
    HttpSession session = request.getSession();
    session.setAttribute("sum", sum);

    // 3. RequestDispatcher
    // 4. Cookie
    // 应该 Servlet 和 JSP 中能用到的转发技术都行。

    // 接下来有几种方式将结果转发给 JSP
    // 1. URL Redirecting: 
    return "result.jsp?sum=" + sum;
}
```

result.jsp: 

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false"%>
Result is : ${sum}
```

**工作原理：**

感觉 Dispatcher Servlet 就像是原始 Servlet 中的`service()`方法与 web.xml 配置文件的综合，它可以寻找到对应路径的映射，每次提交都是提交给 Dispatcher Servlet 。★

---

我们还能使逻辑处理更加简洁，请看下节。

### 24. @RequestParam

代码改进：

HomeController.java: 

```java
@RequestMapping("add")
// 使用 @RequestParam 注解获取 URL 参数，session 对象也由 Spring Boot 提供
public String add(@RequestParam("num1") int num1, @RequestParam("num2") int num2, HttpSession session) {
    int sum = num1 + num2;
    session.setAttribute("sum", sum);

    return "result.jsp";
}
```

那个 session 对象也可以去掉，下一节讲解。

> 经过测试，貌似不要 @RequestParam 也能工作 。。。

### 25. @ModelAndView

再改进：

HomeController.java: 

```java
@RequestMapping("add")
public ModelAndView add(@RequestParam("num1") int num1, @RequestParam("num2") int num2) {
    sum = num1 + num2;

    ModelAndView modelAndView = new ModelAndView();
    modelAndView.addObject("sum", sum);
    
    // 注意是 setViewName ，而不是 setView 
    modelAndView.setViewName("result.jsp");

    return modelAndView;
}
```

> ModelAndView 的好处就是它既包含了数据也包含了页面。

### 26. Prefix and Suffix

若需要使 JSP 文件不被别人输入 URL 直接访问（绕过了 Controller ），将它们放入 WEB-INF 文件夹；若需要将它们放入 webapp 中的一个文件夹中，需要在 application.properties 文件中做一些配置：Google 搜索 spring boot application properties 。

找到 Spring MVC ，找到 prefix 和 suffix ，我们需要这两个。

application.properties: 

```properties
spring.mvc.view.prefix=/view/
spring.mvc.view.suffix=.jsp

# 若需要使其对外不可见 (private) ，则使用下面这句：
spring.mvc.view.prefix=/WEB-INF/view/
```

> 缺点：所有的 JSP 后缀文件都只能放在同一个目录中，并且返回值不能再加后缀。★

这样，我们的 HomeController.java 文件中就只能这样写了：

HomeController.java:

```java
...
public ModelAndView add( ... ) {
    ...
    
    // 注意：这里不能加 .jsp 
    modelAndView.setViewName("result");

    return modelAndView;
}
```

### 27. Model and ModelMap

其他方式实现：

HomeController.java:

```java
...
public ModelAndView add( ... ) {
    ...

    // 可以直接在 ModelAndView 的构造方法中传递 JSP 文件名。★
    ModelAndView modelAndView = new ModelAndView("reuslt");
    modelAndView.addObject("sum", sum);
    
    return modelAndView;
}
```

HomeController.java:

```java
@RequestMapping("add")
// 也可以使用 ModelMap，它们唯一的区别就是 ModelMap 是装在一个 Map 中的。★
public String add(@RequestParam("num1") int num1, @RequestParam("num2") int num2, Model model) {
    sum = num1 + num2;

    model.addAttribute("sum", sum);

    return "result";
}
```

#### Model or ModelAndView? 

根据自己的情况。

> 建议：若只需要数据，或者先只需数据，后面再返回页面，则使用 Model；若数据和页面都需要，则使用 ModelAndView 更好。

### 28. Need of ModelAttribute

传递对象？

HomeController: 

```java
@RequestMapping("addAlien")
public String addAlien(@RequestParam("aid") int aid, @RequestParam("aname") int aname, Model model) {
    Alien alien = new Alien();

    alien.setAid("aid");
    alien.setAname("aname");

    model.addAttribute("alien", alien);

    return "result";
}
```

result.jsp: 

```jsp
Result is : ${alien}
```

Alien.java: 

```java
public class Alien {
    private int aid;
    private String aname;

    getter ... 
    setter ...

    toString() ... 
}
```

### 29. ModelAttribute

代码改进：

HomeController.java: 

```java
@RequestMapping("addAlien")
public String addAlien(@ModelAttribute Alien alien, Model model) {
    model.addAttribute("alien", alien);

    return "result";
}
```

再改进：

HomeController.java:

```java
@RequestMapping("addAlien")
public String addAlien(@ModelAttribute Alien alien) {
    return "result";
}
```

如果想要在 result.jsp 中使用与 alien 不同的名字，可以在 @ModelAttribute 中指定：

HomeController.java: 

```java
@RequestMapping("addAlien")
// 在 @ModelAttribute 中指定名字
public String addAlien(@ModelAttribute("a") Alien alien) {
    return "result";
}
```

此时 result.jsp 中可以使用名字 a ：

result.jsp: 

```jsp
Result is : ${a}
```

> 注意：虽然在 addAlien() 中 Alien 类型的对象名字为 a 时，在 result.jsp 中使用 alien 也能工作（但若在 @ModelAttribute 中指定了名字，就不能工作），但是会引起歧义，因此不推荐使用。★

### 30. ModelAttribute at Method Level

可以将 @ModelAttribute 设置在方法之前，这样每次调用其他方法之前，都会调用此方法：

HomeController.java: 

```java
... 
public class HomeController {
    // 调用其他方法之前优先调用此方法。★
    @ModelAttribute
    public void modelData(Model model) {
        model.addAttribute("name", "Aliens");
    }

    ... 
}
```

result.jsp: 

```jsp
<%--@elvariable id="alien" type="com.google.model.Alien"--%>
<%--@elvariable id="name" type="java.lang.String"--%>
Result is : ${alien} <br/>
Welcome back ${name}
```

### 31. Spring MVC Project

本节创建一个普通的 Spring MVC Project，不使用 Spring Boot 。

#### 创建项目：

首先创建一个 Maven 项目，骨架选择 webapp 。

#### 添加 Tomcat：

因为不是 Spring Boot，所以没有内置的 Tomcat，需要手动添加一个外置的 Tomcat 。

#### 添加依赖：

要使用 Spring MVC，需要添加依赖：maven repository 搜索 spring mvc -> 点击 Spring Web MVC 。

#### 运行：

将上面的 Spring Boot MVC 项目的文件拷贝过来，使用 Tomcat 运行。

> 此时运行会报 404 Page Not Found 错误，需要进行一些配置。下节课再讲。

### 32. Spring MVC Part 2

使所有请求通过 DispatcherServlet：

web.xml : 

```xml
<!--配置 DispatcherServlet-->
<servlet>
  <servlet-name>fuck</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
</servlet>

<servlet-mapping>
  <servlet-name>fuck</servlet-name>
  <url-pattern>/</url-pattern>
</servlet-mapping>
```

此时启动 Tomcat，报 500 Internal Server Error ，Can not open ServletContext resource [/WEB-INF/fuck-servlet.xml] 。

> 那个 xml 文件的名字就是 web.xml 中配置的 DispatcherServlet 时取的名字加上 -servlet.xml 。

我们需要在 WEB-INF 中创建这个文件 ( fuck-servlet.xml )：

> 不建议使用此版本，使用官网的版本。

```xml
<!--需要定义一个 beans 标签-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.0.xsd">
       
    <ctx:component-scan base-package="com.google"/>       
    <ctx:annotation-config/>
       
</beans>
```

> 根据官网，应该这样配置：★

fuck-servlet.xml:


```xml
<!--需要定义一个 beans 标签-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-3.0.xsd">
    <!-- DispatcherServlet Context: defines this servlet's request-processing infrastructure -->

    <!-- Scans within the base package of the application for @Components to configure as beans -->
    <!-- @Controller, @Service, @Configuration, etc. -->
    <context:component-scan base-package="com.google" />

    <!-- Enables the Spring MVC @Controller programming model -->
    <mvc:annotation-driven />
</beans>
```
此时启动 Tomcat ，报了不同的错误，404 Not Found，No mapping for GET / springmvc/index 。

**解决方法：**

此时需要再添加一个 bean 标签，使其在指定路径去寻找 View：

fuck-servlet.xml: 

```xml
...
<ctx:...>

<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver>
    <!--还需要添加一个 JSTL 的 property-->
    <property name="viewClass" value=org.springframework.web.servlet.view.JstlView"/>
    
    <property name="prefix" value="/views/"/>
    <property name="suffix" value=".jsp"/>
</bean>

...
```

此时报错，JstlView 类找不到，此时将添加的那个 JSTL 的 property 标签删掉，即可正常工作。

### 33. Post Mapping

回到 Spring Boot Project 。

首先在 web.xml 中的 form 标签中指定某种特定的方法 (POST)。

**方法一：**

然后在 HomeController.java 中方法的 @RequestMapping 中指定：

HomeController.java:

```java
...
// 在此处指定。
// 原本是两种方法都可以访问该方法，现只有 POST 能够访问。★
@RequestMapping(value="addAlien", method=RequestMethod.POST)
public String addAlien() {
    ... 
}
```

**方法二：**

将 @RequestMapping 改为 @GetMapping or @PostMapping ：

HomeController.java: 

```java
... 
// 使用 @PostMapping
@PostMapping("addAlien")
public String addAlien() {
    ...
}
```

### 34. Get Mapping

从 Server 获取数据：

HomeController.java:

```java
...
// 想要列出所有的 Aliens
@GetMapping("getAliens")
public String getAliens() {
    List<Alien> alienList = Arrays.asList(new Alien(1, "Jack"), new Alien(2, "Tom"));

    // 这里将报 404 Not Found 错误，因为 Spring MVC 默认将返回的 String 当作 jsp 的名字去寻找对应的 JSP 页面
    return alienList.toString();
}
```

修改：

HomeController.java:

```java
...
public String getAliens(Model model) {
    ...
    
    // 还需要添加属性至 Model ★
    model.addAttribute("result", aliens);
    
    // 将上面的 return 语句改为该语句，然后创建一个 showAliens.jsp 文件    
    return "showAliens";
}
```

下节将展示怎样只获取一个 Alien 。

## 5. Spring ORM

### 35. Spring ORM Theory

**ORM: **Object Relational Mapping. 

**映射关系：**

Java 是以对象为基础的（面向对象），所以可以将一个类中的成员变量映射到数据库表的每列，然后将每个类对象映射到不同的行。

![ORM 映射](F:\Note\JavaWeb\Udemy\Spring\Spring and Spring Boot with Telusko\ORM 映射.png)

要使用 Spring ORM，就要用到 JPA Hibernate 。

如果要开始事务，则要使用 Spring Transaction 。

### 36. Spring Hibernate Config

> 连接数据库可以使用普通的 JDBC，但是在大型项目中，使用 Hibernate 更好，因为它能更好的处理事务。★

**使用 Hibernate：**

需要添加几个依赖：★

maven repository 搜索 Hibernate Core -> 选择 Hibernate ORM Hibernate Core 。**原因：**使用 Hibernate 。

搜索 Spring ORM -> 选择 Spring Object/Relational Mapping 。**原因：**连接 Spring 和 Hibernate 。★

搜索 Spring tx ( transaction ) -> 选择 Spring Transaction 。**原因：**让 Spring 处理事务。

搜索 Mysql connector -> 选择 Mysql connecter/J 。

搜索 c3p0 -> 选择 C3P0 。**原因：**JDBC 连接池，可以限定连接数量。

**配置 fuck-servlet.xml: **

要使用，还需要做一些配置：

fuck-servlet.xml: 

```xml
<!--添加这几句-->
xmlns:tx="http://www.springframework.org/schema/tx"
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/mvc/spring-tx.xsd

<bean id="myDataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">
    <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/telusko"></property>
    <property name="user" value="root"></property>
    <property name="password" value="12345678"></property>

    <property name="minPoolSize" value="5" />
    <property name="maxPoolSize" value="10" />
    <property name="maxIdleTime" value="30000" />
</bean>


<bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
    <property name="dataSource" ref="myDataSource" />
    <property name="packageToScan" value="com.telusko.springmvc.model" />
    <property name="hibernateProperties">
    <props>
        <prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
        <prop key="hibernate.show_sql">true</prop>
    </props>
    </property>  
</bean>



<bean id="myTransactionManager" class="org.springframework.orm.hibernate5.HibernateTransactionManager">
	<property name="sessionFactory" ref="sessionFactory" />
</bean>

<tx:annotation-driven transaction-manager="myTransactionManager" />
```

### 37. MySQL and DAO

#### 下载 MySQL：

去官网，下载 Community 版本。需要下载一个 Server 和 MySQL Workbench 。

#### 使用 MySQL Workbench：

新建一个连接：

将 hostname 改为 localhost 。

#### 创建数据库：

```mysql
create database spring_mvc;
use spring_mvc;
create table alien(
	aid int,
    aname varchar(20)
);
insert into alien values(1, 'Fuck'), (2, 'Rose');
```

### 38. DAO Creation

创建一个目录：dao，在 Spring Boot 中是 repository 。（这里都行）

创建一个类 AlienDao ：

AlienDao.java: 

```java
// 使 Spring 帮你获取它的对象
@Component
public class AlienDao {
    // 如何获取这些 Alien 对象数据？
    // 要传递数据，需要用到 session ，要使用 session ，就要用到 SessionFactory 。★
    
    // 这里使用 @Autowired ，使其能够使用 primary-servlet.xml 中配置的 sesstionFactory 类。★
    @Autowired
    private SessionFactory sessionFactory;

    public List<Alien> getAliens() {
        Session session = sesstionFactory.getCurrentSession();
        // 若只获取其中一条 Alien 数据，则使用下述这句话：
        // session.get();

        // 要获取所有的 Alien 数据，使用如下这句：
        // 要转换为 List ，使用 list() 方法。
        List<Alien> alienList = session.createQuery("from Alien", Alien.class).list();
        
        return alienList;
    }
}
```

HomeControlller.java: 

要添加与修改的代码：

```java
@Controller
public class HomeController {
    @Autowired
    private AlienDao alienDao;
    ...

    @GetMapping("getAliens")
    public String getAliens(Model model) {
        model.addAttribute("result", alienDao.getAliens());

        return "showAliens";
    }
}
```

此时访问 .../getAliens ，会报 500 Internal Server Error，Could not obtain transaction-synchronized Session for current thread 。

**原因：**要通过 Hibernate 和 Spring ORM 从数据库获取数据，就需要先开启事务，获取完成后再 commit 。

**解决：**

AlienDao.java: 

```java
...
// 在此处添加注解：
@Transactional
public List<Alien> getAliens() {
    Session session = sesstionFactory.getCurrentSession();
    List<Alien> alienList = session.createQuery("from Alien", Alien.class).list();
    
    return alienList;
}
...
```

启动，再报 500 ，但是错误不同，此时是 Alien is not mapped 。

**原因：**要使用 Hibernate 或者 Spring ORM，需要确保 Model 类是 Entity，这样才能使用这些 Model 类去访问数据库表中的数据。（添加前面所讲述的类与数据库表的映射关系）。★★★

**解决：**

Alien.java:

```java
// 添加如下注解：
// 作用：添加该类与数据库表的映射关系。★★
@Entity
public class Alien {
    // 此注解表示该类成员是主键。★
    @Id
    private int aid;
    private String aname;
    
    ...
}
```

#### 控制台显示 SQL 语句：

此时在控制台会显示 SQL 的查询语句。若不想显示，则这样使用：

primary-servlet.xml:

```xml
...
<!--将以前的 true 改为如下的 false -->
<prop key="hibernate.show_sql">false</prop>
...
```

下一节讲新增一条 Alien 数据和只查询一条 Alien 数据。

### 39. Add and Fetch

**插入一条数据：**

AlienDao.java:

```java
...
@Transactional
public void addAlien(Alien alien) {
    Session session = sessionFactory.getCurrentSession();
    session.save(alien);
}
...
```

HomeController.java:

```java
...
@RequestMapping("addAlien")
public String addAlien(@ModelAttribute("result") Alien alien) {
    alienDao.addAlien();

    return "showAliens";
}
...
```

showAliens.jsp:

```jsp
${result}
```

**查询指定的某条数据：**

AlienDao.java:

```java
...
@Transactional
public Alien getAlien(int aid) {
    Session session = sessionFactory.getCurrentSession();
    // 这里也可以使用 load() 方法。★
    Alien alien = session.get(Alien.class, aid);

    return alien;
}
...
```

HomeController.java:

```java
...
@RequestMapping("getAlien")
public String getAlien(@RequestParam int aid, Model model) {
    model.addAttribute("result", alienDao.getAlien(aid));

    return "showAliens";
}
...
```

index.jsp:

```jsp
<!--添加如下代码-->
<hr/>
<form action="getAlien" method="post">
    Enter your id: <input type="text" name="aid" /> <br/>
    <input type="submit" value="Submit" />
</form>
```

## 6. Spring Data JPA

### 40. Spring Data JPA Configuration

#### 使用 Hibernate 有几个问题：

1. 要手动导入的依赖太多。
2. 配置太多 ( xml ) 。程序员不应该专注与配置，而应该专注于逻辑，这就是为什么会出现 Spring Boot 。
   Spring Boot 的配置是在 properties 文件中的，而非 xml ，这简单多了。

#### 使用 Spring Boot：

首先添加 MySQL Connector/J 依赖。

添加 Spring Boot Data JPA Starter -> 搜索 spring boot data 。可以去掉版本，因为上面的 Spring Boot 依赖已经定义过了，可以删去。

此时直接启动，报错，未指定 url ：

**配置：**

application.properties:

```properties
...

# 添加如下配置
spring.datasource.url=jdbc:mysql://localhost:3306/spring_orm
spring.datasource.username=root
spring.datasource.password=123456

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
```

此时启动，就不会报错了，其他的那些工作，我们下节课继续。

### 41. JPARepository

**获取所有 Alien 数据：**

创建一个接口：AlienRepo

AlienRepo.java:

```java
// JpaRepository 第一个参数为实体 (Entity) ，第二个参数为主键的类型。
public interface AlienRepo extends JpaRepository<Alien, Integer> {
}
```

HomeController.java

```java
...
@Autowired
AlienRepo alienRepo;

@GetMapping("getAliens")
public String getAliens(Model model) {
    // 这里虽然 AlienRepo 接口中没有定义任何方法，但是因为它继承了 JpaRepository，所以可以看到有许多方法可以使用。
    model.addAttribute("result", alienRepo.findAll());
    
    return "showAliens";
}
```

注：要成功运行，Alien 类必须要有默认构造函数。

> 这里那些接口中的方法 ( JpaRepository 及其上层接口 ) 并未定义，只进行了声明，但是竟然可以获得结果，这些都是 Spring Boot Data JPA 依赖的功效。

#### Spring Boot 的好处：

可以发现，同样的功能，使用 Spring Boot 和 Hibernate，Spring Boot 能减少很多代码。代码越少，错误就越少。★

> 使用 Spring Boot 也不需要使用 @Transactional 。★

### 42. JpaRepository Add and Fetch

**查询一条 Alien 数据：**

HomeController.java:

```java
...
@PostMapping("getAlien")
public String getAlien(@RequestParam int id, Model model) {
    model.addAttribute("result", alienRepo.getOne(id));

    return "showAliens";
}
...
```

**增加一条 Alien 数据：**

HomeController.java: 

```java
...
@PostMapping("addAlien")
public String addAlien(@ModelAttribute("result") Alien alien) {
    alienRepo.save(alien);

    return "showAliens";
}
...
```

根据主键查询是比较方便的，所以 JpaRepository 接口要求我们给他主键的类型，JpaRepository 的`getOne()`方法也是需要传递主键。但是如果我们想根据名字来插叙（非主键），应该怎么做？看下节。

### 43. Query DSL

**不根据主键查找：**

HomeController.java: 

```java
...
@GetMapping("getAlienByName")
public String getAlienByName(@RequestParam String name, Model model) {
    // findByName 方法是我们自己创建的，所以需要在 AlienRepo 中定义。
    model.addAttribute("result", alienRepo.findByName(name));
}
...
```

AllienRepo.java:

```java
public interface AlienRepo extends JpaRepository<Alien, Integer> {
    // 因为不根据主键查找，可能会有多个结果，所以返回一个 List 。★
    // 这叫 Query DSL (Domain Specific Language) . ★
    // 但是这也是有规则的，前面必须为 getBy or findBy ，后接类成员名字，首字母大写；后面也必须传递对应的参数。★★
    List<Alien> findByAname(String aname);
    
    // 还能进行排序
    List<Alien> findByNameOrderByAname(String aname);
    
    // 降序
    List<Alien> findByNameOrderByAidDesc(String aname);
    
    // 还可以使用 and 和 or 。
}
```

> 我们并未定义我们自己的`findByName()`方法，但是依然有效，这就是 Spring Data JPA 的神奇之处。★★

上述就是 Query DSL 的美。

关于如何自定义查询，看下节。

### 44. Query Annotation

根据 name 查找，但不使用`findByAname()`方法：

HomeController.java:

```java
...
public String getByName(@RequestParam aname, Model model) {
    // alienRepo.find 方法为自定义方法，使用它来根据 aname 进行查找。
    model.addAttribute("result", alienRepo.find(aname));

    return "showAliens";
}
...
```

AlienRepo.java:

```java
...
// :name 为占位符。find 函数中的 aname 参数传递给 @Param 中的 name 参数，然后再传递给 :name 。★
// 注：导包要为 data jpa 的包。
@Query("from Alien where aname= :name")
List<Alien> find(@Param("name") String aname);
...
```

## 7. Spring REST

### 45. What is REST

客户端与服务器之间传输数据，一般客户端是人在看，而服务器是机器；而人需要的是 HTML 页面（design），机器需要的只是数据（data）就足够了。两个机器之间发送请求、返回响应，有两种选择：

1. 使用 Servlet、JSP 或者 Spring MVC （它们强调的是 action ，一个 action 对应一个 URL 。）
2. 使用 Spring REST（强调名词（noun），如：www.abc.com/employee ，就展示出 employee 的数据。Java 正好可以，POJO 类就是这样。）

**被称作 REST （全名：RESTful Web Service/API ）的原因：**Representational、State、Transfer。

**REST 用途：**传送对象的状态（the state of the object）。

> 当你第一次给 Server 传送数据的时候，Server 会给你一个 Token，下次传送，你需要携带这个 Token 。★

我们依旧使用 HTTP 的 GET、POST、PUT 和 DELETE 方法。

### 46. Postman Setup

下载一个 Postman -> 在 Workspace 中 New 一个 Request -> 通过 URL 访问`localhost:8080/...`。

### 47. REST Getmapping

在 Postman 中使用 GET 方法输入 URL ：`localhost:8080/aliens`，会报错，404 Not Found，因为我们本来就没有处理 aliens 这个 URL 。

我们新建一个类 AlienController ，不建也行：

AlienController.java:

```java
@Controller
public class AlienController {
    @Autowired
    AlienRepo alienRepo;

    // 这里我们不再需要 Model，因为 Model 是通过 Session 传递数据，发送 JSP 页面，但这里我们不发送 JSP，我们只获取数据（data）。
    @GetMapping("aliens")
    public String getAliens() {
        List<Alien> alienList = alienRepo.findAll();

        // 因为不使用 JSP，所以不用返回 JSP 页面。★
        return alienList.toString();
    }
}
```

此时在访问`.../aliens`，依然报 404 错误，但是 message 中返回了所有的 aliens 。（根据自己尝试：貌似新版的 Postman 并未返回 aliens 的信息，message 那一栏为空字符串。★）

**原因：**我们返回的 String 默认是 Spring MVC 去寻找对应的 JSP 页面，因为我们在 application.properties 中定义过了 prefix 和 suffix 。

**解决：**告诉 Spring MVC 我们发送的不是 JSP ，而是真正的数据（data）：★

代码修改：

AlienController.java:

```java
@Controller
public class AlienController {
    ... 
    @GetMapping("aliens")
    // 添加此注解，以告诉 Spring MVC 该方法返回的是 data 。★
    @ResponseBody
    public String getAliens() {
        ... 
    }
}
```

但是还是有点小下次，我们需要返回的是 JSON、XML，但是只获得了 Plain Text 。

代码改进：

AlienController.java:

```java
@Controller
public class AlienController {
    @GetMapping("aliens")
    @ResponseBody
    public List<Alien> getAliens() {
        List<Alien> alienList = alienRepo.findAll();

        // 不使用 toString() 方法，直接返回 List 。★
        return alienList;
    }
}
```

要使用 POST 方法获取某个 alien ，看下节。

### 48. Jackson

我们通过上述操作返回了一个 JSON 的 List 。

**原理：**展开 Maven Dependencies，可以看到 jackson 的 jar 包 ( Spring Boot )，是它，使 Java 的 List 转换为 JSON 。

Google jackson documentation ，可以看到其文档，发现有 JSON Generator 。

### 49. PathVariable

获取一个 Alien ：

AlienController.java:

```java
@Controller
public class AlienController {
    ... 
    // 此时发现是有问题的，我们只能访问 104 ，而不能访问其他的 aid . ★
    @GetMapping("alien/104")
    @ResponseBody
    public Alien getAlien(int aid) {
        Alien alien = alienRepo.getOne(aid);

        return alien;
    }
}
```

此时启动，会报 500 错误。

代码改进：

AlienController.java: 

```java
... 
// 将 104 改为 {aid} : 
@GetMapping("alien/{aid}")
@ResponseBody
// 在 aid 前面添加注解 @PathVariable
public Alien getAlien(@PathVariable int aid) {
    ... 
}
...
```

又报 500 错误。

**原因：**@PathVariable 的参数没有映射到 aid 。

**解决：**在 @PathVariable 后面添加映射`("aid")`。★

再改进：

AlienController.java:

```java
... 
@GetMapping("alien/{aid}")
@ResponseBody
// 在 @PathVariable 后面添加映射 ("aid") 。★
public Alien getAlien(@PathVariable("aid") int aid) {
    ... 
}
...
```

此时还是报 500 。

**原因：**可能是方法使用错误。不知道为什么`getOne()`方法不行。

**解决：**将`getOne()`方法修改为`findById()`。★

AlienController.java:

```java
@GetMapping("alien/{aid}")
@ResponseBody
public Alien getAlien(@PathVariable("aid") int aid) {
    ... 
    // 使用 findById() 方法。★
    // findById() 返回 Optional ，为了避免返回空，产生 NullPointerException，所以需要添加 orElse() 方法。★
    Alien alien = alienRepo.findById(aid).orElse(new Alien(0, ""));

    return alien;
}
```

此时就能工作了，如果输入数据库中没有的 aid ，那么就会返回 aid=0, aname="" 的那条数据。★

### 50. RestController

可以直接将一个类声明为 RestController，而不用在每个方法前面添加 @ResponseBody ：

AlienController.java:

```java
// 声明为 RestController
@RestController
public class AlienController {
    @GetMapping("aliens")
    // 这里就不需要 @ResponseBody 了。
    public List<Alien> getAliens() {
        List<Alien> alienList = alienRepo.findAll();

        return alienList;
    }

    @GetMapping("alien/{aid}")
    // 这里也是。
    public Alien getAlien(@PathVariable("aid") int aid) {
        Alien alien = alienRepo.findById(aid).orElse(new Alien(0, ""));

        return alien;
    }
}
```

> 也可以在 @Controller 中使用 @ResponseBody ，混合返回 JSP 和 data 。★

### 51. PostMapping

在 Postman 中使用 POST 方法提交数据。

> POST 和 GET 的 URL 可以相同，因为它们是两个不同的方法，所以不会冲突。★

在 Postman 中：

POST : localhost:8080/alien ，提交，会报 404，因为我们并未映射这个 URL 。

还可以传递 KEY 和 VALUE：点击 Body ，form-data （也可以点击 raw ，自定义 JSON 格式 。★）-> KEY：aid ，VALUE：107；KEY：aname，VALUE：Komal -> Send 。因为未映射 URL ，所以还是报 404 。

**映射 URL ：**

AlienController.java: 

```java
...
@PostMapping("alien")
public Alien addAlien(Alien alien) {
    alienRepo.save(alien);

    return alien;
}
...
```

#### 只返回 XML ：

Postman 中使用 GET 方法 -> 点击 Headers -> KEY：Accept ，VALUE：application/xml -> Send 。

发现该方框区域的右下方，Status：406 Not Acceptable 。

**原因：**默认只支持返回 JSON 。

**解决：**需要添加一个 Jackson XML jar 包。★

### 52. Jackson XML

Maven Repository -> jackson dataformat xml 。

> 注：版本必须与 Spring Boot 中的 Jackson 版本一致。★

此时再获取所有的 Aliens ，就可以返回 XML 格式了。

### 53. Produces Attribute

#### 在 AlienController 中指定只返回 XML 格式：

AlienController.java:

```java
...
// 在此处中的 produces 属性中指定要返回的格式；花括号中可以指定多种类型，用逗号隔开。★
@GetMapping(path = "aliens", produces = {"application/xml"})
public List<Alien> getAliens() {
    List<Alien> alienList = alienRepo.findAll();

    return alienList;
}
...
```

但是此时在 Postman 中指定返回 JSON ( application/json )，就报 406 了。★

既然可以在 Server Side 指定返回 ( @GetMapping ) 特定的格式，那么也可以指定获取 ( @PostMapping ) 的数据的特定格式，见下节。★

### 54. RequestBody and Consumes Attribute

指定 POST 的特定格式：

Postman POST -> Headers -> KEY: Content-Type, VALUE: application/json 。

也可以在 Body 中的 raw 中选择 application/json ，然后自己编写 JSON 代码：

```json
{
    "aid": "10", 
    "aname": "Tom"    
}
```

此时 Postman 中 Send ，发现返回的结果不正常，虽然报 200 OK ，但是数据库中也没有成功插入数据。

**原因：**可能是我们写的 JSON 格式错误：aid 的值不应该加引号；并且 AlienController 中的`addAlien()`方法中的 Alien 参数前面未加 @RequestBody 注释。

**解决：**改进代码：

Postman -> POST -> Body -> raw -> JSON: 

```json
{
    "_comment1": "将下面键值对的值的双引号去掉", 
    "_comment2": "经过尝试，发现不去掉双引号也能识别出来，但感觉还是去掉更好，因为 Postman 返回的 Alien 数据是去掉双引号的，并且 aid 本来也是整型。★", 
    "aid": 10, 
    "aname": "Tom"
}
```

#### 附：JSON 的两种键值对注释格式：

```json
{
    "_comment1": "这是第一种格式", 
    "__comment2__": "这是第二种格式"
}
```

> 注：JSON 本身并不支持注释，因为它本身就很清晰。★

AlienController.java:

```java
...
@PostMapping("alien")
// 在 Alien 前面添加 @ReqeustBody 注解，来将 JSON 或者 XML 格式的数据转换为 Java 对象。★
// @ResponseBody 是将 Java 对象转换为 JSON 或者 XML 。
public Alien addAlien(@RequestBody Alien alien) {
    alienRepo.save(alien);

    return alien;
}
...
```

在 Server 端指定特定的格式：

AlienController.java:

```java
...
// consumes 的花括号内既可以像 produces 中一样使用双引号，也可以像下述这样使用 MediaType 。★
// Navin：我更喜欢双引号。
@PostMapping(path = "alien", consumes = {MediaType.APPLICATION_JSON_VALUE})
public Alien addAlien(@RequestBody Alien alien) {
    alienRepo.save(alien);

    return alien;
}
...
```

此时就只能 POST JSON 了。若此时 POST XML，报 415 Unsupported Media Type 。

## 8. Spring AOP

### 55. Why AOP

所有的应用程序都有一些共同点：

1. 维护日志
2. 维护安全
3. 处理事务

#### 日志：

例如：在 AlienController 中，每个方法调用时，都应该写一句日志，这里使用`System.out.println()`；然后在方法结束时，说明方法结束了。

当然我们还需要安全和事务。

#### 问题：

但是我们需要在每个方法中都写入它们，并且它们与处理逻辑的代码混在了一块，这样是不好的。

#### 解决：

所以我们应该将它们分离出来。

#### 行动：

新建一个类处理日志：LoggingAspect：

```java
public class LoggingAspect {
    public void log() {
        System.out.println("getAliens method called");
    }
}
```

如何在每个方法中都使用它，并且还不会污染逻辑代码？这就要用到 AOP ，请看下节。

### 56. AOP Terms

> Google Spring AOP Documentation 。官方文档。★

Spring AOP 本身不复杂，但是条款 ( terms ) 有点奇怪。

#### 一些概念：

**Aspect ：**即一些可以复用的与逻辑无关的类（如：Logging、Security 和 Transaction）。

**Join Point 与 Advice ：**我们在方法中需要调用这些 Aspects 的方法（ Logging 。。。 ），这些调用者方法被称为：Join Point ，而这些 Aspects 的方法被称为：Advice 。

**Pointcut：**我们调用 Aspects 的方法的时候，需要映射一些 URL （如：当调用`getAlien()`方法时调用`log()`方法，此时需要映射`getAlien()`），此时需要用到通配符，这些通配符就叫做 Pointcut 。

**Weaving：**最重要的一个。AOP 并不是新东西，一般我们所说的 AOP （非 Spring AOP ），需要将真正的方法与 Advice 连接。这种连接可以在编译或者运行时，但是 Spring AOP 在运行时完成连接。★

#### Types of advice: 

Before advice: 调用`getAlien()`时调用`log()`，`log()`先执行。

After advice: `getAlien()`先执行。

Around advice: 在执行`getAlien()`时执行`log()`。

### 57. Aspect and Before Annotation

使用普通 Spring 需要导入 Spring AOP jar 包，但是 Spring Boot 中自带了。

LoggingAspect.java:

```java
@Aspect
// 让 Spring 知道这个类是一个其中一个成员。
@Component
public class LoggingAspect {
    // 此处选择 Advice 类型，此处为 Before advice 。
    // 参数为 Join Point 的类，注意写上访问修饰符 ( public/private ) 、返回类型、加上包名的类名的方法名。★
    @Before("execution(public List<Alien> com.google.controller.AlienController.getAliens())")
    public void log() {
        System.out.prinln("getAliens method called");
    }
}
```

此时报错，说返回类型有问题。

**解决：**改进返回类型：

LoggingAspect.java:

```java
...
public class LoggingAspect {
    // 将此处的返回类型 List 中的 Alien 写全（加上包名），经自己尝试，List 也需要写全，可见异常麻烦，感觉还是通配符比较好。
    // 或者直接将返回类型使用通配符 * 代替：★
    // 如下所示：
    @Before("execution(public * com.google.controller.AlienController.getAliens())")
    @Before("execution(public List<com.google.model.Alien> com.google.controller.AlienController.getAliens())")
    public void log() {
        System.out.prinln("getAliens method called from aspect");
    }
}
```

> 重点是，逻辑代码都不知道还执行了 logging 。★

不只是 Logging ，Security 和 Transaction 都可以这样使用。★

下节使用 @After 。

### 58. Logger

使用`System.out.println()`的方式来写日志是不正确的，我们导入 lsf4j 的 Logger 包：

LoggingAspect.java:

```java
public class LoggingAspect {
    // 使用 Logger 。
    private static fianl Logger LOGGER = LoggerFactory.getLogger(LoggingAspect.class);

    @Before("execution(public * com.google.controller.AlienController.getAliens())")
    public void log() {
        // 将 System.out.println 替换为 Logger.info 。★
        Logger.info("getAliens method called from aspect");
    }
}
```

application.properties:

```properties
...
# 默认级别调为 info
logging.level.root=info

# 将日志输出到 app.log 文件中。★
# 此语句已过时，使用最下面一句：★
logging.file=app.log
logging.file.name=app.log
```

### 59. After Finally

LoggingAspect.java:

```java
public class LoggingAspect {
    @After(...)
    public void log() {
        Logger.info("getAliens method called");
    }
}
```

AlienController.java:

```java
@GetMapping("aliens")
public List<Alien> getAliens() {
    List<Alien> alienList = alienRepo.findAll();

    System.out.println("fetching aliens");

    return alienList;
}
```

> 文档中 After 有三种类型：After returning advice、After throwing advice 和 After (finally) advice 。默认是 After (finally) advice 。这个 finally ，跟 Java 中的 finally 关键字一样，无论 Join Point 是否报错，都会执行 Advice 方法。★★★

可以在 AlienController 中制造一个错误：

AlienController.java:

```java
@GetMapping("aliens")
public List<Alien> getAliens() {
    List<Alien> alienList = alienRepo.findAll();
    // 在此处制造一个错误，运行程序，发现控制台会输出我们的 Log 日志。★
    int i = 9 / 0;

    System.out.println("fetching aliens");

    return alienList;
}
```

另外两个 After 的使用，看下节。

### 60. AfterReturning and Throwing

直接将`@After`改为`@AfterReturning`或者`@AfterThrowing`即可。

## 9. Spring Security

### 61. What is Spring Security

安全是非常重要的。

> 注：我们这里讨论的是 Web Security ，不是 JVM Security 。

#### 应用举例：

最典型的例子就是登录登出：有一些页面是公共的，不用登录也能访问；而另一些则是私有的，需要登录后访问。★★

另一个例子则是密码的保存，我们会加密密码，但可能黑客会黑掉你的数据库，它们自然就有能力解密你的密码。★★

#### 算法举例：

现在流行的加密密码的加密算法是：Bcrypt 。

#### Spring Security

还有许多要用到的东西，这些都需要调用很多库、做许多配置，比较复杂，于是就有了 Spring Security ，它使维护安全更简洁。★

> Spring 并不会默认给你提供这所有的一切，你需要做一些配置。★

Spring Security 还会帮你 Authentication （认证）和 Authorization （授权）。

### 62. Spring Security Part 2

**创建 Spring Boot 项目：**

> 原因：普通的 Spring 配置太多，并且现在大多项目都是使用的 Spring Boot 创建。★

选择 Spring Starter Project -> 勾上 Web ( 如果是 JPA 的话也须勾上，但现在不用。)，也可以勾上 Security，也可以等会手动导入，这里我们不勾 。

**编写项目：**

创建一个 HomeController ，其中`home()`方法返回 index.jsp 。此时启动 Tomcat ，自动下载 jsp 文件，需要导入与 Spring Boot 内置 Tomcat 版本对应的 Tomcat Jasper 依赖。

**添加 Security ：**

导入依赖：Maven 搜索 Spring Security Boot -> Spring Boot Security Starter ( 可以去掉版本 ) 。

> 此时只要重启 Spring Boot App ，访问`localhost:8080`就跳到登录页面，而我们并未创建登录页面，只是添加了 Security 依赖。这就是 Spring Security 的妙处。★★

此时一切都是 Spring Security 管理，包括维持会话 (maintain session) 、Authentication and Authorization 。★

**默认用户名：**user

**默认密码：**Spring Boot App 的控制台中的日志会输出。

更改用户名和密码、使用数据库中的用户名和密码，看下节。

### 63. Spring Security Part 3

要自定义用户名和密码，需要做一些配置。

两种配置方法：★

1. Annotation
2. Create a Class

这里使用第二种，创建一个 AppSecurityConfig 类：

AppSecurityConfig: 

```java
// 此处添加下述两个注解
@Configuration
@EnableWebSecurity
// 此类必须重写以下两个方法。★
public class AppSecurityConfig extends WebSecurityConfigurerAdapter {
    // 我们需要用到 UserDetailService 的对象，所以需要 @Bean 。★
    @Bean
    @Override
    protected UserDetailService userDetailService() {
        List<UserDetails> userList = new ArrayList<>();

        // 此方法已经过时了，但我们这里只是理解，后面讲如何改进。★
        // 因为 Spring Security 不止可以认证，还能授权，所以我们可以使用 .role() 方法。★
        userList.add(User.withDefaultPasswordEncoder().username("Fuck").password("1234").roles("USER").build());

        return new InMemoryUserDetailsManager(userList);
    }
}
```

下节连接数据库。

### 64. Spring Security MySQL

AppSecurityConfig: 

```java
...
// 添加这个注释，是因为我们想让该方法的返回类型，即 AuthenticationProvider 成为 Bean 。★
@Bean
public AuthenticationProvider authProvider() {
    DaoAuthenticationProvider provider = new DaoAuthenticationProvider();

    return provider;
}
...
```

此时肯定不能工作，因为我们并未做什么连接工作。

#### MySQL 准备工作：

**添加两个依赖：**

spring boot jpa 、mysql connector 。★

**配置 application.properties ：**

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/spring_security
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

**创建 Model 类，映射到数据库：**

创建一个 User 类，类成员与数据库表中的字段一致，且创建 Getters and Setters 。★

> 记得添加 @Entitiy 和 @Id 。★

#### 编写：

AppSecurityConfig.java: 

```java
...
@Autowired
private UserDetailService userDetailService;

...
public AuthenticationProvider authProvider() {
    DaoAuthenticationProvider provider = new DaoAuthenticationProvider();

    // Contorller 与 Service 层通信，然后 Service 层再与 Dao 通信。所以这里我们还需要 Service 。★
    // 此方法，从数据库中获取数据。
    provider.setUserDetailService(userDetailService);
    // 这里我们不使用加密密码和 Hash 值，因为只是演示并理解其中的作用。现实中不推荐这么做。★★
    provider.setPasswordEncoder(NoOpPasswordEncoder.getInstans());

    return provider;
}
...
```

此时 userDetailService 这个对象并不知道我们连接了数据库，所以需要创建一个 MyUserDetailService 类来代表它：

MyUserDetailService.java:

```java
public class MyUserDetailService implements UserDetailService {
    @Autowired
    private UserRepository repo;

    // 因为此方法的返回类型是 UserDetails，而它是一个接口，所以还需要创建一个类来实现它。★
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = repo.findByUsername(username);

        if(user == null) {
            throw new UsernameNotFoundException("User 404");
        }

        return new UserPrincipal(user);
    }
}
```

还需要一个 UserRepository 接口：

UserRepository.java:

```java
public interface UserRepository extends JpaRepository<User, Long> {
    User findByusername(String username);
}
```

实现 UserDetails ：

UserPrincipal.java:

```java
/**
 * 将下面返回布尔值的方法全部默认改为 ture 。★
 */
public class UserPrincipal implements UserDetails {
    private User user;

    public UserPrincipal(User user) {
        this.user = user;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return Collections.singleton(new SimpleGrantedAuthority("USER"));
    }

    @Override
    public String getPassword() {
        return user.getPassword();
    }

    @Override
    public String getUsername() {
        return user.getUsername();
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}
```

此时会报错，无法注入 Service 。

**原因：**未添加 @Service 注解。

**解决：**在 MyUserDetailService 类中添加注解 @Service ：

MyUserDetailService: 

```java
// 在此处添加注解。
@Service
public class MyUserDetailService implements UserDetailService {
   ...
}
```

#### 对整个流程的总结：

使用 Security ，首先看 AppSecurityConfig ，它是最重要的。然后后面就是照着流程来了。★★

### 65. Spring Security BCrypt Password Encoder

