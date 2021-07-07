# Spring 揭秘 (2021.5.12 - )

## 序：

**心法：**须知万物溯其源，学东西不是为了学而学，最初是有个场景、问题，然后就是解决方案的提出、选择、权衡、实施、反思和改进。

**对于 Java 学习和应用：**如能掌握精髓，自可海阔鱼跃天高鸟飞，只因心中已修得真经。若方法不当，无人指导作战思路和心得，纵使看了规范、API 和手册，也不解其意，只能硬头先抄，盼经年累月恍然自知，但效率太低。

## 第一章、Spring 框架的由来：

EJB 太笨重，所以就有了灵活的 Spring 。但具体使用什么还是需要根据需求来决定。

> 没有任何一种解决方案是普遍适用的，只有适合用于特定场景的解决方案，脱离具体场景来讨论任何解决方案都是脱体实际的表现。★

![Spring总体结构](F:\Note\IT\Programming Language\Java\Spring\From Book\Spring 揭秘\Pictures\Chapter1\Spring总体结构.png)

(https://blog.csdn.net/wangmaohong0717/article/details/53325104)

抓住了这副骨架，也就抓住了 Spring 框架的学习主线。

只要掌握了 Spring 的理念和方法，就能自己“造轮子“，在相应的应用场景中创造新的”Spring“。★

> Before the dream lifts you into the clouds, make sure look hard at the facts on the ground. ——(Donald J. Trump, How to Get Rich)

## 第二章、IoC 基本概念：

**IoC 理念：**与好莱坞原则：Don't call us, we will call you. 一致。

### 三种注入方式：——(Martin Fowler, Inversion of Control Containers and the Dependency Injection pattern)

1. 构造方法注入：对象被构造完成之后，马上就可以使用。
   （缺点：对象多的时候构造方法的参数列表唱，此时对相同类型的参数处理困难，不好维护和使用；并且 Java 中构造方法无法被继承，无法设置默认值；对非必须的依赖处理，要引入多个构造方法，参数数量上的变动也会不好维护。
2. setter 方法注入：可以在对象构造完成之后注入，使用于不着急使用的场景。
   （优点：除构造方法的缺点对应的部分外，还有良好的 IDE 支持。缺点：对象无法在构造完成之后立马进入就绪状态。）
3. 接口注入：必须实现某个接口，比较死板和烦琐。
   （不提倡使用，因为它强制对象实现不必要的接口，带有侵入性）

## 第四章、BeanFactory

BeanFactory 是最基本的容器，而 ApplicationContext 有更多的功能。

xml 文件的 XSD 格式是较于 DTD 之后出新的，推荐使用。★

### BeanFactory 的使用：

```java
DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(factory);
reader.loadBeanDefinitions(new FileSystemResource("beans.xml"));

factory.getBean("...");
```

### 对一个字符串注入 null：

使用`<null/>`。

### `<bean/>`配置的自动绑定：

**注：**★

1. 手工明确指定的绑定关系总会覆盖自动绑定的行为。
2. 自动绑定只适用于“原生类型、String 以及Classes类型以外“的对象类型，对这些类型及其它们的数组无法自动绑定。

建议手动绑定，因为有良好的 IDE 支持，通常不介意多敲那几个字符，并且有助于自己把握系统的行为。当然，任何事都不是绝对的，找到对于该场景合适的即可。

**技巧：**

可以在`<beans/>`标签中指定一些属性，它们会直接运用于所有的`<bean/>`。★

### 继承：

可以在`<bean/>`中指定 parent 属性，甚至还可以指定 abstract ，避免容器对其实例化，特别是 ApplicationContext 。

### scope 属性中的 singleton and prototype：

singleton 与单例设计模式不同：singleton 保证这种类型的 bean 在同一个容器中只存在一个共享实例；而 Singleton 设计模式则是保证在同一个 ClassLoader 中只存在一个这种类型的实例。