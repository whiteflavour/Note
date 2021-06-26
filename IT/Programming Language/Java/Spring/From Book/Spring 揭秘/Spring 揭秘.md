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