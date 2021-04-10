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

