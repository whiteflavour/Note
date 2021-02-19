# 写在最前

> “考试的、学理论的给我滚！”
>
>  ——@Frank Xiang



# Java怎么执行的

## .exe和.class的区别

- .exe是win系统特有的
- .class字节码文件是跑在jvm上的
  - 特殊的可执行文件，需要jvm
  - 优点：跨平台
  - 缺点：过于依赖虚拟机

## 模拟执行

```java
//假如此时有一个Test.java文件
public class Test{
    //main函数：程序入口点
    public static void main(String[] args){
        System.out.println("Hello!");
    }
}
```

- 执行过程如下：

```shell
javac Test.java
java Test
Hello!
```

# Package

- 包名：com.公司.模块（**不能用复数！！！**不能tools！！！）

- eg. com.microsoft.demo

- 本质：“包”就是“文件夹”

- 定位

  ```java
  package com.microsoft.demo
  ```

- 导包

  ```java
  import com.google.* //*代表全部导入
  ```

- java.lang包、java.io包是java自带的，包括了很多基础功能

  - 不用导，是亲孩子
  - 像常用的java.util，是需要导的（eg.Random）

# 注释和文档

- 生成Java文件的API
  - 网上查阅JavaDoc的详解，都找得到
    - @author
    - @since
    - @version
  - 指令

```shell
javadoc Main.java
```

- 打开生成API的目录——**index.html**
- **方法外部注释一定要用/**,不要用//**
- 方法内部注释，单行用//，多行用/*（在语句上面写，且//后面加空格）
- 所有**类**都要加上**创作者和日期**
- 特殊注释标记（标记人，标记时间，[预计处理时间]）
  - TODO：需要实现，但还未实现
  - FIXME：错误代码，无法工作，需要纠正

# 注意事项

## 常量

- 常量定义不同于c/c++
  - c/c++：const
  - Java：final

## 字符串

- 格式化输出
  - System.out.printf();（同C语言）
- 格式化创建
  - String.format();
- 等等一系列操作，一定要下功夫，很重要！包括正则表达式。
- 为了开发的友好，隐含了’\0’
  - ‘\0’的作用——结束符，堵住字符串，不然会“烫烫烫”

## 自动类型转换

- 从低到高

  ：byte/short/char->int->long->float->double

  - 《主角与配角》小品（朱时茂、陈佩斯）
    - 前半段：int与char
    - 后半段：String与char——有函数不用
  - 能String就不要char

## 数组

- 初始化

```java
int[] arr = {1,2,3};	//不同于C
int arr[] = {1,2,3};	//也可以，但不是首选
```

- 分配方式——对象

```java
int[] arr = new int[5];	//类似于malloc()
```

- 数组的length是变量，**不用括号**！

以上都是**静态数组**，Java不常用，因为**无法扩容**！！

```java
Arrays.sort(arr);	//排序方法
Arrays.binarySearch(val);	//二分查找
Arrays.fill(arr,-1);	//类似c的memset(),用来初始化
```

- 动态的内存分配
- 很多方法可以调用

## 增强for循环——For Each

```java
for(int num:list){
	System.out.println(num);
}
```

# 方法的重载

- **方法名字相同**
- 参数不同
  - 个数
  - 类型
- 举例：求和函数

```java
public static int sum(int x,int y){
	return x + y;
}
public static double sum(int x,int y){
	return x + y;
}
public static int sum(int x,int y,int z){
	return x + y + z;
}
```

- **优点——一个名字闯天下**

# 面向过程——POP

- 走一步看一步
- 目标不明确的咸鱼
- 不适用普遍情况

# 面向对象——OOP

- 目标明确——即“对象”
- 程序大众化，普遍
- 过程弱化，不惜一切代价达成目标
- 举例：
  - 明确目标——考取研究生
  - 设计计划——复习计划
  - 执行计划——读书
  - 达成目标——考取
- **本质——站在更高层面看问题、看事物**

## 类与对象

- 对象——具体
- 类——抽象
- 属性 = 变量+ 方法（包括共性、特性）
- **类中的变量——成员**
  - 它们构成了类，是类的重要组成部分
- **类中的方法——行为**
  - 谁调用的“方法”，谁就是“this”

## 空指针异常

个人理解——**对象即指针**

```java
//分配一块Dog的内存，让指针puppy指向这块内存
Dog puppy = new Dog();
puppy.name = "Emy";
puppy.age = 2;
//正常运行
puppy.eat();
//对象销毁——指针
puppy = null;
//Error:NullPointerException
puppy.eat();
```

- 实际情况是——指针指向对象，**对象才是那块内存**
- 对象null了之后，内存被破坏，当垃圾回收了，也就是原来的内存已经GG了
- 要用只能再new了

## 垃圾回收机制

背景：在C / C ++中，程序员负责对象的创建和销毁。通常，程序员会忽略无用对象的破坏。由于这种疏忽，在某些时候，对于创建新对象，可能没有足够的内存，并且整个程序将异常终止，从而导致OutOfMemoryErrors。但是在Java中，程序员不必关心不再使用的所有那些对象。垃圾收集器会破坏这些对象。垃圾收集器是Daemon线程的最佳示例，因为它始终在后台运行。垃圾收集器的主要目标是通过破坏无法访问的对象来释放堆内存。

- 相当于“移民”，你人走了，档案就被撤销了，原来赋值的属性那块内存也被破坏了，就被回收掉了
- 在main()里，System.gc()【手动】
- 但其实是自动回收的，我们不用管

## 异常

- 运行时异常
  - 遇到异常就停了
- 非运行时异常
  - 编译不通过

## OOP封装

- public——不安全，用户可以为所欲为（比如：balance余额）

- private——安全，私有的，用户没法操作

  - 那用户怎么设置属性呢？举个例子：（年龄的设置和访问）

  ```java
  //用public的方法给用户提供服务
  public void setAge(int age){
      if(age < 0 || age > 100){
          this.age = 0;
      }else{
          this.age = age;
      }	
  }
  
  public int getAge(){
  	return this.age;
  }
  ```

- **作用——避免用户不合法操作**

- 实质

  - setter()
  - getter()

- Lombok的jar包——直接加入插件就行

  - @Getter
  - @Setter
  - @ToString
  - @Data（代表了equals()、toString()、hashCode()）
  - 一般写在类上，也可以单独写在属性前

## OOP继承

- 特点：**上梁不正下梁歪**

- 在类后**extends**

- 如果前面@Setter、@Getter过了，不用再@一遍了

- 不能**多继承**（C++支持，因为“杂交”过于复杂，Java取消了）

  ```java
  //错的,无法同时
  class Human extends Animal,Monkey;
  
  //对的
  class Monkey extends Animal;
  class Human extends Monkey;
  ```

- 方法重写：@Override

- super.父类方法()——**“啃老”**（@Override后自动生成）

- 儿子无法继承父亲的构造器——**你老子还是你老子**

  - 解决方法：**啃老啃到底**——在构造方法里super(field);
  - 也可以自己写——**儿子出息了**

- final——**断子绝孙**

  - 修饰符

  - 无法继承

  - 方法final，无法被重写，**只能用爸爸准备好的**

  - **需要写死就final**，比如一些固定的静态常量

    - 即使在同一个类中也改不动

    - 常量定义需要全**大写**，单词用下划线隔开（ctrl+shift+u=变大写）

    - 一次定义终生使用

    - eg.

      ```java
      // 常量定义，避免后续误操作
      private static final String TEXT_COMMUNITY_NAME = "flower";
      ```

### 权限修饰符/访问控制修饰符

| 修饰符      | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包)    | 其他包 |
| ----------- | ------ | -------- | -------------- | ----------------- | ------ |
| `public`    | Y      | Y        | Y              | Y                 | Y      |
| `protected` | Y      | Y        | Y              | Y/N（见下方解释） | N      |
| `default`   | Y      | Y        | Y              | N                 | N      |
| `private`   | Y      | N        | N              | N                 | N      |

protected 需要从以下两个点来分析说明：

- **子类与父类在同一包中**：被声明为 protected 的变量、方法和构造器能被同一个包中的任何其他类访问；
- **子类与父类不在同一包中**：那么在子类中，子类实例可以访问其从父类继承而来的 protected 方法，而不能访问父类实例的protected方法。

protected 可以修饰数据成员，构造方法，方法成员，**不能修饰类（内部类除外）**。

- 个人理解：protected就是“对自己的家人和邻居好，即使家人去了外地，我们也还是一家人；但邻居搬家搬到别处去了我也管不着了。”

**请注意以下方法继承的规则：**

- 父类中声明为 public 的方法在子类中也必须为 public。
- 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
- 父类中声明为 private 的方法，不能够被继承。

## OOP多态

- 要有**继承**关系
- 本质——**“花木兰替父从军”**

```java
// 替父从军 向上转型
HuaHu huaHu = new HuaMuLan();
System.out.println(huaHu.name);
System.out.println(huaHu.age);
huaHu.fight();

// 有一天，仗打完了，遇上自己心爱的人,做回自己 向下转型
HuaMuLan huaMuLan = (HuaMuLan)huaHu;
System.out.println(huaMuLan.name);
System.out.println(huaMuLan.age);
huaMuLan.dressing();
```

上面这段程序的输出：

> HuaHu
>
> 45
>
> 干架！
>
> HuaMuLan
>
> 19
>
> 化妆！

- 吕子乔类似 aka.吕小布
- **多个行为，功能多了**

# JAR包

- 直接上Maven Repository
- 工程下New Directory
- 右键->add as library
- 设置-编译器-Annotation-第一行Enable
- 遇到问题在插件里进官网，找github（版本很重要！）
- 以后尽量用Maven/Gradle
- 特殊情况，方法重写
  - 比如setAge有年龄限制，再写一遍就好

# JVM中的堆栈

## 堆（heap）

- 用于存放所有的Java对象

## 栈（stack）

- 用于存放基本类型数据和对象的引用

# 变量的声明与使用

## 基本类型

- boolean
- char
- byte(-128-127，signed)
- short
- int
- long
- float
- double

(String不是！！！)

### 关于内存

- 声明时，会在栈中分配内存
- 赋值时，把数据放进内存

## 对象——【指针】

### 输出

- 输出一个对象——包名@地址
- 如果需要输出对象的属性，就需要在类里——**toString()**，类上@Override

### 声明

- 声明一个对象类型的变量时，会在栈中分配内存
- 这块内存用来存储一个**对象的引用（存的是空间地址）**【暂且理解为“**指针**”】

### 赋值

- new一个对象，会在堆中分配内存来**存储对象**
- 将该对象类型变量赋值给另一个变量时，相当于两个变量都**引用了这个对象**

### 调用

- 英文的(.)
- 先找对象类型
- 再找对象类型里的成员
- 引用和对象的关系
  - 遥控器——引用
  - 电视机——对象

# 构造函数/构造器

- new一个对象相当于【注册账户】
- 构造函数相当于【注册时填写用户名、密码、邮箱】
- setter()相当于【注册后再补充资料】
- 本质——**初始化对象：定义+使用**
- **与类名相同**
- Java当创建一个类，**默认隐藏有一个无参的构造函数**
  - 自己写了有参的，一定要再写一个无参的
- 一样可以写很多个类型——**重载**

# 静态变量/方法

- 静态属于类，不属于方法

- 不依赖对象

- **要用public**

  ```java
  /* 有一个Dogs类 */
  
  // flower小区
  public static String community = "flower";
  
  // 狗狗月底都要打针
  public static void injection(){
      System.out.println("所有狗狗月底都要打针！");
  }
  
  // main()里调用
  String str = Dogs.community;
  Dogs.injection();
  ```

- 就算没有“用户注册”，我也知道我小区是啥（**静态，也就是那些不变的属性**）

- 具有强制性，在最上层

- **本质——“所有都”**

- 但是这时候存在缺陷，它没被封装起来，有风险啊！！！咋办？

  ```java
  // flower小区
  private static String community = "flower";
  
  // getInstance()方法——静态不用this
  public static String getCommunityInstance(){
      return community;
  }
  
  // main()里调用
  String str = Dogs.getCommunityInstance();
  ```

# static单例模式

- **设计模式——单例**
- **只有一个！**eg.太阳，地球…

```java
public class Earth{
    //在类里new好，无论怎么get，都是这块内存
	private static Earth earthInstance = new Earth();
    //无参构造——外部类就无法new了
    private Earth(){
        
    }
    //暴露给外部——获取单个实例
    public static Earth getEarthInstance(){
        return earthInstance;
    }
}
```

**在main()里调试：**

```java
Earth earth = Earth.getEarthInstance();
Earth earth2 = Earth.getEarthInstance();
Earth earth3 = Earth.getEarthInstance();
System.out.println("earth = " + earth);
System.out.println("earth2 = " + earth2);
System.out.println("earth3 = " + earth3);
```

**输出结果：**

```java
earth = com.microsoft.demo.Earth@74a14482
earth2 = com.microsoft.demo.Earth@74a14482
earth3 = com.microsoft.demo.Earth@74a14482
```

- **结论：证明你get再多，也就是那一个对象**

# 内部类

- **不推荐！！！！**
- 实际工作中并不常用
- 一个文件里只能有一个public class
- 会用的是“**匿名内部类**”
- 静态内部类只能用静态变量
- 可以在方法里写个class，并且这个类只能在该方法中有效

# 抽象与具体

## 衍生

- 问题提出
  - 最开始的父类Animal没人用咋办？？？
  - 写继承类有些方法程序员忘记写继承了咋办？？？（比如老鼠还是“动物叫”）
- 本质来说，最开始的父类是没有人用的，它是抽象的，抽取了各种动物的共性，实际是没人new它的
- **抽象出现的目的是为了概括具体的共性**

```java
// 将Animal改成抽象类
public abstract class Animal{}

// 下面开始报错
Animal animal = new Animal();
```

## 使用

- 避免忘记，在抽象类中的方法前面加上abstract

  ```java
  // 一定需要被继承实现
  public abstract void barking();
  ```

- 只要有抽象方法，类必须抽象；但抽象类不一定有抽象方法

- 一旦抽象，就无法new了

  ```java
  new Animal();// 会报错的！！！
  ```

- 当一个类继承一个抽象类，此时，该子类必须重写抽象类的抽象方法

# 接口（Interface）

- 当一个抽象类中都是抽象方法，没有必要写抽象类，直接上接口
- 接口里的方法，**都是抽象方法**
- 接口不是继承extends，是**implements**
- 抽象类的方法我们叫**重写**，接口的方法我们叫**实现**
- 工作应用：DAO Service

## 抽象类与接口的区别

- 抽象类是对**具体事物**的抽象，针对具体事物【根源】
- 接口是对它的**行为**进行抽象，针对行为
- 抽象类不能new，接口可以new

# 匿名内部类

- 举个例子(假设Human是个接口)

```java
// 一般用法：内部类
Human chinese = new Human(){
	
	@Override
	public void eat(){
		System.out.println("吃中国菜！");
	}

};
chinese.eat(); 

// 高端用法：匿名内部类
new Human(){
	
	@Override
	public void eat(){
		System.out.println("吃中国菜！");
	}

}.eat();
```

# 所有类的爸爸——Object

- 包括自己定义的类，默认extends Object
- 所以toString()、equals()、hashCode()等等可以@Override
- 推荐好物：Apache的开源IO工具包Commons