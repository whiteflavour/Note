# Java进阶与生活 —— 完成时间：2021.2

## 0. Base API

### 0-0. 引言

Java 与生活主要讲的是面向对象，这个基础要打牢。初学者实习出去写 Java 顶多就是写 HTTP ，API ，不会让你写多线程。顶多面试题问问你多线程的东西。面试题自己去准备，网上一堆。接下来的课程偏向于练习，一定要多练习。

### 0-1. API 的定义和用处

API ：Application Programming Interface 。Java 中的自带的那些有趣的函数，类，相当于 C 语言中的标准库的那一套规范，叫做 Java API 。API 是给客户用的。Java API 是给 Java 开发人员用的 API，方便程序员开发。

只要有 API ，就应当有对应的 API 文档。

只要把 API 文档研究透了，把源码研究透了，就知道 Java 的底层是怎么实现的，就对 Java 的理解更加深入（Java 虚拟机是更深入的东西）。你就知道所谓的高级功能，只不过是 API 文档里面的东西而已。

### 1. Scanner

**基础最重要！！（面向对象思想）**。

JDK 自带的源码用 IDEA 打开，该文件的图标上有一把锁。

<img src="F:\Note\Frank\My笔记（看完Frank的付费课后）\Java进阶\Scanner 源码.png" alt="Scanner 源码" style="zoom:300%;" />

---

**阅读源码的顺序（方法）：**充分利用 Java 的好处：社区庞大。

1. IDEA 中 ，Ctrl + 鼠标左键点击该方法，进入源码，阅读该方法上面的注释。
2. 如果读不懂，去 Java API 中找到该方法对应的那段注释，拷贝下来，谷歌翻译。
3. 如果还看不懂，把方法拷贝下来，谷歌搜索。

不用把所有的方法都精通，都弄明白，没有人能够弄明白，可能以后工作中会用到。可以先弄懂一些常用的。知道那是干什么用的。

### 2. Number

面向对象的伟大之处：将所有的内置类型包装为一个类来管理，这些类有一个共同的父类。方便管理。

**装箱**：将内置类型封装进对应的一个类中，将变量封装为对象。

**拆箱**：需要使用这个变量的时候（对该变量实行加减等），将其从箱子中取出来使用，使用完后又装回去。

Number 就是用面向对象思想把整个数据类型重新设计一下。所以面向对象特别强，有一本书叫 《Java编程思想》，特别屌，是大师级别看的，初学者看就是一头雾水，没有太大意义，不建议参考这本书，买来收藏可以。

### 3. Math

写工具类的时候可以把方法定义成静态方法，就不用 new 了，方便使用。

这一块可以根据兴趣去搞一搞，先会用，要知道有这么一个东西，原理的东西比较复杂。

### 4. Random

查看 jdk9 官方文档（Java9 API）：

1. 谷歌搜索 jdk9 doc 或者 Java9 API

2. 进入官方文档（API DOCUMENT），点击 FRAME ，如图所示：

    ![查看 Java9 官方文档](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\查看 Java9 官方文档.png)

3. 模块中选择 java.base 或者搜索，如图：

    ![Java9 API java.base](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\Java9 API java.base.png)

    ![Java9 API search](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\Java9 API search.png)

### 5. ThreadLocalRandom

ThreadLocalRandom 可以限制随机数的范围。而 Random 类限制有限，有的还根本不能限制。（虽然可以通过算法不用 ThreadLocalRandom 来限制范围，但是有现成的为啥不用，而且还能减少出错）

### 6. Date

很多方法都过时了。

看源码！！（带你们讨论源码，文档全部翻一遍，是不是很刺激，我觉得这才叫进阶——Frank）★

### 7. DateFormat 和 SimpleDateFormat

DateFormat 是一个抽象类，SimpleDateFormat 是它的子类，可以用它来将 Date 类型转换为想要的时间格式，也可以将一定的格式转换回 Date 。

### 8. Calendar

在程序中，西方国家定义月份从 0 开始。★

西方国家的星期日是一周的开始。★

### 9. System

Java 中 lang 包不用导入，直接用。★

System 中的 arraycopy 方法是系统级别的，性能可能比 Array 里面的高。

API 需要自己去深入研究，我只能领入门，这样你的 API 学的才够屌。——Frank ★

一些方法实在不会用，直接复制谷歌，看看那些论坛上是怎么写的，就会了。

讲这些的目的不是让你们去背会 API，而是让你们去熟悉 API，熟练去掌握它，能够使用上述方法去学习其他的 API，哪怕是没有讲过的  API 。

java base 里面的东西非常常用，可以去玩儿玩儿。一个 java.util 就够你玩一阵子了，不是让你全部精通。——Frank ★

数据结构应该在学 Java 之后学，Java 有面向对象的思想，好学，能够理解（数据结构）。——Frank ★

## 1. unit test and main function

### 0. 抛出企业问题，脱离 main 测试，模块化概念抛出

业界上没有 Base API 这种说法，是我这么教的。——Frank

main 方法是程序的入口点，程序从这开始执行。

一个项目只能有一个 main 方法，所以在企业中不能写多个 main 方法来进行测试。

以往的测试方法：在 main 中测试。（调用函数，打印结果，看输出是否符合预期）——预期结果和测试结果都是通过人工计算。

main 方法中不能有太多的逻辑性语句或者功能性的语句，像这种语句都应该抽离出去，变成一个函数。（你不能在 main 中编写一个函数，因为它的复用性很差，如果把它变成函数，复用性就很强了）

main 函数中只有一条或者很少的语句，没有判断性逻辑的成分，没有模块功能化的成分。

这很不容易，肯定会遇到问题，遇到问题肯定就是你技术学的不行，记住我这句话。——Frank

main 就是让程序开始运行的东西，不应该有测试的东西。

main 就是一个程序的入口点，而不应该是处理逻辑、功能模块的一个点。当清楚这点的时候，你的编程思想就已经和你的同学远远甩开了。★

### 1. JUnit单元测试的含义和用途

以前的那种方式不符合企业规范，你会发现牛逼的框架 main 里面就一句话，`runApplication();`，其他的就没了，其他的都是扯淡。（这叫做模块化编程，把它模块化、函数化）

JUnit ：Java 的单元测试框架。

单元测试是给程序员用的，不是给测试人员用的。

### 2. maven repository 获取 junit.jar

JUnit 使用最新版，用最新版肯定会出问题，出现问题我们去解决，不要怕。——Frank

可以在官网去学习一下怎么用：

![查看 JUnit 官方文档](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\查看 JUnit 官方文档.png)

---

maven 后面学框架要用到，不是让你去搞什么东西，只是让你下 jar 包，不是让你安装一个 maven 。★

只是告诉你有 maven repository 这个东西，能搜索到你想要的任何 jar 包，记住这个网站。★

如果学了 maven 或 gradle，就可以直接把这段话引入到 maven 里直接用：

![使用 maven 导入 jar 包](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\使用 maven 导入 jar 包.png)

---

maven 就是一个中央仓库，大家还在 Java 基础阶段，不用它，还太早了。——Frank

**下载 JUnit**：

1. 谷歌搜索 maven repository ，并进入。
2. 搜索 JUnit ，选择 JUnit，进入：

![下载 JUnit 的 jar 包](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\下载 JUnit 的 jar 包.png)

3. 选择 4.13 ，下载最新版本：

![下载 JUnit 最新版本的 jar 包](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\下载 JUnit 最新版本的 jar 包.png)

我们下载 jar 包引入用（最原始的方法）：将其下载到桌面

![maven repository 下载 jar 包](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\maven repository 下载 jar 包.png)

---

maven repository 是官方网站，绝对权威，就别在百度上去搜 jar 包了，那是愚蠢的行为。——Frank

### 3. 使用 JUnit

jar 包就是牛逼的网站或者开发工程师编写的程序，提供给开发人员使用，他发布到网上，然后你去下载了后引入，就可以使用别人的函数、API 。

**引入 jar 包**：（学了构建工具（maven、gradle 或更先进的构建工具）之后就不用引入 jar 包了，（因为很麻烦），直接配置一下就好了。）

1. 创建一个文件夹 lib：

    ![引入 jar 包 1](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\引入 jar 包 1.png)

---

2. 将 jar 包拖入该目录：

![将 jar 包拖入 lib 目录](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\将 jar 包拖入 lib 目录.png)

3. 现在此 jar 包是不能展开的：

![刚拖入的 jar 包](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\刚拖入的 jar 包.png)

4. 右键点击该 jar 包，点击 `add as library...`：

![将 jar 包添加到库](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\将 jar 包添加到库.png)

5. 成功之后遍可以展开该 jar 包：

![引入 jar 包成功](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\引入 jar 包成功.png)

---

测试的正确做法企业文件夹应该必须有一个对应的 test 文件夹，然后放进去进行单例测试（每个测试用例（编写的另一个用来测试该函数的函数）是独立的）。★

测试本身就是一个模块。

**用注解的方式使用 JUnit** ：（前提是引入 JUnit 这个 jar 包）

- 测试 sum 函数：

    ```java
    package com.google
    
    import org.junit.Test
    
    /**
     * 没解决预期结果和测试结果是人工计算的这个问题
     */
    public class CalcTest {
    	@Test
    	public void sum() {
    		int sum = Calc.sum(1, 2);
    		System.out.println(sum);
    	}
    }
    ```

*运行时出现错误（出现使用最新版 jar 包产生的依赖问题）*：java.lang.NoClassDefFoundError: org/hamcrest/SelfDescribing ......，需要引入一个依赖包：★

![使用最新版 jar 包的依赖问题](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\使用最新版 jar 包的依赖问题.png)

进入下载 JUnit jar 包的页面，往下翻，有一个编译依赖（Compile Dependencies），里面有一个出错时对应的包：

<img src="F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\引入依赖包.png" alt="引入依赖包"  />

---

然后将其引入。

### 4. Assert 断言

```java
package com.google

import org.junit.Test
import org.junit.Assert

/**
 * 测试通过，并且没有输出了，这才是最有逼格的地方，不是 printf。
 */
public class CalcTest {
	@Test
	public void sum() {
		int sum = Calc.sum(1, 2);
		Assert.assertEquals(3, sum);
	}
}
```

### 5. 更进一步，合理编写随机测试，完善代码

```java
package com.google

import org.junit.Test
import org.junit.Assert

import java.util.concurrent.ThreadLocalRandom

/**
 * 这时候就不是人工计算了，只用看测试结果和期望结果是否相等
 * 摆脱了 main 和 printf 这种傻逼的操作
 */
public class CalcTest {
	@Test
	public void sum() {
		int numberA = ThreadLocalRandom.current().nextInt(-9999， 9999);
		int numberB = ThreadLocalRandom.current().nextInt(-9999， 9999);
		int sum = Calc.sum(numberA, numberB);
		
		Assert.assertEquals(numberA + numberB, sum);
	}
	
	@Test
	public void subtraction() {
		int numberA = ThreadLocalRandom.current().nextInt(-9999， 9999);
		int numberB = ThreadLocalRandom.current().nextInt(-9999， 9999);
		int sub = Calc.sub(numberA, numberB);
		
		Assert.assertEquals(numberA - numberB, sub);
	}
}
```

main 方法中的测试只要一步错了后面的可能都会受到影响，而且如果出错了是哪个地方错了都不知道； JUnit 中的测试每个函数是独立的，互不影响，而且每个模块的错误很清楚。

用 main 方法来进行单例测试也是存在的，但最常用的还是使用 JUnit 进行单元测试。

## 2. StringBuilder

### 0. String 存在的问题

以后的 Demo 可以直接在 JUnit 里面写。

String 要多练习，要知道有这么个东西，这是非常重要的。

String 的对象是不可改变的，一旦创建，就不能更改它了，如果要修改，String 会创建一个新的对象，开辟一块新的内存，而不是在原先的对象上修改（所以才叫不可修改，只能创建，这样是极其耗内存的）：

```java
String s1 = "Hello";
String s2 = " World!!"
s1 = s1 + s2;
// 此时的 s1 不是以前的那个对象了，是新开辟的一块空间，是一个新的对象
// 原本的那个 s1 指向的那块内存还是存在的，在垃圾堆中，但是还没有被回收。
```

---

![修改 String ](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\修改 String .png)

---

### 1. StringBuilder 以及链式调用

为了解决 String 不可修改的问题，当我们要频繁对 String 进行修改的时候，不推荐使用 String ，而使用 StringBuilder 或 StringBuffer 。多数情况下使用 StringBuilder，它的速度更快；如果要求线程安全，则使用 StringBuffer 。

![StringBuilder 修改对象](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\StringBuilder 修改对象.png)

---

trimToSize 方法的作用是去掉线性表中空余的内存（StringBuilder 会自动扩容，当字符的长度越来越大时，后面的空余也会越来越多）。当确定了这个 StringBuilder 的长度过后，并且确定不再修改它，那么应该最后调用一下该方法，节省内存。

这里面最常用的应该是 append ，其他的你们可以自己去搞一下。——Frank

**链式调用**：（方法连续调用）

```java
// 链式调用
stringBuilder.append("Hello ").append("World").append("!!");
```

## 3. Throwable

### 1. 异常的介绍

遇到错误首先定位它的错误类型，知道这个错误是什么，知道它是哪来的。这叫定位错误。

异常是比较简单的。——Frank

异常看 API 先看 Throwable ，它是所有异常类的爸爸。

这些异常你全都弄明白，报个错你马上就能定位它在哪。所以说异常非常屌。应该点进去熟悉一下这些异常都是干啥的。也不是所有的异常你都要背会，这不现实。基本上犯错犯多了，你基本就明白这些是什么东西。

报错了应该去看看这些错误是什么东西，API 文档就是这个时候用的。

这些异常应该多看看，多想想。——Frank

### 2. 异常举例以及解决常见错误 bug 方案

报错了，应该直接在官方文档中搜索错误类型：

![Java 报错](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\Java 报错.png)

---

有人说异常的入门是 try 和 catch ，其实并不是，是认识这些异常。——Frank

报错很少报 Error ，因为 Error 很难解决，或者说不能解决，那是严重的错误（系统级别的错误）。

---

![Java 错误定位](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\Java 错误定位.png)

---

### 3. RuntimeException

1 / 0 的错误并不是编译异常，因为在 IDEA 中的 out 包下面对应的路径下发现有那个类的对应 class 文件，代码已经编译了，说明我们的语法没错，程序运行的时候出错了。我们管这玩意儿叫做运行时异常。

运行时异常可处理可不处理，只是不符合用户使用逻辑。我可以不给用户解决这个问题，也没人能把你怎么的。但是客户就倒霉了。

如果是编译错误，IDEA 中的 out 文件夹下就不会出现对应的类的 class 文件。

反射在写框架的时候会用到。

### 4. trycatch 作用以及诱骗毕业设计

处理异常新手能学的就两种方式：

1. try catch
2. throw

**毕业设计万一哪个错误解决不了的时候巧妙的欺骗老师**：（不要用在企业中）★ 

在 catch 中什么都不写：

```java
try {
	// ...
} catch(Exception e) {

}
```

---

**try catch 的作用**：

定位代码可能出现的异常。实际上现在最好别用 try catch 。

### 5. NullPointerException 空指针异常

Objects 类是检查对象的工具类。

如果你学到了 `<T>` 、 `<E>`什么的，那都是写框架级别的了。

try catch 是检测异常，抛出异常是 throw new NullPointerException 。

### 6. throws

可以直接抛出异常：

```java
@Test
public void demo() {
	throw new NullPointerException();
}
```

如果用 throw new 这种方式抛出异常，可以在方法后面添加 throws ：

```java
@Test
public void demo() throws FileNotFoundException {
	throw new FileNotFoundException();
}

// 如果需要抛出的异常太多，可以直接抛出 Exception
@Test
public void demo() throws Exception {
    throw new FileNotFoundException();
}
```

### 7. throw 和 trycatch 区别深度剖析，用途剖析，自定义异常

在开发东西的时候，如果程序遇到错误，你就不应该让他继续执行，否则会引发一连串的错误。

为什么要使用 throw 和 throws 配合这种方式，因为这样运行的时候就报错了，开发者就知道解决这个异常。如果仅仅是输出，这个程序还会继续往下执行，然后一堆东西都错了。这就是为什么你写的东西一堆错误。

throws 和 throw new 这种方式叫做抛出异常，try catch 叫捕获异常，两个是不一样的。一旦出现异常，就要想办法捕获异常。这一块你们要理解，代码可能还用的少。

如果把所有的异常都用 try catch 包起来，就没有异常了，所以 try catch 诱骗毕业设计，太屌了。

一般情况下用 throw new 。异常的可能性一定要给够，如果哪一天你写的代码出 bug 了，一下就能定位到错误在哪。

**自己定义异常**：

如果在编译的时候错了，就继承 Exception ；如果在运行的时候错了，就继承 RuntimeException 。一般情况下我们定义的时候直接就继承 Exception ，谁 tm 继承 RuntimeException 。——Frank

Exception 是编译的时候检测，RuntimeException 是运行的时候检测。这就是为什么我们自己写的异常类一般直接继承 Exception，因为我们希望错误直接就在编译的时候提出来，而不是在运行的时候。

### 8. 手把手教你编写装逼自定义异常

自己编写异常如果用 Exception 的构造函数，这样和 Exception 有什么区别呢？

实际开发过程中这一块应该是架构师去做的，但是我今天带着大家搞一遍。——Frank

**自定义异常**：

1. 定义一个 ErrorCode 接口：

    ```java
    public interface Error code {
    	/**
    	 * 获取错误码
    	 */
    	String getCode();
    	
    	/**
    	 * 获取错误信息
    	 */
    	String getMsg();
    }
    ```

2. 创建一个枚举：

    ```java
    public enum FrankCodeEnum implements ErrorCode {
        // 后面学 HTTP 接口就要出现异常。
        NOT_FOUND_PAGE("404", "找不到网站资源"),
        NOT_FOUND_FILE("888", "找不到文件异常")，
        NOT_O_TEN("233", "只能求0-10以内的加法！")， // 第一个参数是胡乱定义的，在企业中千万不能胡乱定义。
    	;
    	
        private final String code;
        private final String msg;
        
        FrankCodeEnum(String code, String msg){
            this.code = code;
            this.msg = msg;
        }
        
    	@Override
    	public String getCode() {
    		return code;
    	}
    	
    	@Override
    	public String getMsg() {
    		return msg;
    	}
    }
    ```

3. 定义异常类：

    ```java
    public class FrankException extends Exception {
    	public FrankExcepton(ErrorCode errocode) {
    		super(errorcode.getMsg());
    	}
    }
    ```

4. 调用自己的异常类：

    ```java
    public class StringBuilderTest {
    	public int sum(int a, int b) throws FrankException {
    		if (a > 10 || b > 10 || a < 0 || b < 0) {
    			throw new FrankException(FrankCodeEnum.NOT_O_TEN); // 也别在这里面写字符串了，来个枚举，多骚
    		}
    		return a + b;
    	}
    	
    	@Test
    	public void test() {
    		try {
    			int number = sum(19, 21);
    		} catch (Exception e) {
    			e.printStackTrace();
    		}
    	}
    }
    ```

getCode 可能暂时用不到，在 HTTP API 可能会用到。在这里写只是告诉你们规范。——Frank

## 4. File

### 0. 引言

现在不是高中，只需要把知识点背会，区分就行了。现在主要是实用，以及为什么在这个技术点上实用，Java 为什么要有这个东西。

要学文件流，先要知道 文件、文件夹、文件路径。如果这些都不知道，就别学了。——Frank

### 0-1. 必须先弄清楚快递怎么寄才能明白相对路径和绝对路径

绝对地址：无论在哪寄货都能寄到那的地址。范围最大。

相对地址：以某个地址为基准，相对于该地址，要去另一个地址，应该怎么去。例如：我在上海市徐汇区，要去上海市闵行区，那么我就不用出上海，直接从徐汇区走到闵行区就行了，于是我要填写地址为闵行区；如果我在北京市朝阳区，那么要去上海市闵行区就必须先离开北京，再进入上海，于是我要填写地址为上海市闵行区；如果我在非洲，同理，我应该填写的地址为亚洲中华人民共和国上海市闵行区；再例如我在火星，那么应该填写地球亚洲中华人民共和国上海市闵行区。这就是相对地址。

### 1. 绝对路径

文件和文件夹的区别：文件夹中可以放多个文件或文件夹。

**Windows10** 下的绝对路径：磁盘符:\文件夹`\`...\文件名.文件后缀

作用：立马确定它在哪，无论我现在在什么位置。

### 2. 相对路径

这个东西非常重要，你必须要学会，如果不能学会，那基本上凉了。

比如在某个地方右键打开 VS Code ，VS Code 就以该地方为基准，如果要找到该目录下的某个文件，那么可以直接 “文件名.文件后缀” 。那么这个 “文件名.文件后缀” 就叫做相对路径。

在 VS Code 中右键点击文件，可以拷贝它的绝对路径和相对路径。

### 3. File

讲这么多就是为了让 Java 来获取绝对路径和相对路径。

**Windows 与 Linux 中表示目录的标志不同**：★

windows 下：\ ，在 Java 中需要用 `\\`来表示目录，因为 Java 中，`\`表示转义字符，所以需要用 `\\`来表示`\`本身。

linux下：/ 。

windows UNC ：在 Java 中用`\\\`表示目录。

java.io.File 类中最常用的构造方法是 File(Stirng pathname) 。★

这些方法要多去尝试一下，多去练习一下。★

递归的效率太慢了，但是你不得不知道。

一定要注意 CSDN 上的小屁孩，专业度还是优点问题。★

写简历把所谓的个人荣誉放在后面去，把专业技能和你开发过的项目放到前面去，用了什么东西，担当了什么职位，解决了什么问题，这些都很重要。实习经历可以先去掉，把项目经验摆上来。★

### 4. Linux 上的绝对路径是有所不同的

/ 是 Linux 中的根目录。

## 5. IO Stream

### 1. 相对论理解 IO 流

IO Stream 是一个过程。★

关于流，我们想到了流动性，自然而然就像到另外一个东西，叫做管道。

例如：国家水库供水，

![相对论理解IO流](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\相对论理解IO流.png)

### 2. 汉语文学理解IO流

国家水库和家，两个相对于谁来说谁是输入谁是输出，中间有一个管道，谁连上谁，这是很重要的。

不仅仅是水，数据也是如此。我们可以想象数据是否也像水一样流动呢？这样想你就会觉得 IO 流好简单。

### 3. 图解 IO 流

![IO Stream](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\IO Stream.png)

英文好可以尝试去翻译一下，不好也无所谓，因为用到的只有这两张图。我们看这两张图的时候，就能深刻体会到它们带来的魅力。

如果要使用流，要建立流，要建立通道，来传输水，或者数据，我们需要两方的支持，一个是源头，一个是目标，然后中间建立管道，然后使数据进行流通，这是 IO 流的过程。

图1中的 Data Source 就是数据源，可以理解为国家水库；这几个箭头就是通道（管道）——流；Program 是目标，相当于家。

相对于数据源来说它是 output （输出）；相对于目标而言，它是 input（输入）。★

数据源可以是一个程序，一些文件（比如说用播放器打开一个小电影，播放器要去读它，是不是小电影流到程序里）或者说数据库，服务器（将文件上传到百度云，我们去百度云的服务器上下载）。

输入可以理解为获取。

我们的读和写都是相对于我们目前的程序而言。★

所以读为 input ，写为 output 。当我们往程序中写入数据时，比如说往记事本中输入一些东西，保存，对于记事本这个程序来说，是 output ，对于数据源来说是 input 。如图2。

明白了这些，接下来就非常简单了。

所以读，用的就是 input stream 。

### 4. 俩亲爹InputStream和OutputStream

要用 Java 来操作流，就要使用 java.io 这个包。

你会发现 API 的东西太多了，其实能用到的寥寥无几，如果你把这些都学会了，而且都用上了，那你就是大牛，没得说。

我们的关注点在这：FileInputStream 、FileOutputStream ，这是我们关注的重点。用它们来操作文件。

它们的父类 InputStream 、OutputSream 是抽象类，不能 new ，要用只能用它们的儿子。

### 5. FileInputStream 字节流读取文件

这是最原始的读取方式，它一个字节一个字节的读。但是要想学骚的，你必须得 OK 。

在 IDEA 中创建一个 file 目录，右键点击，选择 Make Directory as ，选择 Resources Root 。

![创建资源文件根目录](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\创建资源文件根目录.png)

---

向 FileInputStream 的构造函数中传入 IDEA 复制的文件路径的时候，选择 Path From Content Root 。

![IDEA 复制资源文件的路径](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\IDEA 复制资源文件的路径.png)

---

流用完之后一定要记得把它关闭，如果不关闭是非常恐怖的，内存一直存在，没有释放。★

如果不关闭，打开任务管理器，IDEA 的内存都飙了一个多 G 了。

close 方法关闭整个流，就相当于把管子切断，拽掉，不用了，就比较节省内存。

### 6. FileOutputStream 字节流写入文件

这种方式非常 low ，等会我们介绍牛逼的。你还不能跳过，必须先把它听懂。

要学会定位，比如说在 IDEA 中查找 write 方法，Ctrl + F ，然后输入 `write(` 。

FileInputStream 和 FileOutputStream 是最原始的方法，也是最有效的。

### 7. buff 缓冲复制文件

用 FileInputStream 和 FileOutputStream 也是 OK 的，至少能运行。一定要记得抛出异常，这个很重要。

文件的字节输入输出流还有一个用途，就是文件的拷贝，但是要把 byte 数组设的非常大。但是你要注意，它可能会卡，卡是正常的，待会儿我们再说这个问题。它不限制是 txt 文件，还可以是媒体文件（mp3、mp4 或者说图片）。★

要一个一个字节的去读，那太复杂了，可以借助一个缓冲。

复制后，可以右键点击该文件，选择 `Show in Explorer` ，然后会在资源管理器中显示该图片。

![在资源管理器中查看文件](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\在资源管理器中查看文件.png)

---

直接读就是一个字节一个字节的读，而借助缓冲区就可以一次读 1024 个字节（先把 1024 个字节的数据放入缓冲区里，等会读的时候一次从缓冲区里读完）——相当于搬动西的时候，直接读就是一小件一小件的搬，使用缓冲区就是一箱一箱的搬。

虽然使用缓冲区看上去很快，但是当拷贝大文件的时候，真的是令人堪忧，但已经解决了很大的问题了，总比一个字节一个字节的去扣要好得多。

知道怎么用，知道怎么回事儿就行了，再写一写，练一练。

### 8. buffered 字节缓冲流和装饰设计模式

使用缓冲的这种方式 Java 已经给我们实现了，而且比我们自己写的这种蠢方法要好得多，我们完全可以不用使用自己写的这种方式，但是我们要知道有这么一回事儿。

Java 给我们提供了 BufferedInputStream 和 BufferedOutputStream 来读写文件，代替我们自己写的缓冲，读写就快得多。

**装饰设计模式**：构造方法中的参数类型是一个类（相当于 vip 豪华套餐，把之前的套餐拿过来，升级一下权限。先要定义一个指定的类，才能用这个类）。

BufferedOutputStream 它的缓冲区大小默认直接就是 8192 ，我们刚才创建的缓冲区大小是1024 ，所以要明白它的源码是怎么写的。

复制文件的时候别再傻不拉几的在去用 FileInputStream 和 FileOutputStream 了，还要自己写个缓冲区，这是最傻的方式。直接用 BufferedInputStream 和 BufferedOutputStream 就行了。

你问我还有没有更好的，好的还在后面，这只是介绍基础。—— Frank

### 9. FileReader 和 FileWriter ，俩专门来搞 txt 文件的

前面我们讲的属于俩亲爹 InputStream 和 OutputStream 的子类的那些流等都是字节流——以字节为单位读和写。

**字节流的好处**：可以读写任何类型的文件（txt，图片，mp3，mp4，视频，音频），这些文件都可以化为字节，这个时候j就可以通过程序的字节流来读写这些文件。

但是我们读 txt 文件用字节流感觉有点那个了，Java 也专门提供了用来处理 txt 文件的类。我们可以在 java.io 中找到Reader，Writer，这些类就不属于 InputStream 和 OutputStream 了，它们就是字符流，但我们都不用。

我们用 FileReader 和 FileWriter ，这两个就是专门用来处理 txt 文件的。它们专门针对像记事本这种输入输出设备文件文件。

它们的使用上与前面的没有任何区别。它们的原理也基本上是一致的，这个看起来比较清爽，但还是有区别的，待会儿我们再讲。

实际上我们应该用 BufferedReader 和 BufferedWriter 来复制和读写 txt 文件，快。

### 10. BufferedReader 和 BufferedWriter

使用 BufferedWriter 去写文件，别再用 FileWriter 了。BufferedWriter 有一个单独的换行符方法，就不用去写一个 \n 了，因为不同的系统换行符可能不一样。

同理，使用 BufferedReader 去读文件，它有对应的 readLine 方法，读一行。

所以以后读文件和写文件就用这个，但是我都不用。—— Frank

### 11. 一次性讲解剩余的 N 个流（扩展课）Java 里那些极其骚的 IO 流

用字节流操作字符流的转换流——InputStreamReader 。将字节流转换为字符流去操作，然后再转换回来。但是要注意操作的是字符流，那操作的肯定是文本文件，不能是图片，所以转换流的时候要清楚你的目的是什么。这个用的不是特别多，但有时候突然会有这种需求，你要知道有这么回事儿。

有很多流，可以去试试，上班的时候可能也就是用常用的那几个。

并发是比较难的，并发是一门学问。

LineNumberInputStream 废弃了，废弃了也可以去看一看，知道它为什么被废弃。

Java 中的有些方法它太全了，太完善了。

泛型是写框架的。

Flie 类和流联合起来使用是非常强的。

### 12. Apache Commons IO

可以直接下载 apache 的 commons io 的 jar 包引入来使用。

apache 公司写了很多有意思的代码，比如说 FileUitls类 ，有很多有意思的方法，可以去研究一下。

所以我们前面的东西都白学了吗？没有，基础的东西不学会肯定不行。

使用 FileUtils 类代替 IO 流来操作非常方便，异常方便！—— Frank

FileUtils 里面的方法需传入 ArrayList ，它太方便了，以后创建一个 Strudent 类，直接把对象全部写进去，增删改查太简单了。

网上很多代码，可以参照，去研究一下。Appache 不会让你失望。

如果我早点把这个东西拿出来，你们就学不会文件流了，因为这里面都没有文件流的概念。

### 13. IO 流结束语

要传入的参数很重要。一定要看清楚它传的是什么东西。

Appache Commons IO 对你来说你要知道它是一个工具。所以说想要使用文件或者流等，它最适合不过，它会简化很多东西。只用一两句话就搞定，非常爽。

## 6. Charset

### 0. 阶段

IO 流这部分是比较难的。

最基础的部分一定要学会，不然谈什么深入。

我们没必要以这种愚蠢的方式去复制文件——以字节的方式，Java 中正好有一个 Files 类，里面有复制文件的方法——copy 。当然使用 Apache 的 IO 包也可以，条条大路通罗马，什么用着习惯就用什么，什么适合做这个项目就用什么。

java.nio 这个包里面其实还有点东西。—— Frank

我强烈建议多练习练习这些 API 。—— Frank

从 0 - 5 这几个部分，我告诉了你 API 应该怎么学，你应该能自己解决很多问题。 —— Frank

### 1. 字符集编码吹 B

电脑里面本身是不能存字符的，存的是一些 0101... 的东西。

Java 采用 Unicode 编码，所以设置 Eclipse 和 IDEA 的时候直接把编码改成 UTF-8 。

Unicode 里面的 UTF-8 是最常用的，是国际标准。

Java 是向万维网迸发的，UTF-8是万维网的主要编码形式，所以我一直强调 Java 的编码一定要是 UTF-8 。

在 IDEA Settings 中，选择 File Encodings ，将编码全部改成 UTF-8 。因为你每创一个新项目，可能 Default Encoding 就变成了 GBK 。

如果将 GBK 编码的程序放到 UTF-8 中，中文会乱码。

企业当中字符编码一定是统一的，那就是 UTF-8 ，这一点非常重要。

从国际化抓起，养成好习惯。

你们知道它是怎么来的就行。

不管你的老师教你的什么编码，那绝对是有问题的，全部统一使用 UTF-8 。

### 2. 转换

无论是软件，视频，解构，总共存在两种状态 —— Encode(编码)，Decode(解码)。这就是为什么有的视频需要安装解码器，视频也需要编码，有很多种编码格式。

如果使用 VS Code 打开，分别将编码设置为 UTF-8 和 GBK ，中文的显示将不同。

将你老师发给你的 GBK 文件转换为 UTF-8 文件：

```java
// CSDN 中名为“狗剩和翠花”的人写的代码
package wx.jq.util;
 
import java.io.File;
import java.io.IOException;
import java.util.Collection;
 
import org.apache.commons.io.FileUtils;
 
/**
 * 文件夹中的文件批量从gbk编码转换为utf-8编码
 * @author jiangqiang
 * 2016年7月5日 上午11:24:24
 */
public class FileEncodeConverter {
 
	private static String sourcePath = "C:/Users/jq/Desktop/weekend110-代码/weekend110/src";// 文件夹源路径
	private static String destPath = sourcePath + "_copy";
 
	public static void main(String[] args) throws IOException{
		File sourceDirectory = new File(sourcePath);
		File destDirectory = new File(destPath);
		if (!sourceDirectory.isDirectory()) {
			return;
		}
		// 获取文件夹中的所有.java文件，包括所有子级文件夹中的文件
		Collection
   
     files = FileUtils.listFiles(sourceDirectory, new String[] { "java", "JAVA" }, true);
		for (File file : files) {
			String absolutePath = file.getAbsolutePath();
			String newDir = absolutePath.replace(sourceDirectory.getName(), destDirectory.getName());
			// 把单个文件从gbk编码转化到utf-8编码，生成新文件，可以自动创建父级目录
			FileUtils.writeLines(new File(newDir), "UTF-8", FileUtils.readLines(file, "GBK"));
		}
		// 删除源目录,子文件都删除
		FileUtils.deleteQuietly(sourceDirectory);
		// 把生成文件目录重命名成源目录名
		destDirectory.renameTo(new File(sourceDirectory.getAbsolutePath()));
		System.out.println("success");
 
	}
 
}
```

我没讲编码和解码当中具体的那些实现，你知道怎么用就行了。

## 7. Multithreading

### 0. 问题的提出

提出问题往往比解决问题更重要，提出一个好的问题，可能会让你对这个知识的理解大大提高。

软件工程为什么要提出多线程这一概念？

CPU，中央处理器，是电脑的脑子。单核的 CPU 一次只能执行一个程序，但我们不能每运行一个软件都去买一台计算机。但计算机的鼻祖比较聪明，一个脑子不能多用，我们就让它切换着用。

我们可以最小化浏览器，让它暂停（挂起），然后去聊天。在肉眼看来这两个程序是同时运行的，实际上是脑子切换快。你的脑子可没有电脑的脑子切换快。就会给你一种错觉：电脑同时执行多个程序。**这是单核 CPU**。

**多核 CPU**：各干各的，就不用切换了。可以同时执行几个程序。

所以 CPU 有几核几线程的概念。核心越多，速度就快，因为切换是要消耗资源的。

（多核心可以比作我有多个工人，可以同时干多种活；而单核就只有一个工人，这一块干完了去干另一个。）

### 1. 核心数、进程、线程

![CPU核心、进程与线程](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\CPU核心、进程与线程.png)

### 2. 进程和线程的本质区别以及应用

**进程与线程**：

一个程序至少有一个进程，一个进程至少有一个线程。

对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。

**并发与并行**：

*并发*：没钱。在有限的 CPU 核心下来回切换以执行多个程序的手段，我们称之为并发。

*并行*：有钱，买多核 CPU 。能够同时执行几个程序，互不影响。

### 3. 多线程程序含义和作用的提出

一个进程可以理解为一个应用程序。

主函数本身就是一个线程。

**创建线程的两种方式**：

1. 继承 Thread 类（java.lang.Thread）：必须重写里面的 run 方法。（调用自建线程类的方法，想要看出与单线程执行的区别，需要套一个死循环，让程序一直执行。）
2. 实现 Runnable 接口。

CPU 切换线程特别快。

**start 与 run 方法的区别**：start 方法会多开启一个线程。start 自动调用 run 方法。

多上手，你就能理解它了，去写写案例。

### 4. 多线程的执行过程

![单线程程序与多线程程序的执行过程](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\单线程程序与多线程程序的执行过程.png)

主线程运行的同时也执行子线程。

### 5. Runnable

Java 单继承，实现 Runnable 接口的方法适用于该类已经继承了一个类了，不能再继承 Thread 了。

用匿名内部类来创建线程的方式不可扩展，不灵活。

### 6. 简化操作以及线程名

多线程是比较有讲究的，你需要多学好多东西才能够学习到它的精髓。

### 7. 抢鞋——多线程案例

*多线程的核心*：多个线程操作一个共享变量。

什么叫多线程编程？就是多个线程对一个共享变量进行抢占的这种编程方式。

### 8. 后台守护线程的提出（Daemon）

setDaemon() 、isDaemon() 方法。

前台线程：明摆着抢的这种。

后台线程——守护线程：可以用来垃圾回收、更新等 ...

守护线程一定要优先执行。

### 9. 匿名内部类创建线程——你们老师最喜欢用的

你老师认为是比较有逼格的方式，在我看来是愚蠢的行为。——Frank

也可以使用 lambda 表达式，但 JDK 版本必须在 8 及以上。

### 10. 发现问题，提出 synchronize 的概念和用途

线程不同步（线程不安全）问题 —— 解决方法：Java 中有同步方案：锁或者同步方法（同步代码块）。

### 11. synchronized 同步方法

将同步代码块抽离出来，变成函数。

推荐使用同步方法，这样同步的是哪一块就很清晰。

### 12-1. Lock、ReentrantLock同步锁

使用锁对象的这种方式是比较 low 逼的。

同步锁的这种方式使用比较广泛，一下子就能看到哪里上锁哪里解锁。它更灵活。

提出问题：Lock 锁和 synchronized 到底有啥区别？为什么说 Lock 锁更符合面向对象的这种思想、它更灵活？

### 12-2. Unlock 遗留问题

新手不建议使用 Lock 锁，因为它依赖你对多线程编程的理解。

unlock() 方法应该放在 finally 语句块中。

Java 并发深入研究的方向，有两本推荐的书（Java 核心技术系列）：《并发编程》《并发编程的艺术》★

随着 JDK 版本的更新，synchronized 的性能也在变好，所以用 synchronized 能解决的问题就用 synchronzied ，Lock 锁比较复杂，是比你职位高太多的人去设计这个锁的。

当你 Web 、框架、Java 都学得差不多了，可以去进阶一下多线程，现在去学就浪费时间了，因为进阶的多线程可能在工作的两年之内你都用不到。

### 13. 浅谈 synchronized 和 Lock 的区别

操作得当的话 Lock 的性能要高于 synchronized 。当然实际用什么还要看需求，如果需求足够，用 synchronized 还是非常不错的；如果是高并发的内容，还是需要设置一下 Lock 锁。

可以去网上看一下，多看一下，多练练。

实习基本上用不到它。除非突然有一天 Java 的门槛高了，可能需要多了解一下并发这块。

### 14. Thread API 说明

可以稍微了解一下

### 15. CPU线程调度、Priority 线程优先级、优先级常量以及小问题

每一个线程的优先使用权是系统随机分配，人人平等，谁先分配到谁就先用。

耍赖：我们赋予某一个线程拥有至高使用权——优先级。

分配优先级的这种方式成为 CPU 线程调度。

Java 分配优先级的方式——抢占 CPU 资源。

main() 主线程——优先级的值为 5。

CPU 执行太快了（多核心的），可能还没开始调度，程序就已经执行完了。

优先级依赖于操作系统，尤其是 Java

所以在进行多线程设计的时候，不要依赖于优先级，它有时候拿不准。

了解一下就OK。

### 16. join 线程插队

调用 join() 方法，先执行该线程。

### 17. sleep 线程休眠

优先级、插队、休眠、让步，这几个叫做 CPU 调度。

### 18. yield 线程让步

这个不是太重要。

为什么打印的结果比让步慢？CPU 执行太快，还没打印出来就开始让步了。

### 19. 线程状态还是斗地主吧

线程生命周期（线程状态）：6 种

1. NEW 新建 ：`new Thread(...);`
2. RUNNABLE 可运行：`.start();`
3. BLOCKED 阻塞
4. WAITING 等待
5. TIMED WAITING 计时等待
6. TERMINATED 终止

Java 核心技术中有一张图：

![线程状态](F:\笔记\Frank\My笔记（看完Frank的课后）\Java进阶\线程状态.png)

可以用斗地主来理解。斗地主就是这么实现的。★

### 20. 发现实际问题，抛出线程通信的含义

Windows 系统上有优先级，Unix 系统上所有的线程都是相同的优先级。★

斗地主不能用线程调度，因为取决于操作系统太扯淡了，用线程通信。我出完牌了要通知另外两个人。

京东会员抢东西抢的快可以用线程调度，给它高一点的优先级。线程通信就是绝对的公平，每个人都有每个人的权利。

### 21. 线程的通信 wait 和 notify

线程通信——等待唤醒机制（生产者和消费者买套）。

### 22. notifyAll

如果有多个生产者，唤醒所有的生产者。

### 23. 提及 Process 进程和点到为止章节结束语

ProcessBuilder 和 Process 类是操作进程的。

有兴趣的话就看看文档吧，了解一下。它是属于后面的东西了，它太复杂了。

Java 对并发的操作（死锁等...）不是太那个，如果你们知道 Go 和 C++ 的话，尤其是 Go，它的并发太牛逼了，它的通信不是简单的 wait 和 notify ，有 channel 。

真正大公司的并发有的不是用 Java ，用 Go 。

并发对实习生而言不是一个明显的优势，实习生基础掌握得好，算法掌握得牢，就能进厂。

后面一些东西，比如说任务，就不是 Java 语言的问题了，可能会用到框架，大公司可能会自己写一套。

上述视频的代码可能是有问题的，可能会有安全问题等 ...，因为要全部的考虑到要涉及太多的知识，不助于让你们简单的了解到多线程。★

并发是一个难啃的骨头，实习生可以到此为止，先学完 Web，框架再说，不要把时间浪费在没用的东西上。

## 8. Java collections framework

### 0. 原生数组带来的问题

好的程序员跟 IDE 是没有关系的，不建议花时间去折腾 IDE。企业里大部分还是用的 IDEA。

为什么没有在多线程里面使用 JUnit，因为 main 函数是一个主线程，所以不得不使用 main。使用 JUnit 的好处多多。

如果使用传统的数组，那么会遇到扩容的问题，万一元素溢出，则会下标越界。使用原生的数组，来进行扩容，比如说当下标大于等于数组长度之后，将数组长度扩大为原来的两倍，new 一个新的数组，再将原来的元素放进去。这就要涉及到数据结构和性能的问题。数据结构这门课本身是最难的。于是 Java 就出了一个比较友好的东西—— Java Collections Framework（Java 集合框架）。

### 1. 家族

在 Java 语言中，数组显得没那么实用，除非你要编写底层的一些东西，需要你用原生的数组，手写算法。

在应用层，Java Collections Framework 就要实用得多了。

集合是一个大家族，有类和接口。基本的用类，高级一点的用接口。

整个家族最重要的就是 List ，它来代替我们之前的原生数组。★

Map 是另一个家族。

![Java Collection](F:\Note\Frank\My笔记（看完Frank的付费课后）\Java进阶\Java Collection.png)

![Java Map](F:\Note\Frank\My笔记（看完Frank的付费课后）\Java进阶\Java Map.png)

### 2. 黑帮帮规

因为家族本身比较复杂，从哪里下手就很重要了，下错了就很不好。我们从 Collection 开始，Iterable 先不管，自己去查，看不懂就算了。

要深度了解这两个家族是比较复杂的。

Java 集合框架家族就相当于黑帮，Iterable 是贵人，但家族本身与它并没有关系，只是有这样一个人，在家族最困难的时候给予了帮助，对家族很重要。Collection 是老大，它要制定一套帮规，即 Collection 接口中的方法。它下面的家族，不管分成了几个，都要遵守，都要重写它的方法。

List 是最重要的，先把 List 学会。

### 3. ArrayList 第一讲

找手下办事，首先先找 List 。

ArrayList 重要掌握。

不做泛型限定的这种创建 ArrayList 的方式是不安全的，不推荐使用：★

```java
// 没有泛型限定的 ArrayList ，可以添加任何类型的元素。但是不安全，不推荐使用。
ArrayList arrayList = new ArrayList();

arrayList.add("Fuck");
arrayList.add('c');
arrayList.add(123);

// 泛型限定，只能添加指定类型的元素，甚至是对象。（这里是 String）
ArrayList<String> arrayList = new ArrayList<>();

arrayList.add("Cao");
arrayList.add("Oh");
arrayList.add("my");
```

### 4. ArrayList 第二讲

ArrayList 的类型不能为原生类型，只能为装箱后的类型。★

ArrayList 的使用下标版本的 add 方法，只能往已经存在了的元素的前面或者最后一个元素的后*一个*位置插入，否则下标越界异常，并且将该下标位置的先前已经存在的元素及其后面的元素依次往后移动。

练习非常重要。★

遍历的作用不止是输出，如果只是输出可以直接输出。遍历还可以对每一个元素进行一些操作，比如每一个元素加一。

### 5. ArrayList 第三讲

JDK8 的新特性不属于进阶的范围，要讲的话需要单独开一门课，叫 Java 新特性。要想学这部分的内容，需要先把进阶部分学完，包括*设计模式*。★

ArrayList 可以插入 null ，当 ArrayList 中只存在 null 时，调用 isEmpty() 方法，返回 false；当 ArraylList 中什么也不插入时，isEmpty() 方法返回 true 。★

`remove()`方法的参数有两种：一种是传入下标的；另一种是传入对象的。如果 ArrayList 的泛型为整型（`ArrayList<Integer>`），并且其中的元素有与要删除的元素下标重合的，那么使用的`remove()`方法默认是传入索引的那种。★

`removeRange()`这个方法不能用，因为是 protected 的，只能在同一个包中才能用。★

这些方法的结果是什么，别猜，上手实践。★

在没有 lambda 表达式的时候，是使用 `Collections.sort()`方法排序的。现在可以使用 ArrayList 的`sort()`方法，它是自己指定一种排序的方式，需要用到 lambda 表达式。★

Collections 类里面有各种各样的方法，可以去研究一下。

`subList()`方法左闭右开，数学上来说，即，[x, y) 。（与 C++ 保持一致）

### 6. Linked 链表

为什么要花 1 个小时来讲 ArrayList ？因为在应用层的实用性它比家族其它的高很多。（而很少有人用 Java 去开发底层）★

LinkedList（链表），一般文件系统用的是它（那是属于底层）。

Java 作者说：“ 要 List 用 ArrayList，要 Queue 用 ArraylDeque 。Java 不会底层到要经常用 LinkedList，我也不知道当初脑子进啥水了写了个这个东西出来。”

学会 ArrayList 基本上这块入门就够了。★

用面向对象的语言去学数据结构，你会有更清晰的认识。

ArrayList 查询非常快，但是插入和删除很慢，特别是数据量极大的时候。因为它在中间删除或添加一个元素，在它后面的元素都要移动。而为了解决插入和删除慢的问题，就有了链表。

### 7. LinkedList 一带而过

链表中的每一个元素都以引用的方式来记住它前面或者后面的元素，这样来表示它们的位置就非常方便；而 ArrayList 就不一样了。比作老师记每个同学的排名，他不可能记得住 ArrayList 中的位置，但链表就很方便。对于第二名，他肯定能记住第一名和第三名，这两个人是他要注意的。

LinkedList 是双向链表。

要使用它的话，熟悉它的方法就行了。

了解一下就行了，最好去练习。

这跟 ArrayList 其实是相似的，没啥好讲的。无非是你数据结构学的如何，如果学的好，对它们的理解就有所不同；没学过也没关系，一个 ArrayList 就够你玩儿了，它也是最实用的。

Vector 和 Stack，或者 ArrayDeque 就更不用介绍了，更少用到，除非是在底层上。

### 8. 提醒

很多教程都忽略了 Iterable，这个贵人。以后发财了，别忘了贵人，别忘了 Frank 。所以说人要懂得感恩。

ArrayList 是最常用的，但并不是随便什么都能用，还是需要结合实际情况。★

面试的时候他可能会问你一些数据结构，List ，LinkedList 等，都需要去看一看。★

不可能每个类每个方法都教，那简直是扯淡，我已经教你们怎么看了，教了你们方法。

新特性比较复杂，前提先得把基础学会，然后在单独去学习新特性。你基础都不会搞那些花里胡哨的干啥。所以一定要衡量它们的意义。★

List 下面的实现类可以去看看，非常有用，**尤其是 Stack** 。这些都去看看，有好处，虽然开发的时候不一定能用到，但是面试的时候可能会问你。★

### 9. Iterator 迭代器初试

这个美式的发音就像嘴里有水一样。

Iterator 遍历只对 Collection 家族有效。

**迭代器的优点**：简化了普通的 for 循环。普通的 for 循环要根据不同的数据结构写不同的代码（如：ArrayList 和 LinkedList（其中 LinkedList 可能还需要用到指针，但是非常不幸的是，Java 中没有指针。★）），而使用迭代器就可以直接使用，不存在这样的问题。增加了代码的可移植性。★

实际上 Iterator 在 Collection 家族中都能用。

### 10. fori 增强 for 迭代器区别和注意事项

#### fori 循环：

能读，能修改。

---

#### 增强 for ：

只能读，不能修改，当然也不能删除：（对象除外，如果自定义一个对象，如：Student 类，写一个`setName()`方法，就可以修改★）

经自己尝试，增加元素也不行，但是可以修改。因为`ArrayList.set()`方法是使用索引，而不是使用对象来操作。★

自我理解：如果使用对象来操作，相当于一边使用该对象进行遍历，一边使用该对象来进行集合的操作，显然线程不安全，可能会产生空指针异常。★

```java
// 该举动会报 ConcurrentModificationException 错误。
foreach(String value : arrayList) {
	arrayList.remove(value);
}
```

---

#### 迭代器：

也不能删除，会与增强 for 报同样的错误：（ 好在 Iterator 给我们提供了一个 remove() 方法 ）

```java
// ConcurrentModificationException
Iterator<String> iter = arrayList.iterator();
while (iter.hasNext()) {
	String value = iter.next();
	arrayList.remove(value);
}

// 使用 Iterator 的 remove() 方法
Iterator<String> iter = arrayList.iterator();
while (iter.hasNext()) {
	String value = iter.next();
	iter.remove();
}
```

---

#### 增强 for 和迭代器不能删除元素的原因：

就比如说两个孩子在手拉着手唱歌呢，你突然 biaji ，把他抓走了，那他的手就不知道抓哪了，就完了。你不能用正在操作的这个集合去删除元素。★

---

在迭代器中使用`arrayList.remove()`方法是绝对不允许的，尤其是**增强 for**，在阿里的开发手册中貌似有提及。★

在增强 for 中使用 remove() 是绝对不允许的。

在迭代器中使用`arrayList.remove()`就相当于：好几个小朋友手拉着手，你突然把其中一个干掉了，他两边的人都不知道自己旁边的人是谁了；而使用`Iterator.remove()`就相当于老师告诉了他小朋友，他去补作业了，上次的作业没写完，你俩手拉手。

于是，使用迭代器的 remove() 方法之后，剩下的元素会自动往前移（ Iterator 的操作对象是 ArrayList；若为 LinkedList 则自动建立连接。即相当于不在 foreach 中使用`arrayList.remove()`或`linkedList.remove()` ）。★

#### 不要在 for 语句中嵌套迭代器：

```java
/**
 *  产生 NoSuchElementException 异常，因为使用了多次 next() 方法，如：iterator1 就使用了两次。这样会导致迭代器过度后移，可能 
 *  会超出集合的容量范围，产生空指针异常。所以为了杜绝这样的事情发生，就不允许这样操作，就有了 NoSuchElementException 。
 */
for (Iterator<Integer> iterator1 = linkedList.iterator(); iterator1.hasNext();) {
	for (Iterator<Integer> iterator2 = linkedList_2.iterator(); iterator2.hasNext();) {
		if (iterator1.next() < iterator2.next()) {
			System.out.println(iterator1.next());
		}
	}
}
```

#### 替代方案：（自我感觉还是 fori 比较合适★）

```java
// 使用增强 for
for (Integer value1 : linkedList) {
	for (Integer value2 : linkedList_2) {
		if(value1 < value2) {
			System.out.println(value1);
		}
	}
}
```

---

增器 for 循环本质上也是一种小型的迭代器，只不过它是隐性的迭代器。增强 for 循环在创建的时候就已经创建了一个迭代器，只是是隐式的，你看不到，于是操作就没有那么自由了，你只能读取，不能修改。

### 11. 谈谈三者性能

如果必须修改集合的话不建议使用投机取巧的方法（对象引用），直接使用迭代器。（也可以使用 lambda 表达式）

#### 性能：（这里使用时间复杂度来表示）

需要分情况：

如果是数组的话，它是连续分配数据存储块，称之为可随机访问，这样的就快，时间复杂度为 O(1) ；而链表则不是连续分配数据存储块，就不能随机访问，所以要访问只能遍历，挨个去找需要的索引，时间复杂度最坏为 O(n) 。

对于没有随机访问的数据结构（如：LinkedList ）使用 Iterator 和 foreach ，明显比 fori 快；如果能够随机访问（如：ArrayList ），三者性能变化不大，（除非你对底层算法结构进行了改变，但这种特殊情况我们一般不考虑。对于一般的取元素这种情况，三者是一样的）。★

### 12. Set 和 HashSet

队列就不用讲，如果你熟悉数据结构的话可以去看看。

Set 里面最常用的就是 HashSet，跟 ArrayList 是一个级别的。★

#### Set 与 List 的区别：

它们就相当于射雕英雄传丐帮中的净衣派和污衣派。

Set 集合中的元素没有顺序。比如说：输出 ArrayList 中的元素，就会按照添加的顺序输出；而 Set 是无序的，而且它里面的元素不会重复。★

---

Set 中较为常见的就是 HashSet 和 LinkedHashSet，其中最为常见的是 HashSet，跟 ArrayList 一个级别的。TreeSet 先不说，与数据结构相关，有兴趣可以去看看。★

Set 接口有很多实现类，自己去研究。老师领进门。

HashSet 中如果插入两个相同的元素，则输出只会输出一次。★

在 JDK1.8 之前，Hash 值是使用数组和链表来完成的；1.8 之后，多了一个红黑树，对 HashSet 有一个优化。

Java 存储对象的时候也是用的 Hash 码。

如果不能理解为什么它不能够重复，就不理解，因为与数据结构有关，你要去了解它的底层，要学很多东西。★

### 13. LinkedHashSet

为什么 HashSet 可以不重复，因为每个对象都有一个 Hash Code。就相当于每个元素的值是一个身份证号，添加的时候会检测这个身份证号是否已经存在，若存在，则不会再添加。★

如果你添加了两次，本质上只添加了一次，也不会覆盖，编译器也不会报错。

如果想让它有顺序，使用 LinkedHashSet ，但它也是去重的，Set 永远是去重的。★

还有一些其他的有意思的 Set，你们自己去看一看。

### 14. Map 和 HashMap 以及 Entry

没讲的你们自己去研究。

Map 很多，最常见的也就几个。一个 HashMap，一个 LinkedHashMap 。其他的还真不常用。★

迭代器现在就不能用了，上次说了它是基于 Collection 的。★

有些方法必须要新特性才能学，先学会基础。

`entrySet()`方法可以直接使用 Set 来接，也可以写标准一点，使用`Set<Entry<K, V>>`。Entry 还没学，当扩展：

```java
// 直接使用 Set
Set entry = hashMap.entrySet();

// 使用 Set<Entry<K, V>>
Set<Entry<Integer, String>> entry = hashMap.entrySet();
```

### 15. Map 注意点

如果前面 HashMap 已经添加了这个元素，我再使用 put 方法来添加它，即 Key 与前面相同，换一个 Value 值，这样 IDE 会直接报错，如果运行的话就把原来那个元素覆盖了，但这样做是有危险的，编译器会提示：★

```java
HashMap<Integer, String> hashMap = new HashMap<>();
hashMap.put(0, "Tom");
hashMap.put(1, "Jerry");
hashMap.put(2, "Foo");

// 再次添加 1 号元素。
hashMap.put(1, "Jack");
// 编译器报错，强制运行输出结果是把 "Jerry" 替换成了 "Jack"。但是这样做很危险，编译器会提示。★
```

所以千万不要替换 Key 时直接把它顶掉，请使用`replace()`方法，不要胡搞、瞎搞。★

如果使用`get()`方法去返回一个 HashMap 中没有的元素，它会返回 null ，很有意思。★

### 16. Entry 与 Map 转换 Set 之后遍历

Entry 也是一个类型，专门来存键值对的。★

为什么要把 Map 转换为 Set ？因为要遍历啊，使用高级 for 循环，迭代器。只有转换成 Collection 才能使用迭代器呀。★

比如说要留下本次考 90 分以上的人的学号与分数，就需要转换成 Set 然后迭代。甚至还可以排序。

可以进行各种各样的骚操作，你们自己去想。

### 17. 提及 LinkedHashMap 以及课后作业

既然是泛型，那么就可以使用自己定义的类型，比如说 Student ，你们下来自己去练习，课后作业。你们可以去写一个学生管理系统。到了这个程度，对你们而言，写学生管理系统，简直是太简单了，就写个简单的 CRUD，增删改查吧，我实在想不出比这更简单的了。讲到这课了可以停下来练练手。★

LinkedHashMap 就相当于一个有序的 HashMap （即按照插入元素的顺序），就不用我解释了。

课后作业，写一个增删改查的学生管理系统。★

### 18. 集合框架结束语

不常用的类都没讲，比如说底层的一些东西。很少有人会用 Java 去开发底层。

如果你对队列这些感兴趣建议自己去看。

现在你可以自己去试试跟着文档去学学其他的类了，看看有什么区别，然后总结一下。★

Properties 是后面学框架可能会用到的，它跟 Map 基本上差不多的。读取文件，读取一个配置文件。★

它们有很小的差异，你要注意的是它们的优缺点，和它们的用途，它的数据结构，底层原理是怎样实现的。这些方法你有没有掌握，有没有练习，有没有读懂。哪怕以后忘了，也没关系，但是你用过，有个印象。非常重要。 ★

还有就是你有没有总结笔记。★

把图上的搞懂，你的集合框架就学的很不错了。★

JDK 8 新特性 lambda 表达式， Java Web 都用不到，除非你们学到框架之后，能够用到它。★

新特性题一下，包括设计模式。

有兴趣的可以把没讲的看一下，没兴趣的把课后作业完成就行了。代码能跑起来就 OK 。

有兴趣的可以花一个星期，或者两三天，一天用余下的 1 小时时间，一天学一个，一星期肯定能把剩下的类学完。

Java 网络部分基本上不是太多，网络的东西基本上了解一下就 OK 。

## 9. JDBC

### 0. 说明

装上 MySQL 5.7.29 ，版本一样，否则报错与我无关。★

学完 Java SE 基础部分，学校可能要求写一个学生（图书）管理系统。因为数据是存储在内存中的，所以关机就没了，于是有的学校出了一个加分项，将数据放在文件里。但是，这两种都是愚蠢的行为。★

重要的用户的 持久型 数据，肯定要放到数据库里。★

这章我们使用 Java 来操作数据库。

为什么会出这章？除了能装逼，最重要的是打老师的脸，这是我最想看到的。——Frank

这部分是以 MySQL 为基础的。

### 1. JDBC 由来和定义

各大数据库公司要求 Java Sun 公司开发一套规范，即一套 API、接口，把它拿到所有的数据库都适用，然后各大数据库公司再去实现它就行了，因为你不能让 Adidas 去造布料吧。于是就产生了 JDBC 。★

JDBC 就是布料和棉花，拿到 Nike 公司，让他自己去造鞋；拿到 Adidas，让他自己去生产衣服。★

JDBC 是面向 关系型数据库 的，即不支持 MongoDB、Redis 。★

驱动程序，即驱动底层的程序，一开始的时候不是由 Java 实现的，而是由 C/C++ 实现的。因为性能的原因，这些中间层都是由 C/C++ 编写。随着优化编译器，即 Java 字节码，转换成高效的特定机器码，有这种技术之后，才使 Java 在中间层开发的优势显示出来。随后 JDBC 才会被重视。

JDBC 不是那么好理解的，因为它有一些步骤，需要知道。所以训练的时候多写一遍。★

### 2. JDBC 体验

#### MySQL 的连接 jar 包下载：

虽然 javax.sql 包中写好了驱动，但是要连接 MySQL ，需要下一个 MySQL 的连接 jar 包：

去 maven 库中搜 MySQL Connector/J ，我们追求稳定，下载使用人数最多的——5.1.6 ，有时候版本太新不是好事，使用最新的还有一个依赖。★

JDBC 相当于染布坊，这个 jar 包就相当于物流、货车，把人家造好的布料拉到厂家去生产产品。

#### 使用 JDBC 第一步，加载驱动程序：

这步就相当于打电话，Nike、Adidas 这些厂商要订购原料，肯定要先打电话告诉原料生产商自己是谁、是哪个厂的呀：★

```java
// 加载 MySQL 的驱动程序 -> 给布料厂商打电话，我缺布料，你得给我送来，我是 mysql 公司的。
Class.forName("com.mysql.jdbc.Driver");
```

#### 第二步，获得数据库的连接：

打完电话过后，布料厂的快递员需要知道路线，从哪个厂到哪个厂，于是总部（DriverManager）接到电话过后，告诉下属谁打了电话，地址在哪，然后返回一条路线（一个连接，即 Connection ）：

```java
// 函数格式
DiverManager.getConnection(url, user, password);


// 于是我们需要先定义三个常量

// 最后那个 student 是表名
public static final String URL = "jdbc:mysql://localhost:3306/student";
// MySQL 中我们使用的用户名和密码
public static final String USER = "root";
public static final String PASSWORD = "123456";

// 返回准确路线、导航 -> 告诉送货员，具体走什么路线才能送货
Connection connection = DriverManager.getConnection(URL, USER, PASSWORD);
```

#### 第三步，获取数据库操作对象：

创建订单完毕`connection.createStatement();`，卸货（statement），返回一个货物：

```java
// 返回一个货物 -> 送货送到了，然后卸货
Statement statement = connection.createStatement();
```

#### 第四步，打开 Navicat ，连接数据库：

连接名随便写，这里写 local -> 密码写自己设的密码 -> 测试连接 -> 点击 确定。

右击 连接名 -> 新建数据库 -> 数据库名为 Java 中指定的 -> 字符集 utf8mb4 （mb4 指支持表情包）-> 排序规则 不选，默认就行 -> 确定。

创建一张表 info ，三个字段：

```mysql
id bigint(30) unsigned auto_increment primary key not null;
name varchar(50) not null;
age tinyint unsigned not null;
```

#### 第五步，使用查询语句：

```java
// 语法
statement.executeQuery("SELECT * FROM MYTABLE");

// 举例
// 这个 ResultSet 里面封装了一个 cursor，正好有 next() 方法，就相当于迭代器。
ResultSet resultSet = statement.executeQuery("SELECT * FROM info");

while (resultSet.next()) {
    // id 在数据库中我们定义的是 bigint unsigned 类型，转换成 Java 的类型，就是 int ；getInt() 方法中的数字表示在数据库中的该表中（这里是 info 表）定义的字段的编号，从上往下，第一个的编号是 1 ，依次递增。
    int id = resultSet.getInt(1);
    String name = resultSet.getString(2);
    int age = resultSet.getInt(3);
    System.out.println("id: " + id + ", name: " + name + ", age: " + age);
}
```

#### 第六步，关闭仓库、关闭连接：

```java
statement.close();
connection.close();
```

这样就能查出来了，但并不完善。下面我们介绍完善的，先练习一下、理解一下。★

### 3. 整理和释放

上节课的代码是不规范的，是有问题的。★

很多同学跟我说框架、模板，但 JDBC 必须要手敲，你务必要会手写，非常重要，否则以后你遇到问题都不知道问题在哪。★

更完善的写法：

```java
public class JDBCStart() {
   	// 配置文件
	public static final String URL = "jdbc:mysql://localhost:3306/jdbc_start";
	public static final String USER = "root";
	public static final String PASSWORD = "123456";
	public static final String DRIVER = "com.mysql.jdbc.Driver";
	
	public static Connection connection;
	public static Statement statement;
	public static ResultSet res;
	
	public static void main(String[] args) {
		try {
			// 1. 加载驱动
			Class.forName(DRIVER);
			
			// 2. 获得数据库连接对象
			connection = DriverManager.getConnection(URL, USER, PASSWORD);
			
			// 3. 获取数据库的操作对象
			statement = connection.createStatement();
			
			res = statement.executeQuery("SELECT * FROM info");
			
			while (res.next()) {
                  // 里面的参数表示 第几列 的字段 ★
				int id = res.getInt(1);
				String name = res.getString(2);
				int age = res.getInt(3);
				
				System.out.println("id: " + id + ", name: " + name + ", age: " + age);
			}
		} catch (Exception e) {
            e.printStackTrace();
        } finally {
        	try {
				res.close();
				statement.close();
				connection.close();
        	} catch(SQLException e) {
        		e.printStackTrace();
        	}
        }
	}
}
```

不要把包导错了，Connection 和 Statement 都是导的 java.sql 包中的。★

`Class.forName()`应该直接使用 try/catch 包裹起来，因为如果 SQL 出错了，应该停止执行。★

这样才是一个完美的程序，要有资源的关闭。释放资源时先开启的后释放，就跟栈一样。★

### 4. 封装 JDBCUtils

#### 提出问题：

把前面的程序放在一个`selectAll()`方法中，那么只需在 main 方法中调用它，即可查询全部。★

如果再写一个函数`selectById(int id)`，那么在这个函数中还要把 连接数据库那 4 个步骤再写一遍，这是非常愚蠢的行为。如果换一个类，也要再写一遍最前面的 配置文件，那太蠢了。有更好的方法帮我们解决这个问题。★

#### 解决问题：

我们创建一个 folder，在 IDEA 中可以直接使用 点 的形式（com.google.util），而 VS Code 中需要使用 斜杠 的形式（com/google/util）。然后在里面创建一个 JDBCUtils.java 类，把它当作工具类去使用，把它抽离出来。★

#### 创建配置文件：

这里引入配置文件的概念：我们不应该将 配置 以字符串的形式来写，我们不可能让用户去编译这个程序，所以我们应该将它单独写在一个文件里，即配置文件。然后让它去读取文件：

在 src 目录下新建一个 db.properties 这样一个文件，将前面代码中的 配置文件 部分拿过来：**一定要在 src 目录下创建，否则会找不到该文件导致 InputStream 空指针异常。★**

#### 配置文件的路径问题：

经过自己尝试，配置文件也能放在其他地方，但是要将文件 完整的路径 传给类加载函数。路径 是从 src 目录开始的。如：如果我将 db.properties 放在 src 下的 com.google.jdbc_test 包中，那么该文件的 绝对路径 为：src/com/google/jdbc_test/db.properties，相对路径  为：./com/google/jdbc_test/db.properties 。★

```
url=jdbc:mysql://localhost:3306/jdbc_start
user=root
password=123456
driver=com.mysql.jdbc.Driver
```

#### 使用配置文件：

在 JDBCUtils.java 中：

```java
public class JDBCUtils {
	private static String url;
	private static String user;
	private static String password;
	private static String driver;
	
	// 通过静态代码块，来预先执行读取配置文件的配置项，做预处理。
	static {
		try {
			// 这句写不写都行，因为有一种更简便的写法。★
			// JDBCUtils.class.getClassLoader();
			
			// 更简便的写法，在 Java Web 中不能这么写。★
			InputStream inputStream = ClassLoader.getSystemResourceAsStream("db.properties");
			
			Properties properties = new Properties();
			properties.load(inputStream);
			
			url = properties.getProperty("url");
			user = properties.getProperty("user");
			password = properties.getProperty("password");
			driver = properties.getProperty("driver");
			
			// 这样就获取到他们的值了，可以用输出来看看。
			System.out.println("url: " + url + ", user: " + user + ", password: " + password + ", driver: " + driver);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
	
	// 写一个函数来调用，方便在其他类中调用该类来测试。
	public static void test() {
		System.out.println("使用！");
	}
    
    // 写一个单例
    public static Connection getConnection() throws SQLException {
    	return DriverManager.getConnection(url, user, password);
    }
    
    // 关闭资源，需要重载，因为如果不是查询语句的话可能就没有那个 ResultSet 。★
    public static void close(Connection connection, Statement statement) throws SQLException {
    	if (statement != null) {
    		statement.close();
    		
    		// 关闭之后可以把它清零，也可以不写，无所谓。★
    		// statement = null;
    	}
    	if (connection != null) {
    		connection.close();
    	}
    }
    
    // 重载 
    public static void close(Connection connection, Statement statement, ResultSet resultSet) throws SQLException {
    	if (statement != null) {
    		statement.close();
    		
    		// 关闭之后可以把它清零，也可以不写，无所谓。★
    		// statement = null;
    	}
    	if (connection != null) {
    		connection.close();
    	}
    	if (resultSet != null) {
    		resultSet.close();
    	}
    }
}
```

点开 Properties ，你会发现它跟 Map 很像，实际上它就是一个 Map 。可以这么理解。

### 5. 增删改 executeUpdate()

`executeQuery()`只能用于查询。

进行 增删改 操作并测试 我们的 JDBCUtils 类：

```java
public class JDBCTest() {
    public Connection connection;
    public Statement statement;
    
	@Test
    public void insertTest() {
        try {
            connection = JDBCUtils.getConnection();
            statement = connection.createStatement();
            
            // 测试一下获取到 connection 没有
            // System.out.println(connection);
            
            String sql = "INSERT INTO info(name, age) values('qq',16)";
            
            // 增删改都使用该语句，返回值为 int，意为 改变了几行 ★
            int res = statement.executeUpdate(sql);
            
            if (res > 0) {
                System.out.println("Insert success! ");
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                JDBCUtils.close(connection, statement);
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

删 和 改 操作同理。

### 6. 字符编码问题（装 X 需谨慎）

有同学说不能插入中文，乱码；包括查询，在 Navicat 中添加一条中文数据，IDEA 中查出来会乱码，字符编码有问题。

解决办法：在 db.properties 文件中第一句话后面添加`?characterEncoding=utf8`：

```
url=jdbc:mysql://localhost:3306/jdbc_start?characterEncoding=utf8
user=root
...
```

此时发现 VS Code 中查询还是不行，但是插入可以了，因为 终端 是 gbk 编码。

此时将 Win 10 的编码改为 utf8，然后重启。

还要在 终端 中将 MySQL 的一些东西改成 utf8：

```cmd
# 终端中连接 MySQL 后
show variables like "%char%";

# 将 charcter_set_database 和 charcter_set_server 都改为 utf8
set charcter_set_database=utf8;
set charcter_set_server=utf8;
```

将 jdbc_start 数据库删除，重新创建。

使用 VS Code Java 的插件 (Java Process Console) 终端来输出时，结果是有问题的，乱码，即使把所有的编码都改为了 utf8，它自己编译的时候也是说的 utf8 ，但是就是乱码。所以使用 VS Code 装逼，需谨慎。插件慎用。★

插件本来就是不完善的。

IDEA 上应该不会出现这种问题。

Windows 上没办法，很蛋疼，一定要注意字符编码的问题。★

经自己尝试，和 Frank 的提示，在 IDEA 上，按照上述方法改完字符编码后，注意将所有客户端的编码保持一致，然后重新创建一个类重新写代码查询，即可正常显示。★

### 7. PreparedStatement 和问号占位

获取 statement 对象还有一种更先进的方式。万一需要 用户输入 呢：

```java
connection = JDBCUtils.getConnection();

// 用户输入
// 在 preparedStatement = connection.preparedStatement(); 语句前面添加
System.out.println("请先输入姓名，然后输入年龄，用回车隔开：");

Scanner scanner = new Scanner(System.in);
String name = scanner.nextLine();
int age = scanner.nextInt();

// sql 语句使用上面输入的 name 和 age 
// 使用 ? 来接
String sql = "INSERT INTO info(`name`,age) values(?,?)";

// 此时就不能使用 Statement 类了，Java 中提供了一个更屌的东西 PreparedStatement 。
preparedStatement = connection.preparedStatement(sql);
// 这里的第一个参数表示 第一个占位符 ，即上面 sql 语句 values 中的第一个 ? ★
preparedStatement.setString(1, name);
preparedStatement.setInt(2, age);

int affectedRows = preparedStatement.executeUpdate();
```

以后我们都不用 Statement 了，都用 PreparedStatement 。因为它是 防注入 的。这是一种比较高级的手法，推荐使用。★

scanner 也要关闭。

查询就直接把`executeUpdate()`改为`executeQuery()`，其他的改改，就不用我说了。

### 8-1. 最终 Demo 说明

下节课整治一下学生管理系统。脑子清醒再去看。需要大概 3 个小时。

### 8-2. 对象封装，重构代码，学生管理系统模块化编程

select all 希望返回的学生信息是 ArrayList ，需要封装一下。

Student 类中的数据类型要跟数据库对应，不要瞎搞。

select all 把查出来的每一行的数据都 new 一个 Student，然后将它放进 ArrayList 中。还可以把这些代码专门封装到查询函数中，返回 ArrayList 。

selectById 返回一个 Student 。

delete 返回 布尔 。

update 可以重载。改函数名。

新建一个 包 ：com.google.service，新建一个类 StudentService.java ，将所有的方法 粘贴 到这；建一个 com.google.model，将 Student 类放进去；建一个 com.google.main ，创建 RunApplication.java ，里面写 main 方法`functionService()`和`init()`方法，`init()`中输出一些初始化的东西，`functionService()`中调用一些方法，然后`init()`调用`functionService()`， main 中调用`init()`。

JDBC 还有一个东西，分页，这里用不到，Java Web 可能会用到。数据很多，sql 语句中使用 limit 限制，一次查 10 个。★

不要每次都 new 一个 Scanner ，那太蠢了，小伙子。

这种分层就叫做模块化，MVC 分层，设计模式。

## 10. Java 人脸识别认证

### 0. 说明

前提是进阶看完，否则一脸懵。

### 1. 提出问题，引入SDK概念

这个和语言没关系。

学生要做这种东西太难了。大公司有 人脸识别 的东西，我们什么都不会，但可以买。但这节课讲的东西是不花钱的。

通常情况下，我们要买大公司的一些服务，一些功能。如果我们买了，他们会给我们 SDK （软件开发工具包），即大公司底层的程序员，给上层应用层程序员提供的开发工具包，说白了就是给小白用的，给我们用的。我们买了，他们会把 SDK 和其 文档 等套餐给我们，我们用就行了。

我们引入他们的包就 OK 了，无需关心人工智能，图像是怎么识别的，人脸是怎么识别的。我们关心的是找一个合适的 SDK ，而且是免费的。

这就是 SDK ，明白它怎么来的，怎么用就行。

### 2. 选择平台

找了很久，只有 虹软 的是免费的，不容易。它是美国硅谷的一家大公司，很权威，文档也很全。最重要的是免费。

### 3. SDK下载和文档说明

直接搜 虹软，进入公司的官网。

右上方 虹软技术 -> 选择 人脸识别 ，可以看一下，关注一下。

右上方 开放平台 -> 人脸识别 SDK ，使用最新的。需要注册和身份验证，这是一个国际大公司，安全性肯定没问题的 -> 点击 免费获取 -> 选择平台，如果是毕业设计，就可以选 Linux，这里选择 Windows x64 。-> 创建 一个 应用，人证对比，互联网金融。-> 下载 SDK

帮助中心 -> 可以看看 API 文档，这一块要了解一下，比如说人脸识别是怎么回事儿。★

这个东西学生用足够了，完全够你毕业设计，或者期末什么的装逼。★

下载 SDK 后的文件夹解压缩出来有三个文件夹，**libs 下面有一个 jar 包，等会需要引入**。WIN64 下面是三个库，这些在文档中都有。

看文档看了半天还是不知道怎么用，接下来就告诉大家怎么用。

### 4. 人脸检测

随便找两张帅照，一定要是同一个人。

下载的 SDK 一定要改名，一定不能用他给的那个特别长的那个名。★

打开 IDEA -> import Project -> 选择刚刚下载的 SDK 的那个文件夹 -> 一路 Next -> Finish -> 创建一个 src 文件夹，右击， Make directory as -> Resouces root

在 src 中创建一个 Test 类，写主函数，将他给的案例代码 从官网获取 部分拷贝过来，然后将官网的 appId 和 sdkKey 拿过来，分别去掉前面的 APP ID: 和 SDK Key: 。

激活引擎 部分拿过来，将 libs 文件夹下的 WIN64 这个文件夹的路径拿过来放到`new FaceEngine()`中。

下面的东西一路拿过来，看懂就行，基本上不用我们写。一直到 激活引擎 那部分，运行，如果什么都不输出，就激活成功了。★

先把 人脸检测1 的路径换为自己找的图片的路径，然后从 设置活体测试 一直拷到 年龄检测 ，运行。输出的 性别，0 是男，1 是女，-1 是未知，文档中都有，直接在文档中搜索 gender ，往上翻一下，就能看到。

文档就足够了，如果你还觉得不行，看源码，源码是解决问题的关键，基本上你看完源码，你就知道是怎么用的了。★

这些功能都可以研究一下，不研究也无所谓，这些都无所谓。★

### 5. 人脸对比

我这里就不封装函数了，你们要封装一下。★

你要依葫芦画瓢，不过不懂也没关系。★

这块很简单，基本上就是复制粘贴，但要用得更好的话，必须要知道这些是怎么用的。看变量名基本上都能才出来它是干啥的，还可以点进去看看源码。最好的就是看文档。★

想用好这个东西，还是要看文档。

### 6. 建议和结束语

关于这个人脸识别，文档中的都可以去想，去尝试，这个没法教，因为各大学校做的案例都不一样。

怎么去用它们，就看你们自己了。关键是这个是免费的，非常良心。★

这个应用层的东西，可以去自己研究一下，创新一下。

有能力的同学还可以把它们封装成函数，再封装一层，是完全没有问题的。因为企业向他给的 案例代码 那样写，是绝对不允许的，从官网获取 的那部分就应该写成 配置文件。★

创建引擎 应该是一个单例。★

人脸检测 的前面那一块都不应该在 service 层出现，应该在 main 中写一个`init()`函数。★

下面那些 都可以挨个封装成函数。★

这个代码肯定是不专业的。

有能力封装一下，没能力这个代码也能用。从商业角度来说，只要你的产品做得好，没人管你代码写的多烂。★

这个代码仅供参考，有异议的话，文档、源码 什么都有，非常全，他们可能还提供技术支持，自己去问问。

## 结束语_Frank的话

看完这个视频，恭喜你们，走完了很多人没走完的路。

有很多东西没教，比如说：网络编程、TCP/UDP 编程，还有同学说 JDK 新特性。

以后可能还要接触更深层次的东西，比如说：反射、泛型、注解 和 更深层次的 JVM、并发 。

学到这，基本上能应付 Java Web 了。

得高分不重要，看重的是代码是否规范，给同学看的时候要写些注释，或者说是否要给他们写个文档。★

学习的过程总是不断在变化，在更新，哪里出错了，是好事儿，不是坏事儿。心态一定要好。报错有 bug 是好事儿，你要想着你以后去面试，去工作的时候，那 bug 更多。只有这样，你才能让自己的技术不断增长，才能屹立于这个社会的技术顶尖之上。★





















































































