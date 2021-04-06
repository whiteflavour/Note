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

