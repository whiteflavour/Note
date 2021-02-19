# Java笔记 —— 完成时间：2020.3

## 一丶代码规范，IDEA基本操作（快捷键）

### 1.Java注释规范（函数与类）-> Javadoc

```java
/**
*@author ...
*@version ...
*@since ...
*@param ...
*@return ...
*@...   ...
*/
```

**例如**

>

```java
/**
 * @author sheree
 * @version 1.0
 * @param number_a
 * @param number_b
 * @return 两个参数的和
 */
public static int sum(int number_a,int number_b)
{
    return number_a+number_b;
}
```

### 2.其他代码规范

**见《阿里Java开发手册》**

### 3.IDEA的一些常见快捷操作

## 二丶Java基础

### 1.研究String类 ★，正则表达式（重点）★ ->   JDK doc        菜鸟教程

**println函数输出对象为字符串 -> 默认调用toString函数**

## 三丶POP与OOP

### 1.POP：面向过程 -> 走一步看一步，没有目标，咸鱼

### 2.OOP：面向对象（目标） -> 有目标，过程不重要，大众化。-> 站在更高的层面看待事物

### 3.对象 -> 实例：对象的一种具体表示，生活中具体的一个例子，是唯一的

### 4.类中的变量和方法 -> 属性（特性 、共性）

## 四丶在注解中引入getter，setter

**导入Lombok包（插件）-> @getter，@setter**

需要查看 IDEA 官方的配置方法。★

## 五丶static （静态变量、方法）-> 与整个类有关，与每个对象（实例）无关，可直接用类名调用，而无需创建对象

## 六丶单例设计模式

```java
package com.coretechnology.demo;

public class Earth {
    private static Earth earth = new Earth();
    private Earth() {}
    public static Earth getEarthInstance() {
        return earth;
    }
    public void playing() {
        System.out.println("Hello");
    }
}
```

## 七丶抽象类和接口的区别 （重点！！-> 易被误导）✡

### 1.抽象类：对具体事物的抽象

### 2.接口：对行为的抽象

## 八丶匿名内部类 （用在接口上）✤

```java
// 假设已经有了Human接口
new Human{
@override
public void eat() {
 System.out.println（"中国人吃中国菜"）;
}
@override
public void run()
}.eat()
```

## 九丶Object类（超类：superclass） -> 所有派生类的基类

## 十、IO, Stream -> Java自带的包不常用，更常用的是*第三方包* （maven repository 里面去找） ★

