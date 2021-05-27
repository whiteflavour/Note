# Java for the Real World

## 1. The Java Virtual Machine (JVM)

### 1. JVM Overview

#### Java 代码的翻译：

Java 代码先被 JVM 翻译，然后再给操作系统。

**好处：**跨平台。★

#### Java Version：

##### 长期维护版本 (LTS —— Long Term Supported)：企业使用的版本 ★★

Java 8, 11, 14 ... 

#### JVM Varieties: 

Oracle 有两种 JDK ：Oracle JDK (相当于商业版 —— 收费) 和 Open JDK (免费) 。

区别：Oracle JDK 有一些特殊的功能，供大公司的特殊用途。★

> 除了 Oracle ，还有一些其他公司的 JDK ，才入门大可不必担心到底用哪个，那是后话。★

### 2. JVM Versions

#### 特点：

向下兼容。

> 注：如果在新版本上编译 Java 文件，然后在旧版本上运行，会报错；但是在旧版本上编译的则可以在新版本上运行。★

所以一定要保证你的电脑上的 Java 版本要跟服务器上的一致，否则就可能报上述错误，很尴尬。★★

## 2. Build Tools

### 3. Building Java Applications

> jar File 是跨平台的。

**存在 Build Tools 的原因：**

使用`javac`命令来构建 太麻烦了，而且也不好跨平台。★

### 4. Ant

**优点：**

灵活。

---

Ant 没有管理依赖 (dependencies management) 的工具，所以需要用到 Ivy ，它可以集成到 Ant 中。★

### 5. Maven

应用很广泛。

### 6. Maven: Navigating a POM File

如果要迁移项目，如果新项目无法工作，那么需要将能够工作的项目的 POM.xml 的`<plugin>`部分复制过去，然后修改一下`<mainClass>`即可。

写代码的过程中遇到错误：

1. Google
2. StackOverflow

### 7. Maven Repositories

有些公司会有私有仓库。

也有不同于中央仓库的其他公开的仓库，如果要使用它们，你的 pom.xml 会配置得完全不同。★

### 8. Maven Summary

Ant: 灵活，但是配置繁琐。

Maven: 开箱即用，但不那么灵活。有时遇到错误，就是没有遵循 Maven 的规则。★

Gradle: 结合了上述两者的优点。

### 9. Gradle

配置文件：build.gradle

#### 关于 build.gradle: 

plugin: shadow ：相当于 Maven 中的 shade 插件，将项目打包为 jar 文件。★

## 3. Testing

### 10. Preparing the IScream Applicatiion for Testing

JUnit 是使用最广泛的测试库。★

### 11. JUnit

xUnit-style framework. 

NUnit, PHPUnit, CPPUnit ...... 跟这些类似。★

JUnit 可以自定义断言。★

**可以通过命令来执行测试：**

`gradle test` and `mvn test`

**缺点：**在控制台上不会显示错误信息。

#### 控制台下测试的错误信息：

1. 需要到 build 文件夹 -> test-results -> test -> binary -> 有个 XML 文件，打开它，即可看到错误信息。
2. build -> reports -> tests -> test -> 浏览器打开 index.xml ，这更好看。★

#### 使用断言：

需要导入 Assert 类的方法：

```java
// 导入 Assert 类的所有方法。★
import static org.junit.Assert.*;

public class UnitTestDemo {
    @Test
    public void addTest() {
        int num1 = 3;
        int num2 = 8;

        int sum = num1 + num2;

        assertEquals(11, sum);
    }
}
```

### 12. TestNG

xUnit-style framework. 

**与 JUnit 唯一的区别：**

断言方法中的参数顺序与 JUnit 相反：

TestNG：actual, expected

JUnit：expected, actual

**TestNG 的特色：**

它可以在一个单元测试中将 JSON 文件 List 中的多个数据同时测试，但是每个单独列出来。★

> 但是现在 JUnit 也可以了。★

### 13. Test Doubles Overview

#### Java has many test double frameworks: 

1. EasyMock：在老 Project 中可能会看到。
2. Mockito：最常用。★
3. PowerMock: 有除上述两者之外的更多功能。
4. ...

#### 优点：

帮助你在有很多依赖类的情况下不进行太多改动即可测试代码。如：若需要访问外部资源（一个网站、数据库。。。），但实际我们在测试的时候不想去真正访问它们，因为需要消耗一些时间，但是 Mock 可以帮助我们。

#### Creating a Mock: 

1. Create the mock object
2. Set expectations for the mock object
3. Inject the mock into the test object
4. Invoke the test object
5. Verify

通用的步骤是 1, 2 和 5，其他两步根据使用的测试框架不同而不同。★

### 14. EasyMock

断网也能用。

### 15. Mockito

在 Java 开发中比较常见，是 EasyMock 的一种分支，所以都差不多。

但是它比 EasyMock 简单，并且有更多特性。★

一般 Mockito 不会抛出 NullPointerException ，默认返回空字符串、空 List 等等。

### 16. PowerMock

在使用第三方库的时候有些不是 Static Method ，可能需要用到 PowerMock 来测试。

Spring Framework 就有一些 Mock 测试类，来方便单元测试，就不需要使用第三方库了。

## 4. Logging

