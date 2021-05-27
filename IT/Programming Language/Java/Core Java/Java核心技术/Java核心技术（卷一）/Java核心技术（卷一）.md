# Java核心技术（卷Ⅰ）

## 第一章、Java程序设计概述

## 1.1 Java程序设计平台

### 1.Java和C++最大的不同在于Java采用的指针模型可以消除重写内存和损坏数据的可能性。-> P1

---

## 第二章、Java程序设计环境

---

## 第三章、Java的基本程序设计结构

## 3.1 一个简单的Java应用程序

### 2.Java 中的所有函数都属于某个类的方法（标准术语将其称为方法， 而不是成员函数）。因此，Java 中的 main 方法必须有一个外壳类。-> P30

### 3.所不同的是 main 方法没有为操 作系统返回“ 退出代码” . . 如果 main 方法正常退出， 那么 Java 应用程序的退出代码为 0, 表示成功地运行了程序。如果希望在终止程序时返回其他的代码， 那就需要调用 *System, exit* 方法。-> P30

## 3.3 数据类型

## 3.3.1 整型

### 4.注意， Java 没有任何无符号（unsigned) 形式的 int、 long、short 或 byte 类型。-> P33

## 3.3.3 char 类型

### 5.： Unicode 转义序列会在解析代码之前得到处理。 -> P34

## 3.3.4 Unicode 和 char 类型

### 6.强烈建议不要在程序中使用 char 类型，除非确实需要处理 UTF-16 代码单元。最好 将字符串作为抽象数据类型处理。 -> P35

## 3.5 运算符

### 7.因此，这两种 方式的区别仅仅在于采用默认的方式不会产生溢出， 而采用严格的计算有可能产生溢出。 -> P39

## 3.5.1 数学函数与常量

### 8.floorMod 方法的目的是解决一个长期存在的有关整数余数的问题。 -> P39

### 9.如果得到一个完全可预测的结果比运行速度更重要的话， 那么就应该使用 StrictMath 类。 -> P40

## 3.5.3 强制类型转换

### 10.如果想对浮点数进行舍入运算，那就需要使用 Math.round 方法。 -> P41

### 11.只有极少数的情况才需要将布尔类型转换为数值类型，这时可以使用条件表 达式 b ? 1:0。 -> P42

## 3.5.5 自增与自减运算符

### 12.建议不要在表达式中使用 ++, 因为这样的代码很容易让人闲惑，而且会带来烦人的 bug。 -> P42

## 3.5.7 位运算符

### 13.不过 & 和丨运算符不采用“ 短路” 方式来求值。 -> P43

### 14.>>> 运算符会用 0 填充高位，这与 >> 不同，它会用符号位填充高位。 -> P44

## 3.6 字符串

## 3.6.2 拼接

### 15.如果需要把多个字符串放在一起， 用一个定界符分隔，可以使用静态 join 方法。 -> P46

## 3.6.4 检测字符串是否相等

### 16.一定不要使用 == 运算符检测两个字符串是否相等！ 这个运算符只能够确定两个字串 是否放置在同一个位置上。当然， 如果字符串放置在同一个位置上， 它们必然相等。但是， 完全有可能将内容相同的多个字符串的拷贝放置在不同的位置上。 -> P48

### 17.如果虚拟机始终将相同的字符串共享， 就可以使用 == 运算符检测是否相等。但实际上 只有字符串常量是共享的，而 + 或 substring 等操作产生的结果并不是共享的。 -> P48

## 3.6.5 空串与Null串

### 18.空串是一个 Java 对象， 有自己的串长度（ 0 ) 和内容（空）。不过， String 变量还可以存 放一个特殊的值， 名为 null, 这表示目前没有任何对象与该变量关联。 -> P48

## java.lang.string 1.0

### 19.除非对底层的代码单元感兴趣， 否则不需要调用这个 方法。 -> P50

```java
char charAt(int index)
```

---

### 20.可 以用 String 或 StringBuilder 对象作为 CharSequence 参数。 -> P51

## 3.6.9 构建字符串

### 21.有些时候， 需要由较短的字符串构建字符串， 例如， 按键或来自文件中的单词。采用字 符串连接的方式达到此目的效率比较低。每次连接字符串， 都会构建一个新的 String 对象， 既耗时， 又浪费空间。使用 StringBuilder类就可以避免这个问题的发生。 -> P54

### 22.在 JDK5.0 中引入 StringBuilder 类。 这个类的前身是 StringBuffer, 其效率稍有些 低， 但允许采用多线程的方式执行添加或删除字符的操作 U 如果所有字符串在一个单线 程中编辑 （通常都是这样，) ， 则应该用 StringBuilder 替代它。 这两个类的 API是相同的。 -> P54

## 3.7 输入输出

## 3.7.1 读取输出

### 23.因为输入是可见的， 所以 Scanner 类不适用于从控制台读取密码。Java SE 6 特别 引入了 Console 类实现这个目的。 -> P57

### 24.采用 Console 对象处理输入不如采用 Scanner 方便。每次只能读取一行输入， 而没有能够读取一个单词或一个数值的方法。 -> P57

## 3.7.2 格式化输出

### 25.参 教 索 引 值 从 i 开 始， 而 不 是 从 0开 始， 对 第 1 个 参 数 格 式 化 这 就 避 免 了 与 0 标 志 混 淆。 -> P60

## 3.7.3 文件输入与输出

### 26.如果文件名中包含反斜杠符号，就要记住在每个反斜杠之前再加一个额外的反斜杠： “ c:\\mydirectory\\myfile.txt ”。 -> P61

### 27.： 在这里指定了 UTF-8 字符编码， 这对于互联网上的文件很常见（不过并不是普遍 适用）。如果 省略字符编码， 则会使用运行这个 Java 程序的机器的“ 默认编码”。 这不是一个好主意， 如果在不同的机器上运行这个程序， 可能会有不同的表现。 -> P61

```java
Scanner in = new Scanner(Paths.get("niyflle.txt"), "UTF-8");
```

---

### 28.要记住一点：如果 用一个不存在的文件构造一个 Scanner, 或者用一个不能被创建的文件名构造一个 PrintWriter, 那么就会发生异常。Java 编译器认为这些异常比“ 被零除” 异常更严重。 -> P62

## 3.8 控制流程

## 3.8.1 块作用域

### 29.一个块可以嵌套在另一个块中。但是，不能在嵌套的两个块中声明同名的变量。 -> P63

### 30.在 C++ 中， 可以在嵌套的块中重定义一个变量。在内层定义的变量会覆盖在外层定义的变量。这样，有可能会导致程序设计错误， 因此在 Java 中不允许这样做。 -> P63

## 3.8.2 条件语句

### 31.其中 else 部分是可选的。else 子句与最邻近的 if 构成一组。 -> P65

## 3.8.4 确定循环

### 32.在循环中，检测两个浮点数是否相等需要格外小心。下面的 for 循环

```java
for (double x = 0; x != 10; x += 0.1) . . . 
```

### 可能永远不会结束。 由于舍入的误差， 最终可能得不到精确值。 例如， 在上面的循环中， 因为 0.1 无法精确地用二进制表示， 所以，x 将从 9.999 999 999 999 98 跳到 10.099 999 999 999 98。 -> P70

---

## 3.8.5 多重选择：swich 语句

### 33.标注是为了编译器或处理 Java 源文件或类文件的工具提供信息的一种机制。 -> P73

### 34.case 标签可以是：

 •类型为 char、byte、 short 或 int 的常量表达式。

 •枚举常量。

 •从 Java SE 7开始， case 标签还可以是字符串字面量。

-> P73

## 3.8.6 终端控制流程语句

### 35.与 C++ 不同，Java 还提供了一种带标签的 break语句，用于跳出多重嵌套的循环语句。 -> P75

### 36.请注意，标签必须放在希望跳出的最外 层循环之前， 并且必须紧跟一个冒号。 -> P75

### 37.因此，如果希望使用一条 goto 语句， 并将一个标签放在想要跳到的语句块之前， 就 可以使用 break 语句！ 当然，并不提倡使用这种方式。另外需要注意， 只能跳出语句块， 而不能跳入语句块。 -> P75

## 大数值

### 38.如果基本的整数和浮点数精度不能够满足需求， 那么可以使用java.math 包中的两个很有用的类：Biglnteger 和 BigDecimal。 -> P76

### 39.遗憾的是，不能使用人们熟悉的算术运算符 (如：+ 和 * ) 处理大数值。 而需要使用大数值类中的 add 和 multiply 方法。 -> P76

### 40.与 C++ 不同， Java 没有提供运算符重载功能。 程序员无法重定义 + 和 * 运算 符， 使其应用于 BigInteger 类的 add 和 multiply 运算。Java 语言的设计者确实为字符串 的连接重栽了 + 运算符，但没有重载其他的运算符，也没有给 Java 程序员在自己的类中 重栽运算符的机会 。 -> P76

## 3.10 数组

### 41.数组长度不要求是常量：

```java
new int[n]
```

### 会创建 一个长度为 n 的数组。 -> P79

---

### 42.创建一个数字数组时， 所有元素都初始化为 0。boolean 数组的元素会初始化为 false对 象数组的元素则初始化为一个特殊值 null, 这表示这些元素（还）未存放任何对象。 -> P79

## 3.10.1 for each 循环

### 43.有个更加简单的方式打印数组中的所有值， 即利用 Arrays 类的 toString 方法。 -> P80

## 3.10.2 数组初始化以及匿名数组

### 44.甚至还可以初始化一个匿名的数组：

```java
small Primes = new int[] { 17, 19, 23, 29, 31, 37 }; 
```

### -> P80

---

### 45.在 Java 中， 允许数组长度为 0。在编写一个结果为数组的方法时， 如果碰巧结果 为空， 则这种语法形式就显得非常有用。此时可以创建一个长度为 0 的数组： new elementType[0] 注意， 数组长度为 0 与 null 不同。 -> P81

## 3.10.3 数组拷贝

### 46.在 Java 中，允许将一个数组变量拷贝给 另一个数组变量。这时， 两个变量将引用同 一个数组：

```java
intQ luckyNumbers = smallPrimes; 
luckyNumbers[S] = 12; // now smallPrimes[5] is also 12
```

![Java核心技术（卷一） 数组拷贝](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一） 数组拷贝.png)

---

### 47.如果希望将 一个数组的所有值拷贝到一个新的数组中去， 就要使用 Arrays 类的 copyOf方法：

```java
int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);
```

###  第 2 个参数是新数组的长度。这个方法通常用来增加数组的大小： 

```java
luckyNumbers = Arrays.copyOf(luckyNumbers , 2 * luckyNumbers.length);
```

### 如果数组元素是数值型，那么多余的元素将被赋值为 0 ; 如果数组元素是布尔型，则将赋值 为 false。相反，如果长度小于原始数组的长度，则只拷贝最前面的数据元素。 -> P81

---

### 48.Java 数组与 C++ 数组在堆栈上有很大不同， 但基本上与分配在堆（heap) 上 的数组指针一样。 -> P81

### 49.Java 中的 [ ] 运算符被预定义为检查数组边界，而且没有指针运算， 即不能通过 a 加 1 得到数组的下一个元素。 -> P81

## 3.10.4 命令行参数

### 50.在 Java 应用程序的 main 方法中， 程序名并没有存储在 args 数组中u 例如, 当使用下列命令运行程序时

```powershell
java Message -h world 
```

### args[0] 是“ -h”， 而不是“ Message” 或“ java”。 -> P82

---

## 3.10.5 数组排序

### 51.要想对数值型数组进行排序， 可以使用 Arrays 类中的 sort 方法：这个方法使用了优化的快速排序算法。快速排序算法对于大多数数据集合来说都是效率比较高的。 -> P82

### 52.Math.random 方法将返回一个 0 到 1 之间（包含 0、 不包含 1 ) 的随机浮点数。用 乘以这个浮点数， 就可以得到从 0 到 n-1之间的一个随机数。 -> P83

## 3.10.6 多维数组

### 53. for each 循环语句不能自动处理二维数组的每一个元素。它是按照行， 也就是一维 教组处理的要想访问二维教组 a 的所有元素， 需要使用两个嵌套的循环， 如下所示：

 ```java
for (doubleG row : a) {
	for (double value : row) {
		do something with value
	}
}
 ```

### -> P86

---

### 54.要想快速地打印一个二维数组的数据元素列表， 可以调用：

```java
 System.out.println(Arrays.deepToString(a));
```

### -> P86

---

## 3.10.7 不规则数组

### 55.但实 际存在着一些细微的差异， 而这正是 Java 的优势所在：Java 实际上没有多维数组，只有一维数组。多维数组被解释为“数组的数组。” -> P88

---

## 第四章 、对象与类

## 4.1 面向对象程序设计概述

### 56.传统的结构化程序设计通过设计一系列的过程（即算法）来求解问题。需要注意的是，在 Wirth 命名的书名中， 算法是第一位的，数据结构是第二位的，这就明确地表述了程序员的工作方式。首先要确定如何操作数据， 然后再决定如何组织数据， 以便于数据操作。 而 OOP 却调换了这个次序， 将数据放在第 一位，然后再考虑操作数据的算法。对于一些规模较小的问题， 将其分解为过程的开发方式比较理想。而面向对象更加适用 于解决规模较大的问题。 -> P92

## 4.1.1 类

### 57. 由类构造（construct) 对象的过程称为创建类的实例 （instance ). -> P92

## 4.2 使用预定义类

## 4.2.1 对象与对象变量

### 58. 如果使用类， 这些设计任务就交给了类库的设计者。如果类设计的 不完善， 其他的操作员可以很容易地编写自己的类， 以便增强或替代（ replace) 系统提供 的类（作为这个问题的印证：Java 的日期类库有些混乱， 已经重新设计了两次)。 -> P96

### 59. 在对象与对象变量之间存在着一个重要的区别。例如， 语句 

```java
Date deadline; // deadline doesn't refer to any object 
```

### 定义了一个对象变量 deadline, 它 可 以 引 用 Date 类型的对象。但是，一定要认识到： 变量 deadline 不是一个对象， 实际上也没有引用对象。此时，不能将任何 Date 方法应用于这个变 量上。语句 

```java
s = deadline.toString(); // not yet 
```

### 将产生编译错误。 -> P97

---

### 60. 一定要认识到： 一个对象变量并没有实际包含一个对象，而仅仅引用一个对象。 在 Java 中，任何对象变量的值都是对存储在另外一个地方的一个对象的引用。new 操作 符的返回值也是一个引用。下列语句：

```java
Date deadline = new Date();
```

### 有两个部分。表达式 new Date() 构造了一个 Date 类型的对象， 并且它的值是对新创建对象的 引用。这个引用存储在变量 deadline 中。

### 可以显式地将对象变量设置为 mil，】 表明这个对象变量目前没有引用任何对象。

```java
deadline = null;
...
if (deadline != null)
	System.out.println(deadline);
```

### 如果将一个方法应用于一个值为 null 的对象上，那么就会产生运行时错误。

```java
birthday = null;
String s = birthday.toStringQ; // runtime error!
```

### 局部变量不会自动地初始化为 null，而必须通过调用 new 或将它们设置为 null 进行初始化。 -> P98

---

### 61. 很多人错误地认为 Java 对象变量与 C++ 的引用类似。然而，在 C++ 中没有 空引用， 并且引用不能被赋值。可以将 Java 的对象变量看作 C++ 的对象指针。例如，

```java
Date birthday; // Java
```

### 实际上，等同于

```c++
Date* birthday; // C++
```

### 一旦理解了这一点， 一切问题就迎刃而解了。 当然，一个 Date* 指针只能通过调用 new 进行初始化。就这一点而言，OH■ 与 Java 的语法几乎是一样的 。 -> P98

### 62. 有关世界上各种日历的有趣解释， 从法国革命的日历到玛雅人计算 曰期的方法等， 请参看 Nachum Dershowitz 和 Edward M. Reingold 编写的《 Calendrical Calculations》第 3 版（剑桥大学出版社，2007 年）。 -> P99

### 63. 将时间与日历分开是一种很好的面向对象设计。通常，最好使用不同的类表示不同的概念。 -> P99

### 64. 不要使用构造器来构造 LocalDate 类的对象。实际上，应当使用静态工厂方法 (factory method) 代表你调用构造器。下面的表达式

```java
Local Date.now()
```

### 会构造一个新对象，表示构造这个对象时的日期。 -> P99

---

### 65. 实际上，Date 类还有 getDay、getMonth 以及 getYear 等方法， 然而并不推荐使用 这些方法。 当类库设计者意识到某个方法不应该存在时， 就把它标记为不鼓励使用。 -> P99

## 4.2.3 更改器方法与访问器方法

### 66. 再来看上一节中的 plusDays 方法调用：

```java
LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);
```

### 这个调用之后 newYeareEve 会有什么变化？ 它会改为 1000 天之后的日期吗？ 事实上，并没 有。plusDays 方法会生成一个新的 LocalDate 对象，然后把这个新对象赋给 aThousandDaysLater 变量。原来的对象不做任何改动。 我们说 plusDays 方法没有更改调用这个方法的对象。（这类 似于第 3章中见过的 String 类的 toUpperCase 方法。在一个字符串上调用 toUpperCase 时，这 个字符串仍保持不变，会返回一个将字符大写的新字符串。） -> P100

---

### 67. Java 库的一个较早版本曾经有另一个类来处理日历，名为 GregorianCalendar。 可以如下 为这个类表示的一个日期增加 1000 天：

```java
Cregori anCalendar someDay = new CregorianCalendar(1999, 11, 31);
// Odd feature of that cl ass: month numbers go from 0 to 11
someDay.add(Calendar.DAY_0F_M0NTH, 1000);
```

### 与 LocalDate.plusDays 方法不同，GregorianCalendar.add 方法是一个更改器方法 ( mutator method ) 调用这个方法后，someDay 对象的状态会改变。可以如下査看新状态：

```java
year = someDay.get(Calendar.YEAR); // 2002
month = someDay.get(Calendar.MONTH)+ 1; // 09
day = someDay.get(Ca1endar.DAY_0F_M0NTH); // 26
```

-> P100

---

## 4.3 用户自定义类

## 4.3.4 从构造器开始

### 68. 构造器与其他的方法有一个重要的不同。构造器总是伴随着 new 操作符的执行被调用， 而不能对一个已经存在的对象调用构造器来达到重新设置实例域的目的。 -> P107

### 69. Java 构造器的工作方式与 C++ —样。但是， 要记住所有的 Java 对象都是在 堆中构造的， 构造器总是伴随着 new 操作符一起使用。 -> P107

### 70.请注意， 不要在构造器中定义与实例域重名的局部变量。例如， 下面的构造器将 无法设置 salary。

```java
public Employee(String n, double s, . .)
{
	String name = n; // Error
	double salary = s; // Error
	...
}
```

### 这个构造器声明了局部变量 name 和 salary。这些变量只能在构造器内部访问。这些变量屏蔽了同名的实例域。 -> P107

## 4.3.5 隐式参数与显式参数

### 71. 在 Java 中， 所有的方法都必须在类的内部定义， 但并不表示它们是内联方法。是否 将某个方法设置为内联方法是 Java 虚拟机的任务。即时编译器会监视调用那些简洁、经 常被调用、 没有被重载以及可优化的方法。 -> P109

## 4.3.6 封装的优点

### 72. 注意不要编写返回引用可变对象的访问器方法。在 Employee 类中就违反了这个设 计原则， 其中的 getHireDay 方法返回了一个 Date 类对象：

```java
class Employee
{
	private Date hireDay;
	...
	public Date getHireDay();
	{
		return hireDay; // Bad
	}
	...
}
```

### LocalDate 类没有更改器方法， 与之不同， Date 类有一个更改器方法 setTime, 可以 在这里设置毫秒数。

### 出错的原因很微妙。d 和 harry.hireDay 引用同一个对象（请参见图 4-5 )。对 d 调用更改器方法就可以自动地改变这个雇员对象的私有状态！

![Java核心技术（卷一）返回可变数据域的引用](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）返回可变数据域的引用.png)



### 如果需要返回一个可变对象的引用， 应该首先对它进行克隆（clone )。对象 clone 是 指存放在另一个位置上的对象副本。 有关对象 clone 的详细内容将在第 6 章中讨论。 下 面是修改后的代码：

```java
class Employee
{
	...
	public Date getHireDay()
	{
		return (Date) hireDay.clone(); // Ok
	}
	...
}
```

### 凭经验可知， 如果需要返回一个可变数据域的拷贝，就应该使用 clone。 -> P111

## 4.4.2 静态常量

### 73. 如果查看一下 System 类， 就会发现有一个 setOut 方法， 它可以将 System.out 设 置为不同的流。 读者可能会感到奇怪， 为什么这个方法可以修改 final 变量的值。原因在 于， setOut 方法是一个本地方法， 而不是用 Java 语言实现的。本地方法可以绕过 Java 语 言的存取控制机制。这是一种特殊的方法， 在自己编写程序时， 不应该这样处理。 -> P114

## 4.4.4 工厂方法

### 74. 静态方法还有另外一种常见的用途。类似 LocalDate 和 NumberFormat 的类使用静态工 厂方法 (factory methocO 来构造对象。你已经见过工厂方法 LocalDate.now 和 LocalDate.of。 NumberFormat 类如下使用工厂方法生成不同风格的格式化对象：

```java
NumberFormat currencyFormatter = NumberFormat.getCurrencylnstance();
NumberFormat percentFormatter = NumberFormat.getPercentlnstance()；
double x = 0.1;
System.out.println(currencyFormatter.format(x)); // prints $O.10
System.out.println(percentFomatter.format(x)); // prints 10%
```

### 为什么 NumberFormat 类不利用构造器完成这些操作呢？ 这主要有两个原因： 

### •无法命名构造器。构造器的名字必须与类名相同。但是， 这里希望将得到的货币实例 和百分比实例采用不用的名字。

### •当使用构造器时，无法改变所构造的对象类型。而 Factory 方法将返回一个 DecimalFormat 类对象，这是 NumberFormat 的子类（有关继承的详细内容请参看第 5 章)。 -> P115

## 4.5 方法参数

### 75. Java 程序设计语言总是采用按值调用。也就是说， 方法得到的是所有参数值的一个拷 贝，特别是，方法不能修改传递给它的任何参数变量的内容。 -> P118

### 76. 然而，方法参数共有两种类型：

### •基本数据类型（数字、布尔值) 。

### •对象引用。 -> P118

### 77. 下面总结一下 Java 中方法参数的使用情况：

###  •一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）。

###  •一个方法可以改变一个对象参数的状态。

###  •一个方法不能让对象参数引用一个新的对象。 -> P120

## 4.6 对象构造

## 4.6.2 默认域初始化

### 78. 如果在构造器中没有显式地给域赋予初值，那么就会被自动地赋为默认值： 数值为 0、 布尔值为 false、 对象引用为 null。然而，只有缺少程序设计经验的人才会这样做。确实， 如 果不明确地对域进行初始化，就会影响程序代码的可读性。 -> P123

## 4.6.6 调用另一个构造器

### 79.  关键字 this 引用方法的隐式参数。然而，这个关键字还有另外一个含义。

### 	    如果构造器的第一个语句形如 this(...)， 这个构造器将调用同一个类的另一个构造器。下 面是一个典型的例子：

```java
public Employee(double s)
{
	// calls Employee(String, double)
	this("Employee #" + nextld, s);
	nextld++;
}
```

### -> P126

---

## 4.6.7 初始化块

### 80. 由于初始化数据域有多种途径，所以列出构造过程的所有路径可能相当混乱。下面是调用构造器的具体处理步骤： 

### 1 ) 所有数据域被初始化为默认值（0、false 或 null。) 

### 2 ) 按照在类声明中出现的次序， 依次执行所有域初始化语句和初始化块。

### 3 ) 如果构造器第一行调用了第二个构造器，则执行第二个构造器主体 

### 4 ) 执行这个构造器的主体.  -> P127

## 4.6.8 对象析构与finalize方法

### 81. 可以为任何一个类添加 finalize 方法。finalize 方法将在垃圾回收器清除对象之前调用。 在实际应用中，不要依赖于使用 finalize 方法回收任何短缺的资源， 这是因为很难知道这个 方法什么时候才能够调用。 -> P130

### 82. 有个名为 System.mnFinalizersOnExit(true) 的方法能够确保 finalizer 方法在 Java 关 闭前被调用。不过，这个方法并不安全，也不鼓励大家使用。有一种代替的方法是使用方法 Runtime.addShutdownHook 添加“ 关闭钓” （shutdown hook), 详细内容请参看 API 文档。 -> P130

### 83. 如果某个资源需要在使用完毕后立刻被关闭， 那么就需要由人工来管理。对象用完时， 可以应用一个 close 方法来完成相应的清理操作。7.2.5 节会介绍如何确保这个方法自动得到 调用。 -> P131

## 4.7 包

### 84. 从编译器的角度来看， 嵌套的包之间没有任何关系。例如，java.utU 包与java.util.jar 包 毫无关系。每一个都拥有独立的类集合。 -> P131

## 4.7.1 类的导入

### 85. 如果这两个 Date 类都需要使用，又该怎么办呢？ 答案是，在每个类名的前面加上完整的 包名。

```java
java.util.Date deadline = new java.util.Date();
java.sql.Date today = new java.sql.Date(...);
```

### -> P132

### 86. 在 C++ 中， 与 包 机 制 类 似 的 是 命 名 空 间（namespace)。 在 Java 中， package 与 import 语句类似于 C++ 中的 namespace 和 using 指令。 -> P133

### 87. 下面看一个更加实际的例子。在这里不使用默认包， 而是将类分别放在不同的包中 ( com. horstmann.corejava 和 com.mycompany)。

![Java核心技术（卷一）包](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）包.png)

### 在这种情况下，仍然要从基目录编译和运行类，即包含 com 目录：

```powershell
javac com/myconipany/Payrol1App.java
java com.mycompany.PayrollApp
```

### 需要注意，编译器对文件 （带有文件分隔符和扩展名 .java 的文件）进行操作。而 Java 解 释器加载类（带有 . 分隔符 )。 -> P134

---

## 4.8.1 设置类路径

### 88. 有人建议将 CLASSPATH 环境变量设置为永久不变的值。 总的来说这是一个很糟 糕的主意。 -> P139

### 89. 有人建议绕开类路径， 将所有的文件放在 jre/lib/ext 路径。这是一个极坏的主意。 -> P139

## 4.9 文档注释

### 90. JDK 包含一个很有用的工具，叫做javadoc, 它可以由源文件生成一个 HTML 文档。 -> P140

## 4.9.1 注释的插入

### 91. javadoc 实用程序（utility) 从下面几个特性中抽取信息：

### •包 

### •公有类与接口 

### •公有的和受保护的构造器及方法

### •公有的和受保护的域 -> P140

### 92. 在自由格式文本中，可以使用 HTML 修饰符， 例如，用于强调的

```html
<em>...</em>
```

### 用于 着重强调的

```html
<strong>...</strong>
```

### 以及包含图像的

```html
<img ...>
```

### 等。不过，一定不要使用

```html
<hl>
```

### 或 

```html
<hr>
```

### , 因为它们会与文档的格式产生冲突。若要键入等宽代码， 需使用 

```html
{@code ... }
```

### 而不是

```html
<code>...</code>
```

### 这样一来， 就不用操心对代码中的 < 字符转义了。 -> P140

## 4.10 类设计技巧

### 93. 1. 一定要保证数据私有

### 这是最重要的；绝对不要破坏封装性。 -> P144

### 94. 7.优先使用不可变的类

### 更改对象的问题在于， 如果多个线程试图同时更新一个对象，就会发生并发更改。其结 果是不可预料的。如果类是不可变的，就可以安全地在多个线程间共享其对象。 -> P146

## 第五章、继承

### 95. 反射是指在程序运行期间发现更多的类 及其属性的能力。这是一个功能强大的特性，使用起来也比较复杂。由于主要是开发软件 具的人员， 而不是编写应用程序的人员对这项功能感兴趣， 因此对于这部分内容，可以先浏览一下，待日后再返回来学习。 -> P147

## 5.1 类、超类和子类

## 5.1.2 覆盖方法

### 96. 然而， 超类中的有些方法对子类 Manager 并不一定适用。具体来说， Manager 类中的 getSalary方法应该返回薪水和奖金的总和。为此，需要提供一个新的方法来覆盖（override) 超类中的这个方法：

```java
public class Manager extends Employee {
	...
	public double getSalary() {
	...
	}
	...
}

```

### 应该如何实现这个方法呢？ 乍看起来似乎很简单， 只要返回 salary 和 bonus 域的总和就可以了：

```java
public double getSalary() {
	return salary + bonus; // won't work
}
```

### 然而，这个方法并不能运行。这是因为 Manager 类的 getSalary 方法不能够直接地访问超类的 私有域。也就是说，尽管每个 Manager 对象都拥有一个名为 salary 的域， 但在 Manager 类的 getSalary方法中并不能够直接地访问 salary 域。只有 Employee 类的方法才能够访问私有部 分。如果 Manager 类的方法一定要访问私有域， 就必须借助于公有的接口， Employee 类中的 公有方法 getSalary 正是这样一个接口。

### 现在，再试一下。将对 salary 域的访问替换成调用 getSalary 方法。

```java
public double getSalary() {
	double baseSalary = getSalary()；// still won't work
	return baseSalary + bonus;
}
```

### 上面这段代码仍然不能运行。问题出现在调用 getSalary 的语句上，这是因为 Manager 类 也有一个 getSalary方法（就是正在实现的这个方法，) 所以这条语句将会导致无限次地调用 自己，直到整个程序崩溃为止。

### 这里需要指出：我们希望调用超类 Employee 中的 getSalary 方法， 而不是当前类的这个 方法。为此， 可以使用特定的关键字 super 解决这个问题：

```java
super.getSalary()
```

### -> P149

---

### 97. 有些人认为 super 与 this 引用是类似的概念， 实际上，这样比较并不太恰当。这是 因为 super 不是一个对象的引用， 不能将 super 赋给另一个对象变量， 它只是一个指示编 译器调用超类方法的特殊关键字。 -> P150

### 98. 正像前面所看到的那样， 在子类中可以增加域、 增加方法或覆盖超类的方法，然而绝对 不能删除继承的任何域和方法。 -> P150

## 5.1.3 子类构造器

```java
public Manager(String name, double salary, int year, int month, int day) {
	super(name, salary, year, month, day);
	bonus = 0;
}
```

### 99.  使用 super 调用构造器的语句必须是子类构造器的第一条语句。 -> P150

### 100. 如果子类的构造器没有显式地调用超类的构造器， 则将自动地调用超类默认（没有参数 ) 的构造器。 如果超类没有不带参数的构造器， 并且在子类的构造器中又没有显式地调用超类 的其他构造器’ 则 Java 编译器将报告错误。 -> P150

## 5.1.6 理解方法调用

### 101. 在覆盖一个方法的时候，子类方法不能低于超类方法的可见性。特别是， 如果超类 方法是 public, 子类方法一定要声明为 public。 -> P157

## 5.1.7 阻止继承：final类和方法

### 102. final 类中的所有方法自动地成为 final 方法。 -> P158

## 5.1.8 强制类型转换

### 103. 因此，应该养成这样一个良好的程序 设计习惯：在进行类型转换之前，先查看一下是否能够成功地转换。这个过程简单地使用 instanceof 操作符就可以实现。 例如：

```java
if (staff[1] instanceof Manager) {
	boss = (Manager)staff[1];
	...
}
```

### -> P159

### 104. 综上所述：

* 只能在继承层次内进行类型转换。

* 在将超类转换成子类之前，应该使用 instanceof进行检查。

### -> P159

### 105. 如果 x 为 null , 进行下列测试

```java
x instanceof C
```

### 不会产生异常， 只是返回 false。之所以这样处理是因为 null 没有引用任何对象， 当 然也不会引用 C 类型的对象。 -> P160

### 106. 实际上，通过类型转换调整对象的类型并不是一种好的做法。在我们列举的示例中， 大 多数情况并不需要将 Employee 对象转换成 Manager 对象， 两个类的对象都能够正确地调用 getSalary 方法，这是因为实现多态性的动态绑定机制能够自动地找到相应的方法。 -> P160

### 107.只有在使用 Manager 中特有的方法时才需要进行类型转换， 例如， setBonus 方法o 如果 鉴于某种原因，发现需要通过 Employee 对象调用 setBomis 方法， 那么就应该检查一下超类 的设计是否合理。重新设计一下超类，并添加 setBonus 方法才是正确的选择。 -> P160 

### 108. 在一般情况下，应该尽量少用类型 转换和 instanceof 运算符。 -> P160

## 5.1.9 抽象类

### 109. 建议尽量将通用的域和方法（不管是否是抽象的）放在超类（不管是否是抽象类）中。 -> P161

### 110. 抽象方法充当着占位的角色， 它们的具体实现在子类中。扩展抽象类可以有两种选择。 一种是在抽象类中定义部分抽象类方法或不定义抽象类方法，这样就必须将子类也标记为抽 象类；另一种是定义全部的抽象方法，这样一来，子类就不是抽象的了。 -> P161

### 111. 需要注意， 可以定义一个抽象类的对象变量， 但是它只能引用非抽象子类的对象。 例如，

```java
Person p = new Student("Vinee Vu", "Economics");
```

### 这里的 p 是一个抽象类 Person 的变量，Person 引用了一个非抽象子类 Student 的实例。

###  -> P162

### 112. 请牢记，由于不能构造抽象类 Person 的对象， 所以变 量 p 永远不会引用 Person 对象 -> P163

### 113. 是否可以省略 Person 超类中的抽象方法， 而仅在 Employee 和 Student 子类中定义 getDescription方法呢？ 如果这样的话，就不能通过变量 p 调用 getDescription方法了。编译器只允许调用在类中声明的方法。 -> P165

## 5.1.10 受保护访问

### 114. 不过，Manager 类中的方法只能够访问 Manager 对象中的 hireDay 域， 而不能访问其他 Employee 对象中的这个域。这种限制有助于避免滥用受保护机制，使得子类只能获得访问受 保护域的权利。 -> P165

### 115. 在实际应用中，要谨慎使用 protected 属性。假设需要将设计的类提供给其他程序员使 用，而在这个类中设置了一些受保护域， 由于其他程序员可以由这个类再派生出新类，并访 问其中的受保护域。在这种情况下，如果需要对这个类的实现进行修改，就必须通知所有使 用这个类的程序员。这违背了 OOP 提倡的数据封装原则。 -> P 165

### 116. 事实上，Java 中的受保护部分对所有子类及同一个包中的所有其他类都可见。 这与 c++ 中的保护机制稍有不同， Java 中的 protected 概念要比 C++ 中的安全性差。 -> P165

### 117. 下面归纳一下 Java 用于控制可见性的 4 个访问修饰符：

1. 仅对本类可见 —— private。

2. 对所有类可见 —— public。

3. 对本包和所有子类可见 —— protected。

4. 对本包可见 —— 默认（很遗憾)， 不需要修饰符。

## 5.2 Object：所有类的超类

### 118. 由于在 Java中，每个类都 是由 Object 类扩展而来的，所以， 熟悉这个类提供的所有服务十分重要。 -> P166

### 119. 在 C++ 中没有所有类的根类，不过，每个指针都可以转换成 void* 指针。

## 5.2.1 equals 方法

### 120. Object 类中的 equals 方法用于检测一个对象是否等于另外一个对象。 -> P166

### 121. getClass 方法将返回一个对象所属的类，有关这个方法的详细内容稍后进行介绍。在检 测中， 只有在两个对象属于同一个类时， 才有可能相等。 -> P167

## 5.2.2 相等测试与继承

### 122. 在前面的例子中， 如果发现类不匹配， equals 方法就返冋 false: 但是， 许多程序员 却喜欢使用 instanceof 进行检测：

```java
if ( KotherObject instanceof Employee)) {
	return false;
}
```

### 这样做不但没有解决 otherObject 是子类的情况，并且还有可能会招致一些麻烦。这就是建议 不要使用这种处理方式的原因所在。

### Java 语言规范要求 equals 方法具有下面的特性：

1. 自反性： 对于任何非空引用 x, x.equals(?0 应该返回 true。
2. 对称性： 对于任何引用 x 和 y, 当且仅当 y.equals(x) 返回 true , x.equals(y) 也应该返回 true。
3. 传递性： 对于任何引用 x、 y 和 z, 如果 x.equals(y) 返 N true， y.equals(z) 返回 true, x.equals(z) 也应该返回 true。
4. 一致性： 如果 x 和 y 引用的对象没有发生变化，反复调用 x.equals(y) 应该返回同样的结果。
5. 对于任意非空引用 x, x.equals(null) 应该返回 false,

### -> P168

### 123. 然而， 集合是相当特殊的一个例子， 应该将 AbstractSet.equals 声明为 final , 这是因为没 有任何一个子类需要重定义集合是否相等的语义（事实上，这个方法并没有被声明为 final。 这样做， 可以让子类选择更加有效的算法对集合进行是否相等的检测）。 -> P168

### 下面可以从两个截然不同的情况看一下这个问题：

* 如果子类能够拥有自己的相等概念， 则对称性需求将强制采用 getClass 进行检测。
* 如果由超类决定相等的概念，那么就可以使用 imtanceof进行检测， 这样可以在不同 子类的对象之间进行相等的比较。

###  -> P169

### 124. 下面给出编写一个完美的 equals 方法的建议：

1. 显式参数命名为 otherObject, 稍后需要将它转换成另一个叫做 other 的变量。
2. 检测 this 与 otherObject 是否引用同一个对象：

```java
if (this = otherObject) {
	return true;
}
```

### 这条语句只是一个优化。实际上，这是一种经常采用的形式。因为计算这个等式要比一 个一个地比较类中的域所付出的代价小得多。

3. 检测 otherObject 是否为 null, 如 果 为 null, 返 回 false。这项检测是很必要的。

```java
if (otherObject = null) {
	return false;
}
```

4. 比较 this 与 otherObject 是否属于同一个类。如果 equals 的语义在每个子类中有所改 变，就使用 getClass 检测：

```java
if (getClass() != otherObject.getCIass()) {
	return false;
}
```

### 如果所有的子类都拥有统一的语义，就使用 instanceof 检测：

```java
if (!(otherObject instanceof ClassName)) {
	return false;
}
```

5. 将 otherObject 转换为相应的类类型变量：

```java
ClassName other = (ClassName)otherObject
```

6. 现在开始对所有需要比较的域进行比较了。使用 == 比较基本类型域，使用 equals 比较对象域。如果所有的域都匹配， 就返回 true; 否则返回 false。

```java
return field1 == other.field1 && Objects.equa1s(fie1d2, other.field2) && ...
```

### 如果在子类中重新定义 equals, 就要在其中包含调用 super.equals(other) 。

###  -> P169

### 125. 下面是实现 equals 方法的一种常见的错误。 可以找到其中的问题吗？

```java
public class Employee {
public boolean equals(Employee other) {
	return other != null
		&& getClassO == other.getClass0
		&& Objects.equals(name , other.name)
		&& salary == other,sal ary
		&& Objects.equals(hireDay, other.hireDay);
	}
}
```

### 这个方法声明的显式参数类型是 Employee。其结果并没有覆盖 Object 类的 equals 方 法， 而是定义了一个完全无关的方法。

### 为了避免发生类型错误， 可以使用 @Override 对覆盖超类的方法进行标记：

```java
@Override public boolean equals(Object other)
```

### 如果出现了错误， 并且正在定义一个新方法， 编译器就会给出错误报告。例如， 假 设将下面的声明添加到 Employee 类中：

```java
@Override public boolean equals(Employee other)
```

### 就会看到一个错误报告， 这是因为这个方法并没有覆盖超类 Object 中的任何方法。

### -> P170

## 5.2.3 hashCode 方法

### 126. 由于 hashCode方法定义在 Object 类中， 因此每个对象都有一个默认的散列码，其值为 对象的存储地址。来看下面这个例子。

```java
String s = "Ok";
StringBuilder sb = new StringBuilder(s);
System.out.println(s.hashCode() + " " + sb.hashCode());
String t = new String("Ok");
StringBuilder tb = new StringBuilder⑴；
System.out.pri ntl n(t.hashCode() + " "
+ tb.hashCode());
```

### 表 5-2 列出了结果。

<img src="F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）散列码.png" alt="Java核心技术（卷一）散列码"  />

### 请注意， 字符串 s 与 t 拥有相同的散列码， 这是因为字符串的散列码是由内容导出 的。而字符串缓冲 sb 与 tb却有着不同的散列码， 这是因为在 StringBuffer 类中没有定义 hashCode 方法，它的散列码是由 Object 类的默认 hashCode 方法导出的对象存储地址。

### -> P171

### 127. 如果重新定义 equals方法，就必须重新定义 hashCode 方法， 以便用户可以将对象插人 到散列表中（有关散列表的内容将在第 9 章中讨论)。 -> P171

### 128. hashCode 方法应该返回一个整型数值（也可以是负数，) 并合理地组合实例域的散列码, 以便能够让各个不同的对象产生的散列码更加均匀。

### 例如， 下面是 Employee 类的 hashCode 方法。

```java
public class Employee {
	public int hashCode() {
		return 7 * name.hashCode0
			+ 11 * new Double(salary).hashCode()
			+ 13 * hireDay.hashCode();
	}
	...
}
```

### 不过，还可以做得更好。首先， 最好使用 null 安全的方法 Objects.hashCode。 如果其参 数为 null，这个方法会返回 0, 否则返回对参数调用 hashCode 的结果。

### -> P171

### 129. 另外，使用静态方法 Double.hashCode 来避免创建 Double 对象：

```java
public int hashCode() {
	return 7 * Objects.hashCode(name)
		+ 11 * Double.hashCode(salary)
		+ 13 * Objects.hashCode(hireDay);
}
```

### 还有更好的做法，需要组合多个散列值时，可以调用 ObjeCtS.hash 并提供多个参数。这 个方法会对各个参数调用 Objects.hashCode， 并组合这些散列值。这样 Employee.hashCode 方 法可以简单地写为：

```java
public int hashCode() {
	return Objects,hash(name, salary, hireDay);
}
```

### Equals 与 hashCode 的定义必须一致：如果 x.equals(y) 返回 true, 那么 x.hashCode( ) 就必 须与 y.hashCode( ) 具有相同的值。例如， 如果用定义的 Employee.equals 比较雇员的 ID，那 么 hashCode 方法就需要散列 ID，而不是雇员的姓名或存储地址。

### -> P172

### 130. 如果存在数组类型的域， 那么可以使用静态的 Arrays.hashCode 方法计算一个散列 ? ， 这个散列码由数组元素的散列码组成。 -> P172

## 5.2.4 toString 方法

### 131. 绝大多数（但不是全部）的 toString方法都遵循这样的格式：类的名字，随后是一对方括号括起来的域值。

### 下面是 Employee 类中的 toString 方法的实现：

```java
public String toString() {
	return "Employee[name=" + name
		+ ",salary=" + salary
		+ ",hireDay=" + hireDay
		+ "]";
}
```

### 实际上，还可以设计得更好一些。最好通过调用 getClaSS( ).getName( ) 获得类名的字符 串，而不要将类名硬加到 toString方法中。

```java
public String toString() {
	return getClass().getName()
		+ "[name=" + name
		+ ",salary=" + salary
		+ ",hireDay=" + hireDay
		+ "]";
}
```

### -> P173

---

### 132. 随处可见 toString方法的主要原因是：只要对象与一个字符串通过操作符“ +” 连接起 来，Java 编译就会自动地调用 toString方法，以便获得这个对象的字符串描述。例如，

```java
Point p = new Point(10, 20);
String message = "The current position is " + p;
	// automatically invokes p.toString()
```

### -> P173

---

### 133. Object 类定义了 toString 方法， 用来打印输出对象所属的类名和散列码。

### 例如， 调用

```java
System.out.println(System.out)
```

### 将输出下列内容：

```java
java.io.PrintStream@2f6684
```

### 之所以得到这样的结果是因为 PrintStream 类的设计者没有覆盖 toString方法。

### -> P174

### 134. 令人烦恼的是， 数组继承了 object 类的 toString 方法，数组类型将按照旧的格式 打印。例如：

```java
int[] luckyNumbers = { 2, 3, 5, 7, 11, 13 } ;
String s = "" + luckyNumbers;
```

### 生成字符串“ [I@la46e30” （前缀 [I 表明是一个整型数组）。

### 修正的方式是调用静态 方法 Arrays.toString。代码：

```java
String s = Arrays.toString(luckyNumbers);
```

### 将生成字符串“ [2, 3, 5, 7, 11, 13]”。

### 要想打印多维数组（即， 数组的数组）则需要调用 Arrays.deepToString 方法。

### -> P174

### 135. toString方法是一种非常有用的调试工具。在标准类库中，许多类都定义了 toString方 法， 以便用户能够获得一些有关对象状态的必要信息。像下面这样显示调试信息非常有益：

```java
System.out.println("Current position = " + position);
```

### 读者在第 7 章中将可以看到，更好的解决方法是：

```java
Logger.global.info("Current position = " + position);
```

### -> P174

---

### 136. 强烈建议为自定义的每一个类增加 toString 方法。这样做不仅自己受益， 而且所 有使用这个类的程序员也会从这个日志记录支持中受益匪浅。 -> P174

## 5.3 泛型数组列表

### 137. 下面声明和构造一个保存 Employee 对象的数组列表：

```java
ArrayList<Employee> staff = new ArrayList<Eniployee>();
```

### 两边都使用类型参数 Employee， 这有些繁琐。Java SE 7中， 可以省去右边的类型参数：

```java
ArrayList<Employee> staff = new ArrayList<>()；
```

### 这被称为“ 菱形” 语法，因为空尖括号 o就像是一个菱形。可以结合 new 操作符使用菱形 语法。编译器会检查新值是什么。如果赋值给一个变量，或传递到某个方法，或者从某个方 法返回，编译器会检査这个变量、 参数或方法的泛型类型，然后将这个类型放在o中。在 这个例子中，new ArrayListo()将赋至一个类型为 ArrayList 的变量， 所以泛型 类型为 Employee。

### -> P178

### 138. ：Java SE 5.0 以前的版本没有提供泛型类， 而是有一个 ArrayList 类， 其中保存类型 为 Object 的元素， 它是“ 自适应大小” 的集合。如果一定要使用老版本的 Java, 则需要 将所有的后缀 <. . .> 删掉，, 在 Java SE 5.0 以后的版本中， 没有后缀 <. . .> 仍然可以使用 ArrayList, 它将被认为是一个删去了类型参數的“ 原始” 类型、 -> P178

### 139. 在 Java 的老版本中， 程序员使用 Vector 类实现动态数组。 不过， ArrayList 类更加 有效，没有任何理由一定要使用 Vector 类。 -> P178

### 140. 如果已经清楚或能够估计出数组可能存储的元素数量， 就可以在填充数组之前调用 ensureCapacity方法：

```java
staff.ensureCapacity(100);
```

### 这个方法调用将分配一个包含 100 个对象的内部数组。然后调用 100 次 add, 而不用重新分 配空间。

### 另外，还可以把初始容量传递给 ArrayList 构造器：

```java
ArrayList<Employee> staff = new ArrayList<>(100);
```

### -> P179

---

### 141. 一旦能够确认数组列表的大小不再发生变化，就可以调用 trimToSize方法。这个方法将存储区域的大小调整为当前元素数量所需要的存储空间数目。垃圾回收器将回收多余的存储空间。

### 一旦整理了数组列表的大小，添加新元素就需要花时间再次移动存储块，所以应该在确 认不会添加任何元素时， 再调用 trimToSize。 -> P179

### 142. ArrayList 类似于 C++ 的 vector 模板。ArrayList 与 vector 都是泛型类型。 但 是 C++ 的 vector 模板为了便于访问元素重栽了 [ ] 运算符。由于 Java 没有运算符重栽， 所以必须调用显式的方法。此外，C++ 向量是值拷贝。如果 a 和 b 是两个向量， 賦值 操作 a = b 将会构造一个与 b 长度相同的新向量 a, 并将所有的元素由 b 拷贝到 a, 而在 Java 中， 这条赋值语句的操作结果是让 a 和 b 引用同一个数组列表。-> P179

## 5.3.1 访问数组列表元素

### 143. 使用 get 和 set 方法实现访问或改变数组元素的操作，而不使用人们喜爱的 [ ] 语法格式。

### 例如，要设置第 i 个元素，可以使用：

```java
staff.set(i, harry):
```

### 它等价于对数组 a 的元素赋值（数组的下标从 0开始)：

```java
a[i] = harry;
```

### 144. 只有 i 小于或等于数组列表的大小时， 才能够调用 list.set(，i x。) 例如， 下面这段代 码是错误的：

```java
ArrayList<Employee> list = new ArrayList<>(100); // capacity 100，size 0
list.set(0, x); // no element 0 yet
```

### 使用 add 方法为数组添加新元素， 而不要使用 set 方法， 它只能替换数组中已经存在 的元素内容。

### 使用下列格式获得数组列表的元素:

```java
Employee e = staff.get(i);
```

### 等价于：

```java
Employee e = a[i];
```

### -> P180

### 145. 下面这个技巧可以一举两得， 既可以灵活地扩展数组， 又可以方便地访问数组元素。首 先，创建一个数组， 并添加所有的元素。

```java
ArrayList<X> list = new ArrayList<>();
while (. . .) {
	x = . . .;
	list.add(x);
}
```

### 执行完上述操作后，使用 toArray 方法将数组元素拷贝到一个数组中。

```java
X[] a = new X[list.size()];
list.toArray(a);
```

### 除了在数组列表的尾部追加元素之外，还可以在数组列表的中间插入元素，使用带索引 参数的 add 方法。

```java
int n = staff.size() / 2;
staff.add(n, e);
```

### 为了插人一个新元素，位于 n之后的所有元素都要向后移动一个位置。如果插人新元素 后， 数组列表的大小超过了容量， 数组列表就会被重新分配存储空间。

### 同样地，可以从数组列表中间删除一个元素。

```java
Employee e = staff.remove(n);
```

### 位于这个位置之后的所有元素都向前移动一个位置， 并且数组的大小减 1。

### 对数组实施插人和删除元素的操作其效率比较低。对于小型数组来说，这一点不必担 心。但如果数组存储的元素数比较多， 又经常需要在中间位置插入、删除元素， 就应该考虑 使用链表了。有关链表操作的实现方式将在第 9 章中讲述。

### 可以使用“ foreach” 循环遍历数组列表：

```java
for (Employee e : staff) {
	do something with e
}
```

### 这个循环和下列代码具有相同的效果

```java
for (int i = 0; i < staff .size(); i ++) {
	Employee e = staff.get(i);
	do something with e
}
```

### 程序清单 5-11 是对第 4 章中 EmployeeTest 做出修改后的程序。在这里， 将 Employee[ ] 数组替换成了 ArrayList 。请注意下面的变化：

- 不必指出数组的大小。
- 使用 add 将任意多的元素添加到数组中。
- 使用 size() 替代 length 计算元素的数目。
- 使用 a.get(i) 替代 a[i] 访问元素。

### -> P181

## 5.3.2 类型化与原始数组列表的兼容性

### 146. 一旦能确保不会造成严重的后果，可以用@SuppressWamings("unchecked") 标注来标记 这个变量能够接受类型转换， 如下所示：

```java
@SuppressWarnings("unchecked") ArrayList<Employee> result =
(ArrayList<Employee>) employeeDB.find(query); // yields another warning
```

### -> P184

---

## 5.4 对象包装器与自动装箱

### 147. 有时， 需要将 int 这样的基本类型转换为对象。 所有的基本类型都冇一个与之对应的类。 例如，Integer 类对应基本类型 int。通常， 这些类称为包装器 （ wrapper ) 这些对象包装器类 拥有很明显的名字：Integer、Long、Float、Double、Short、Byte、Character 、Void 和 Boolean (前 6 个类派生于公共的超类 Number)。对象包装器类是不可变的，即一旦构造了包装器，就不 允许更改包装在其中的值。同时， 对象包装器类还是 final , 因此不能定义它们的子类。 -> P184

### 148. 假设想定义一个整型数组列表。而尖括号中的类型参数不允许是基本类型，也就是说， 不允许写成 ArrayList。这里就用到了 Integer 对象包装器类。我们可以声明一个 Integer 对象的数组列表。

```java
ArrayList<Integer> list = new ArrayList<>()；
```

### -> P184

---

### 149. 由于每个值分别包装在对象中， 所以 ArrayList 的效率远远低于 int[ ] 数 组。 因此， 应该用它构造小型集合，其原因是此时程序员操作的方便性要比执行效率更加重要。

### 150. 幸运的是， 有一个很有用的特性， 从而更加便于添加 int 类型的元素到 ArrayLisKlntegeP 中。下面这个调用

```java
list.add(3);
```

### 将自动地变换成

```java
list.add(Integer.value0f(3));
```

### 这种变换被称为自动装箱（autoboxing)。

### -> P184

### 151. 相反地， 当将一个 Integer 对象赋给一个 int 值时， 将会自动地拆箱。也就是说， 编译器 将下列语句：

```java
int n = list.get(i);
```

### 翻译成

```java
int n = list.get(i).intValue();
```

### 甚至在算术表达式中也能够自动地装箱和拆箱。例如，可以将自增操作符应用于一个包装器 引用：

```java
Integer n = 3;
n++;
```

### 编译器将自动地插人一条对象拆箱的指令， 然后进行自增计算， 最后再将结果装箱。

### -> P185

### 152. 大多数情况下，容易有一种假象， 即基本类型与它们的对象包装器是一样的，只是它们 的相等性不同。大家知道， == 运算符也可以应用于对象包装器对象， 只不过检测的是对象是 否指向同一个存储区域， 因此，下面的比较通常不会成立：

```java
Integer a = 1000;
Integer b = 1000;
if (a == b) . . .
```

### 然而，Java 实现却有可能（ may) 让它成立。如果将经常出现的值包装到同一个对象中， 这种比较就有可能成立。这种不确定的结果并不是我们所希望的。解决这个问题的办法是在 两个包装器对象比较时调用 equals 方法。

### -> P185

### 153. 自动装箱规范要求 boolean、byte、char 127， 介于 -128 ~ 127 之间的 short 和 int 被包装到固定的对象中。例如，如果在前面的例子中将 a 和 b 初始化为 100，对它们进行比较的结果一定成立。 -> P185

### 154. 关于自动装箱还有几点需要说明。

1. 首先， 由于包装器类引用可以为 null, 所以自动装箱 有可能会抛出一个 NullPointerException 异常：

```java
Integer n = null;
System.out.println(2 * n); // Throws NullPointerException
```

2. 另外， 如果在一个条件表达式中混合使用 Integer 和 Double 类型， Integer 值就会拆箱， 提升为 double, 再装箱为 Double:

```java
Integer n = 1;
Double x = 2.0;
System.out.println(true ? n : x); // Prints 1.0
```

3. 最后强调一下，装箱和拆箱是编译器认可的，而不是虚拟机。编译器在生成类的字节码 时， 插人必要的方法调用。虚拟机只是执行这些字节码。

### -> P185

### 155. 使用数值对象包装器还有另外一个好处。Java 设计者发现，可以将某些基本方法放置在包装器中， 例如， 将一个数字字符串转换成数值。

### 要想将字符串转换成整型， 可以使用下面这条语句：

```java
int x = Integer.parselnt(s);
```

### 这里与 Integer 对象没有任何关系， parselnt 是一个静态方法。但 Integer 类是放置这个方法的一个好地方。

### -> P186

### 156. 有些人认为包装器类可以用来实现修改数值参数的方法， 然而这是错误的。在第 4 章中曾经讲到， 由于 Java 方法都是值传递， 所以不可能编写一个下面这样的能够增加 整型参数值的 Java 方法。

```java
public static void triple(int x) // won't work
{
	x = 3 * x; // modifies local variable
}
```

### 将 int 替换成 Integer 又会怎样呢？

```java
public static void triple(Integer x) // won 't work
{
	. . .
}
```

### 问题是 Integer 对象是不可变的： 包含在包装器中的内容不会改变: 不能使用这些包 装器类创建修改数值参数的方法。

### 如果想编写一个修改数值参数值的方法， 就需要使用在 org.omg.CORBA 包中定义的 持有者（ holder) 类型， 包括 IntHolder、BooleanHolder 等。每个持有者类型都包含'一个 公有 （！）域值，通过它可以访问存储在其中的值。

```java
public static void triple(IntHolder x)
{
	x.value = 3 * x.value;
}
```

### -> P186

---

## 5.5 参数数量可变的方法

### 157. printf方法是这样定义的：

```java
public class PrintStream
{
	public PrintStream printf(String fmt , Object... args) { return format(fmt, args); }
}
```

### 这里的省略号 . . . 是 Java 代码的一部分，它表明这个方法可以接收任意数量的对象（除 fmt 参数之外)。

### 实际上，printf方法接收两个参数，一个是格式字符串， 另一个是 Object ] 数组， 其中 保存着所有的参数（如果调用者提供的是整型数组或者其他基本类型的值， 自动装箱功能 将把它们转换成对象 )。现在将扫描 Ant 字符串， 并将第 i 个格式说明符与 args[i] 的值匹配起来。

### 换句话说，对于 printf 的实现者来说，Object… 参数类型与 Object[ ]完全一样。

### 编译器需要对 printf 的每次调用进行转换， 以便将参数绑定到数组上，并在必要的时候 进行自动装箱：

```java
System.out.printf("%d %s", new Object[] { new Integer(n), "widgets" } );
```

### -> P188

---

### 158. 允许将一个数组传递给可变参数方法的最后一个参数。 例如：

```java
System.out.printf("%d %s", new Object[] { new Integer(1), "widgets" } );
```

### 因此， 可以将已经存在且最后一个参数是数组的方法重新定义为可变参数的方法， 而不会破坏任何已经存在的代码。例如， MessageFormat.format 在 Java SE 5.0 就采用了 这种方式。甚至可以将 main 方法声明为下列形式：

```java
public static void main(String... args)
```

### -> P188

---

## 5.6 枚举类

### 159. 读者在第 3 章已经看到如何定义枚举类型。下面是一个典型的例子：

```java
public enum Size { SMALL , MEDIUM, LARGE, EXTRA_LARGE };
```

### 实际上， 这个声明定义的类型是一个类， 它刚好有 4 个实例， 在此尽量不要构造新对象。

### 因此， 在比较两个枚举类型的值时， 永远不需要调用 equals, 而直接使用“ == ” 就 可以了。

### 如果需要的话， 可以在枚举类型中添加一些构造器、 方法和域。当然，构造器只是在构 造枚举常量的时候被调用。下面是一个示例：

```java
public enum Size
{
SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");
private String abbreviation;
private Size(String abbreviation) { this.abbreviation = abbreviation; }
public String getAbbreviation() { return abbreviation; }
}
```

### -> P188

---

### 160.  所有的枚举类型都是 Enum 类的子类。它们继承了这个类的许多方法。其中最有用的一 个是 toString， 这个方法能够返回枚举常量名。例如， Size.SMALL.toString( ) 将返回字符串 “ SMALL”。

### toString 的逆方法是静态方法 valueOf。例如， 语句：

```java
Size s = Enum.valueOf(Size.class, "SMALL");
```

### 将 s 设置成 Size.SMALL。

### -> P188

### 161. 每个枚举类型都有一个静态的 values 方法， 它将返回一个包含全部枚举值的数组。 例 如，如下调用

```java
Size[] values = Size.values();
```

### -> P189

---

### 162. 如同 Class 类一样， 鉴于简化的考虑， Enum 类省略了一个类型参数。 例如， 实 际上， 应该将枚举类型 Size 扩展为 Enum<Size> 。 类型参数在 compareTo 方法中使用 ( comPareTo 方法在第 6 章中介绍， 类型参数在第 8 章中介绍）。 -> P189

## 5.7 反射

### 163. 反射库（ reflection library) 提供了一个非常丰富且精心设计的工具集， 以便编写能够动 态操纵 Java 代码的程序。这项功能被大量地应用于 JavaBeans 中， 它是 Java组件的体系结构 (有关 JavaBeans 的详细内容在卷 II 中阐述)。使用反射， Java 可以支持 Visual Basic 用户习惯 使用的工具。特别是在设计或运行中添加新类时， 能够快速地应用开发工具动态地查询新添加类的能力。 -> P190

### 164. 能够分析类能力的程序称为反射（reflective )。反射机制的功能极其强大，在下面可以看 到， 反射机制可以用来：

- 在运行时分析类的能力。
- 在运行时查看对象， 例如， 编写一个 toString 方法供所有类使用。
- 实现通用的数组操作代码。
- 利用 Method 对象， 这个对象很像中的函数指针。

### -> P190

### 165. 反射是一种功能强大且复杂的机制。 使用它的主要人员是工具构造者，而不是应用程序 员P 如果仅对设计应用程序感兴趣， 而对构造工具不感兴趣， 可以跳过本章的剩余部分， 稍 后再返回来学习。 -> P190

## 5.7.1 Class 类

### 166. 在程序运行期间，Java 运行时系统始终为所有的对象维护一个被称为运行时的类型标识。 这个信息跟踪着每个对象所属的类。 虚拟机利用运行时类型信息选择相应的方法执行。 

### 然而， 可以通过专门的 Java 类访问这些信息。保存这些信息的类被称为 Class, 这 个 名 字很容易让人混淆。Object 类中的 getClass( ) 方法将会返回一个 Class 类型的实例。

```java
Employee e;
. . .
Class cl = e.getClass();
```

### 如同用一个 Employee 对象表示一个特定的雇员属性一样， 一个 Class 对象将表示一个特 定类的属性。最常用的 Class 方法是 getName。 这个方法将返回类的名字。例如，下面这条 语句：

```java
System.out.println(e.getClass().getName() + " " + e.getName());
```

### 如果 e 是一个雇员，则会打印输出：

```java
Employee Harry Hacker
```

### 如果 e 是经理， 则会打印输出：

```java
Manager Harry Hacker
```

### -> P191

---

### 167. 如果类在一个包里，包的名字也作为类名的一部分：

```java
Random generator = new Random():
Class cl = generator.getClass();
String name = cl .getName(); // name is set to "java.util.Random"
```

### 还可以调用静态方法 forName 获得类名对应的 Class 对象。

```java
String className = "java.util.Random";
Class cl = Class.forName(className);
```

### 如果类名保存在字符串中， 并可在运行中改变， 就可以使用这个方法。当然， 这个方法 只有在 dassName 是类名或接口名时才能够执行。否则，forName 方法将抛出一个 checked exception ( 已检查异常）。无论何时使用这个方法， 都应该提供一个异常处理器（ exception handler) o 如何提供一个异常处理器，请参看下一节。

### -> P191

### 168. 在启动时， 包含 main 方法的类被加载。它会加载所有需要的类。这些被加栽的类 又要加载它们需要的类， 以此类推。对于一个大型的应用程序来说， 这将会消耗很多时 间， 用户会因此感到不耐烦。可以使用下面这个技巧给用户一种启动速度比较快的幻觉。 不过，要确保包含 main 方法的类没有显式地引用其他的类。首先，显示一个启动画面； 然后，通过调用 Class.forName 手工地加载其他的类。 -> P191

### 169. 获得 Class类对象的第三种方法非常简单。如果 T 是任意的 Java 类型（或 void 关键字，) T.class 将代表匹配的类对象。例如：

```java
Class cl1 = Randomclass; // if you import java.util.*;
Class cl2 = int.class;
Class cl3 = Double[].class;
```

### 请注意，一个 Class 对象实际上表示的是一个类型，而这个类型未必一定是一种类。例如， int 不是类， 但 int.class 是一个 Class 类型的对象。

### -> P191

### 170. Class 类实际上是一个泛型类。例如， Employee.class 的类型是 Class 。 没有说明这个问题的原因是： 它将已经抽象的概念更加复杂化了。在大多数实际问题 中， 可以忽略类型参数， 而使用原始的 Class 类。有关这个问题更详细的论述请参看第 8 章。 -> P191

### 171. 鉴于历史原 getName 方法在应用于数组类型的时候会返回一个很奇怪的名字：

- Double[ ].class.getName( ) 返回“ [Ljava.lang.Double;’’。
- •int[ ].class.getName( ) 返回“ [I ”。

### 172. 虚拟机为每个类型管理一个 Class 对象。 因此，可以利用 =运算符实现两个类对象比较 的操作。 例如，

```java
if (e.getClass() == Employee.class) . . .
```

### 还有一个很有用的方法 newlnstance( )， 可以用来动态地创建一个类的实例例如，

```java
e.getClass().newlnstance();
```

### 创建了一个与 e 具有相同类类型的实例。 newlnstance方法调用默认的构造器（没有参数的构 造器）初始化新创建的对象。如果这个类没有默认的构造器， 就会抛出一个异常。

### 将 forName 与 newlnstance 配合起来使用， 可以根据存储在字符串中的类名创建一个对象。

```java
String s = "java.util.Random";
Object m = Class.forName(s).newlnstance();
```

### 如果需要以这种方式向希望按名称创建的类的构造器提供参数， 就不要使用上面 那条语句， 而必须使用 Constructor 类中的 newlnstance 方法。

### -> P192

### 173. newlnstance 方法对应 C++ 中虚拟构造器的习惯用法。 然而，C++ 中的虚拟 构造器不是一种语言特性， 需要由专门的库支持。 Class 类与 C++ 中的 type_info 类相似， getClass 方法与 C++ 中的 typeid 运算符等价。 但 Java 中的 Class 比 C++ 中的 type_info 的功能强。C++ 中的 type_info 只能以字符串的形式显示一个类型的名字， 而不能创建那 个类型的对象。 -> P192

## 5.7.2 捕获异常

### 174. 当程序运行过程中发生错误时，就会“ 抛出异常' 抛出异常比终止程序要灵活得多， 这是因为可以提供一个“ 捕获” 异常的处理器 （handler) 对异常情况进行处理。 -> P192

### 175. 异常有两种类型： 未检查异常和已检查异常。 对于已检查异常， 编译器将会检查是否提 供了处理器。 然而，有很多常见的异常， 例如，访问 null 引用， 都属于未检查异常。编译 器不会査看是否为这些错误提供了处理器。毕竟，应该精心地编写代码来避免这些错误的发 生， 而不要将精力花在编写异常处理器上。 -> P193

### 176. 对于已检查异常，只需要提供一个异常处理器。 可以很容易地发现会抛出已检査异常的 方法。如果调用了一个抛出已检查异常的方法，而又没有提供处理器，编译器就会给出错误报告。 -> P193

## 5.7.3 利用反射分析类的能力

### 177. 下面简要地介绍一下反射机制最重要的内容—检查类的结构。

### 在 java.lang.reflect 包中有三个类 Field、 Method 和 Constructor 分别用于描述类的域、 方 法和构造器。 这三个类都有一个叫做 getName 的方法， 用来返回项目的名称。Held 类有一 个 getType 方法， 用来返回描述域所属类型的 Class 对象。Method 和 Constructor 类有能够 报告参数类型的方法，Method 类还有一个可以报告返回类型的方法。这 <个类还有一个叫 做 getModifiers 的方法， 它将返回一个整型数值，用不同的位开关描述 public 和 static 这样 的修饰符使用状况。另外， 还可以利用java.lang.refleCt 包中的 Modifiei•类的静态方法分析 getModifiers 返回的整型数值。例如， 可以使用 Modifier 类中的 isPublic、 isPrivate 或 isFinal 判断方法或构造器是否是 public、 private 或 final。 我们需要做的全部工作就是调用 Modifier 类的相应方法，并对返回的整型数值进行分析，另外，还可以利用 Modifier.toString方法将 修饰符打印出来。 -> P194

### 178. Class类中的 getFields、 getMethods 和 getConstructors 方 法 将 分 别 返 回 类 提 供 的 public 域、 方法和构造器数组， 其中包括超类的公有成员。Class 类的 getDeclareFields、 getDeclareMethods 和 getDeclaredConstructors 方法将分别返回类中声明的全部域、 方法和构 造器， 其中包括私有和受保护成员，但不包括超类的成员。 -> P194

### 179. 值得注意的是：这个程序可以分析 Java 解释器能够加载的任何类， 而不仅仅是编译程序 时可以使用的类。在下一章中， 还将使用这个程序查看 Java 编译器自动生成的内部类。 -> P195

## 5.7.4 在运行时使用反射分析对象

### 180. 从前面一节中， 已经知道如何查看任意对象的数据域名称和类型:

- 获得对应的 Class 对象。
- 通过 Class 对象调用 getDeclaredFields。

### -> P199

### 181. 本节将进一步查看数据域的实际内容。当然， 在编写程序时， 如果知道想要査看的域名 和类型，查看指定的域是一件很容易的事情。而利用反射机制可以查看在编译时还不清楚的 对象域。 -> P199

### 182. 查看对象域的关键方法是 Field类中的 get 方法。如果 f 是一个 Field 类型的对象（例如， 通过 getDeclaredFields 得到的对象，) obj 是某个包含 f 域的类的对象，f.get(obj) 将返回一个 对象，其值为 obj 域的当前值。这样说起来显得有点抽象，这里看一看下面这个示例的运行。

```java
Employee harry = new Employee("Harry Hacker", 35000, 10, 1, 1989);
Class cl = harry.getClass()；
// the class object representing Employee
Field f = cl .getDeclaredField("name"):
// the name field of the Employee class
Object v = f.get(harry);
// the value of the name field of the harry object , i.e., the String object "Harry Hacker"
```

### 实际上，这段代码存在一个问题。由于 name 是一个私有域， 所以 get 方法将会抛出一个 IllegalAccessException。只有利用 get 方法才能得到可访问域的值。除非拥有访问权限，否则 Java 安全机制只允许査看任意对象有哪些域， 而不允许读取它们的值。

### 反射机制的默认行为受限于 Java 的访问控制。然而， 如果一个 Java 程序没有受到安 全管理器的控制， 就可以覆盖访问控制。 为了达到这个目的， 需要调用 Field、 Method 或 Constructor 对象的 setAccessible 方法。例如，

```java
f.setAtcessible(true); // now OK to call f.get(harry);
```

### setAccessible 方法是 AccessibleObject 类中的一个方法， 它是 Field、 Method 和 Constructor 类的公共超类。这个特性是为调试、 持久存储和相似机制提供的。本书稍后将利用它编写一 个通用的 toString方法。

### -> P199

### 183. get 方法还有一个需要解决的问题。name 域是一个 String, 因此把它作为 Object 返回 没有什么问题。但是， 假定我们想要查看 salary 域。它属于 double 类型，而 Java中数值类 型不是对象。要想解决这个问题， 可以使用 Field 类中的 getDouble 方法，也可以调用 get 方法，此时， 反射机制将会自动地将这个域值打包到相应的对象包装器中，这里将打包成 Double。

### 当然，可以获得就可以设置。 调用 f.set(obj，value) 可以将 obj 对象的 f 域设置成新值。

### -> P199

### 184. 泛型 toString方法需要解释几个复杂的问题。循环引用将有可能导致无限递归。因此， ObjectAnalyzer 将记录已经被访问过的对象。 另外， 为了能够査看数组内部， 需要采用一种 不同的方式。有关这种方式的具体内容将在下一节中详细论述。 -> P199

### 185. 可以使用 toString 方法查看任意对象的内部信息。例如， 下面这个调用：

```java
ArrayList<Integer> squares = new ArrayList<>();
for (int i = 1; i <= 5; i++) squares.add(i * i);
System.out.println(new ObjectAnalyzer().toString(squares));
```

### 将会产生下时的打印结果：

```java
java.util.ArrayList[elementData=class java.lang.Object[]{java.lang.Integer[value=l][][],
java.lang.Integer[value=4][][],java.lang.Integer[value=9][][],java.lang.Integer[value=16][][],
java.lang.Integer[value=25][][],null,null,null,null,null},size=5][modCount=5][][]

```

### 还可以使用通用的 toString 方法实现 ft 己类中的 toString 方法， 如下所示：

```java
public String toString()
{
return new ObjectAnalyzer().toString(this);
}
```

### 这是一种公认的提供 toString 方法的手段， 在编写程序时会发现， 它是非常有用的。

### -> P200

## 5.7.5 使用反射编写泛型数组代码

### 186. java.lang.reflect 包中的 Array 类允许动态地创建数组。例如， 将这个特性应用到 Array 类中的 copyOf方法实现中， 应该记得这个方法可以用于扩展已经填满的数组。

```java
Employee[] a = new Employee[100]:
. . .
// array is full
a = Arrays.copyOf(a, 2 * a.length);
```

### 如何编写这样一个通用的方法呢？ 正好能够将 Employee[ ] 数组转换为 Object[ ] 数组， 这让人感觉很有希望。下面进行第一次尝试。

```java
public static Object[] badCopyOf(Object[] a, int newLength) // not useful
{
	Object[] newArray = new Object[newlength]:
	System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
	return newArray;
}
```

### 然而， 在实际使用结果数组时会遇到一个问题。这段代码返回的数组类型是对象数组 (Object[]) 类型，这是由于使用下面这行代码创建的数组：

```java
new Object[newLength]
```

### 一个对象数组不能转换成雇员数组（ Employee[ ] ) 。如果这样做， 则在运行时 Java 将会 产生 ClassCastException 异常。前面已经看到，Java 数组会记住每个元素的类型， 即创建数 组时 new 表达式中使用的元素类型。将一个 Employee[ ] 临时地转换成 Object[ ] 数组， 然后 再把它转换回来是可以的，但一 从开始就是 Object[ ] 的数组却永远不能转换成 Employe[ ]数组。 为了编写这类通用的数组代码， 需要能够创建与原数组类型相同的新数组。为此， 需要 java, lang.reflect 包中 Array 类的一些方法。其中最关键的是 Array类中的静态方法 newlnstance, 它能够构造新数组。在调用它时必须提供两个参数，一个是数组的元素类型，一个是数组的长度。

```java
Object newArray = Array.newlnstance(componentType, newLength);
```

### 为了能够实际地运行，需要获得新数组的长度和元素类型。

### 可以通过调用 Array.getLength(a) 获得数组的长度， 也可以通过 Array 类的静态 getLength 方法的返回值得到任意数组的长度。而要获得新数组元素类型，就需要进行以下工作：

1. 首先获得 a 数组的类对象。
2. 确认它是一个数组。
3. 使用 Class 类（只能定义表示数组的类对象）的 getComponentType 方法确定数组对应 的类型。

### 为什么 getLength 是 Array 的方法，而 getComponentType 是 Class 的方法呢？ 我们也不 清楚。反射方法的分类有时确实显得有点古怪。下面是这段代码：

```java
public static Object goodCopyOf(Object a, int newLength)
{
	Class cl = a.getClass()；
	if (!cl.isArray()) return null;
	Class componentType = cl .getComponentType()；
	int length = Array.getLength(a);
	Object newArray = Array.newlnstance(componentType, newLength):
	System.arraycopy(a, 0, newArray, 0, Math.min(length, newLength));
	return newArray;
}
```

### 请注意，这个 CopyOf 方法可以用来扩展任意类型的数组， 而不仅是对象数组。

```java
int[] a = { 1, 2, 3, 4, 5 };
a = (int[])goodCopyOf(a, 10);
```

### 为了能够实现上述操作，应该将 goodCopyOf 的参数声明为 Object 类型，而不要声明为对象型数组（Object[])。整型数组类型 int[] 可以被转换成 Object，但不能转换成对象数组。

### -> P203

## 5.7.6 调用任意方法

### 187. 在 C 和 C++ 中， 可以从函数指针执行任意函数。从表面上看， Java 没有提供方法指针， 即将一个方法的存储地址传给另外一个方法， 以便第二个方法能够随后调用它。事实上， Java 的设计者曾说过：方法指针是很危险的，并且常常会带来隐患。他们认为 Java 提供的 接口（interface ) (将在下一章讨论）是一种更好的解决方案。然而， 反射机制允许你调用任意 方法。 -> P205

### 188. 微软公司为自己的非标准 Java 语 言 ( 以 及 后 来 的 C#) 增加了另一种被称为委 托（ delegate ) 的方法指针类型， 它与本节讨论的 Method 类不同。然而， 在下一章中讨 论的内部类比委托更加有用。 -> P205

### 189. 为了能够看到方法指针的工作过程， 先回忆一下利用 Field 类的 get 方法查看对象域的过 程。与之类似， 在 Method 类中有一个 invoke 方法， 它允许调用包装在当前 Method 对象中 的方法。invoke 方法的签名是：

```java
Object invoke(Object obj, Object... args)
```

### 第一个参数是隐式参数， 其余的对象提供了显式参数（在 Java SE 5.0 以前的版本中，必须传递一个对象数组， 如果没有显式参数就传递一个 null )。

### 对于静态方法，第一个参数可以被忽略，即可以将它设置为 null。

### 例如， 假设用 ml 代表 Employee 类的 getName 方法，下面这条语句显示了如何调用这个 方法：

```java
String n = (String)m1.invoke(harry);
```

### 如果返回类型是基本类型， invoke 方法会返回其包装器类型。 例如， 假设 m2 表示 Employee 类的 getSalary 方法， 那么返回的对象实际上是一个 Double, 必须相应地完成类型 转换。可以使用自动拆箱将它转换为一个 double:

```java
double s = (Double)m2,invoke(harry);
```

### 如何得到 Method 对象呢？ 当然， 可以通过调用 getDeclareMethods 方法， 然后对返回 的 Method 对象数组进行查找， 直到发现想要的方法为止。 也可以通过调用 Class类中的 getMethod方法得到想要的方法。它与 getField 方法类似。getField 方法根据表示域名的字 符串，返回一个 Field 对象。然而， 有可能存在若干个相同名字的方法，因此要格外小心， 以确保能够准确地得到想要的那个方法。有鉴于此，还必须提供想要的方法的参数类型。 getMethod 的签名是：

```java
Method getMethod(String name, Class... parameterTypes)
```

### 例如， 下面说明了如何获得 Employee 类的 getName 方法和 raiseSalary 方法的方法指针。

```java
Method ml = Employee.class.getMethod("getName");
Method m2 = Employee.class.getMethod("raiseSalary", double.class);
```

### 到此为止，读者已经学习了使用 Method 对象的规则。

### -> P206

### 190. 上述程序清楚地表明， 可以使用 method 对象实现 C (或 C# 中的委派）语言中函数指针 的所有操作。同 C 一样，这种程序设计风格并不太简便，出错的可能性也比较大。如果在调 用方法的时候提供了一个错误的参数，那么 invoke 方法将会抛出一个异常。

### 另外，invoke 的参数和返回值必须是 Object 类型的。这就意味着必须进行多次的类型转 换。这样做将会使编译器错过检查代码的机会。因此， 等到测试阶段才会发现这些错误， 找 到并改正它们将会更加困难。不仅如此， 使用反射获得方法指针的代码要比仅仅直接调用方 法明显慢一些。

### 有鉴于此，建议仅在必要的时候才使用 Method 对象，而最好使用接口以及 Java SE 8中 的 lambda 表达式（第 6 章中介绍）。特别要重申： 建议 Java 开发者不要使用 Method 对象的 回调功能。使用接口进行回调会使得代码的执行速度更快， 更易于维护。 （✡）

### -> P208

### 191. public     Object     invoke    (  Object    implicitParameter,     Object[  ]    explicitParamenters   )

### 调用这个对象所描述的方法， 传递给定参数，并返回方法的返回值。对于静态方法， 把 mill 作为隐式参数传递。在使用包装器传递基本类型的值时， 基本类型的返回值必 须是未包装的。

### -> P208

## 5.8 继承的设计技巧

2. 不要使用受保护的域 ->

有些程序员认为，将大多数的实例域定义为 protected 是一个不错的主意，只有这样，子 类才能够在需要的时候直接访问它们。然而， protected 机制并不能够带来更好的保护，其原因主要有两点。

第一，子类集合是无限制的， 任何一个人都能够由某个类派生一个子类，并 编写代码以直接访问 protected 的实例域， 从而破坏了封装性。

第二， 在 Java 程序设计语言 中，在同一个包中的所有类都可以访问 proteced 域，而不管它是否为这个类的子类。

不过，protected 方法对于指示那些不提供一般用途而应在子类中重新定义的方法很有用。

3. 使用继承实现“ is-a” 关系

使用继承很容易达到节省代码的目的，但有时候也被人们滥用了。例如， 假设需要定义 一个钟点工类。钟点工的信息包含姓名和雇佣日期，但是没有薪水。他们按小时计薪，并且 不会因为拖延时间而获得加薪。这似乎在诱导人们由 Employee 派生出子类 Contractor, 然后 再增加一个 hourlyWage 域。

```java
public class Contractor extends Employee
{
	private double hourlyWage;
	. . .
}
```

这并不是一个好主意。因为这样一来， 每个钟点工对象中都包含了薪水和计时工资这两个域。 在实现打印支票或税单方法的时候，会带来无尽的麻烦， 并且与不采用继承，会多写很代码。

钟点工与雇员之间不属于“ is-a” 关系。钟点工不是特殊的雇员。

4.  除非所有继承的方法都有意义，否则不要使用继承

假设想编写一个 Holiday 类3 毫无疑问，每个假日也是一日，并且一日可以用 Gregorian Calendar 类的实例表示，因此可以使用继承。

```java
class Holiday extends CregorianCalendar { . . . }
```

很遗憾， 在继承的操作中， 假日集不是封闭的。 在 GregorianCalendar 中有一个公有方法 add, 可以将假日转换成非假日：

```java
Holiday Christmas;
Christmas.add(Calendar.DAY_OF_MONTH , 12);
```

因此，继承对于这个例子来说并不太适宜。

需要指出， 如果扩展 LocalDate 就不会出现这个问题。由于这个类是不可变的，所以没 有任何方法会把假日变成非假日。

5. . 在覆盖方法时，不要改变预期的行为

置换原则不仅应用于语法， 而且也可以应用于行为，这似乎更加重要。在覆盖一个方法 的时候，不应该毫无原由地改变行为的内涵。就这一点而言，编译器不会提供任何帮助，即 编译器不会检查重新定义的方法是否有意义。例如，可以重定义 Holiday 类中 add方法“ 修 正” 原方法的问题，或什么也不做， 或抛出一个异常， 或继续到下一个假日。

然而这些都违反了置换原则。语句序列

```java
int dl = x.get(Calendar.DAY_OF_MONTH);
x.add(Calendar.DAY_OF_MONTH , 1);
int d2 = x.get(Calendar.DAY_OF_HONTH);
System.out.println(d2 - d1);
```

不管 x 属于 GregorianCalendar 类， 还是属于 Holiday 类，执行上述语句后都应该得到预期的 行为。

当然， 这样可能会引起某些争议。人们可能就预期行为的含义争论不休。例如， 有些人 争论说， 置换原则要求 Manager.equals 不处理 bonus 域，因为 Employee.equals 没有它。实际 上，凭空讨论这些问题毫无意义。关键在于， 在覆盖子类中的方法时，不要偏离最初的设计 想法。

6. 使用多态， 而非类型信息

无论什么时候，对于下面这种形式的代码

```java
if (x is of type 1)
	action1(x);
else if (x is of type 2)
	action2(x);
```

都应该考虑使用多态性。

action, 与 3如0112 表示的是相同的概念吗？ 如果是相同的概念，就应该为这个概念定义一 个方法， 并将其放置在两个类的超类或接口中，然后， 就可以调用

```java
x.action();
```

以便使用多态性提供的动态分派机制执行相应的动作。

使用多态方法或接口编写的代码比使用对多种类型进行检测的代码更加易于维护和扩展。

7. 不要过多地使用反射

反射机制使得人们可以通过在运行时查看域和方法， 让人们编写出更具有通用性的程序。 这种功能对于编写系统程序来说极其实用，但是通常不适于编写应用程序。反射是很脆弱的， 即编译器很难帮助人们发现程序中的错误， 因此只有在运行时才发现错误并导致异常。

现在你已经了解了 Java 支持面向对象编程的基础内容：类、继承和多态。下一章中我们 将介绍两个髙级主题：接口和 lambda 表达式， 它们对于有效地使用 Java 非常重要。

### -> P210

## 第六章、接口、lambda表达式与内部类

### 192. 到目前为止，读者已经学习了 Java 面向对象程序设计的全部基本知识。本章将开始介 绍几种常用的高级技术。这些内容可能不太容易理解，但一定要掌握它们，以便完善自己的 Java 工具箱。 -> P211

### 193. 接口：这种技术主要用来描述类具有什么功能，而并不 给出每个功能的具体实现。一个类可以实现（ implement) —个或多个接口，并在需要接口的 地方， 随时使用实现了相应接口的对象。  

### lambda 表达式：这是 一种表示可以在将来某个时间点执行的代码块的简洁方法。使用 lambda 表达式，可以用一 种精巧而简洁的方式表示使用回调或变量行为的代码。

### 内部类：内部类技术主要用于设计具 有相互协作关系的类集合。

### 代理：, 这是一种实现任意接口的对象。代理是一种非常 专业的构造工具，它可以用来构建系统级的工具。如果是第一次学习这本书，可以先跳过这 个部分。

### -> P211

## 6.1 接口

## 6.1.1 接口概念

### 194. 在 Java 程序设计语言中， 接口不是类，而是对类的一组需求描述，这些类要遵从接口描 述的统一格式进行定义。 -> P211

### 195. 接口中的所有方法自动地属于 public。 因此，在接口中声明方法时，不必提供关键字 public。 ->P212

### 196. 在接口 中还可以定义常。然而， 更为重要的是要知道接口不能提供哪些功能。接口绝不能含 有实例域， 在 JavaSE 8之前， 也不能在接口中实现方法。（在 6.1.4 节和 6.1.5 节中可以看 到，现在已经可以在接口中提供简单方法了u 当然， 这些方法不能引用实例域——接口没有 实例。） -> P212

### 197. 提供实例域和方法实现的任务应该由实现接口的那个类来完成。因此， 可以将接口看成 是没有实例域的抽象类= 但是这两个概念还是有一定区别的。 -> P212

### 198. 为了让类实现一个接口， 通常需要下面两个步骤：

1. 将类声明为实现给定的接口。
2. 对接口中的所有方法进行定义。

### 199. 在实现接口时， 必须把方法声明为 public ; 否则， 编译器 将认为这个方法的访问属性是包可见性， 即类的默认访问属性，之后编译器就会给出试 图提供更严格的访问权限的警告信息。 -> P213

### 200. 以下是 compareTo 方法的实现:

```java
public int compareTo(Object otherObject)
{
	Employee other = (Employee) otherObject;
	return Double.compare(salary, other.salary);
}
```

### 我们可以做得更好一些。可以为泛型 Comparable 接口提供一个类型参数。

```java
class Employee implements Comparable<Employee> {
	public int compareTo(Employee other) {
		return Double.compare(salary, other.salary);
	}
	. . .
}
```

### 请注意， 对 Object 参数进行类型转换总是让人感觉不太顺眼， 但现在已经不见了。

### -> P213

### 201. Comparable 接口中的 compareTo 方法将返回一个整型数值。如果两个对象不相等， 则返回一个正值或者一个负值。在对两个整数域进行比较时，这点非常有用。

### 例如，假 设每个雇员都有一个唯一整数 id，并希望根据 ID 对雇员进行重新排序， 那么就可以返回 id-other.idc 如果第一个 ID 小于另一个 ID, 则返回一个负值；如果两个 ID 相等， 则返回 0 ; 否则， 返回一个正值。

### 但有一点需要注意： 整数的范围不能过大， 以避免造成减法 运算的溢出。如果能够确信 ID 为非负整数， 或者它们的绝对值不会超过（Integer_MAX_ VALUE-1)/2, 就不会出现问题。否则， 调用静态 Integer.compare 方法。

### 当然，这里的相减技巧不适用于浮点值。 因为在 salary 和 other.salary 很接近但又不 相等的时候， 它们的差经过四舍五入后有可能变成 0。x < y 时，Double.compare(x, y) 调 用会返回 -1 ; 如果 x > y 则返回 1。 ✡

### -> P213

### 202. 为什么不能在 Employee 类直接提 供一个 compareTo 方法，而必须实现 Comparable 接口呢？

### 主要原因在于 Java 程序设计语言是一种强类型 （ strongly typed) 语言。在调用方法的时 候， 编译器将会检查这个方法是否存在。

### 在 sort 方法中可能存在下面这样的语句：

```java
if (a[i].compareTo(a[j]) > 0)
{
	// rearrange a[i] and a[j]
	. . .
}
```

### 为此， 编译器必须确认 a[i] —定有 compareTo 方法。如果 a 是一个 Comparable 对象的数组， 就可 以确保拥有 compareTo 方法，因为每个实现 Comparable 接口的类都必须提供这个方法的定义。

### -> P214

### 203. 有人认为， 将 Arrays 类中的 sort 方法定义为接收一个 Comparable[ ] 数组就可以在 使用元素类型没有实现 Comparable 接口的数组作为参数调用 sort 方法时， 由编译器给出 错误报告。但事实并非如此。在这种情况下， sort 方法可以接收一个 Object[ ] 数组， 并 对其进行笨拙的类型转换：

```java
// Approach used in the standard library not recommended
if (((Comparable) a[i]).compareTo(a[j]) > 0)
{
	// rearrange a[i] and a[j]
	. . .
}
```

### 如果 a[i] 不属于实现了 Comparable 接口的类， 那么虚拟机就会抛出一个异常。

### -> P214

### 204. 语 言 标 准 规 定：对 于 任 意 的 x 和 y, 实 现 必 须 能 够 保 证 sgn(x.compareTo(y)) = -sgn (y.compareTo(x)。) （也 就 是 说， 如 果 y.compareTo(x) 抛 出 一 个 异 常， 那 么 x.compareTo (y) 也 应 该 抛 出 一 个 异 常。）这 里 的“ sgn” 是 一 个 数 值 的 符 号：如 果 n 是 负 值， sgn⑻ 等 于 -1 ; 如 果 n 是 0, sgn(n) 等 于 0 ; 如 果 n 是 正 值， sgn⑻ 等 于 1 简 单 地 讲， 如 果 调 换 compareTo 的 参 数， 结 果 的 符 号 也 应 该 调 换 （而 不 是 实 际 值）。

### 与 equals 方 法 一 样， 在 继 承 过 程 中 有 可 能 会 出 现 问 题。

### 这 是 因 为 Manager ，展了 Employee , 而 Employee 实 现 的 是 Comparable, 而 不 是 Comparable 如 果 Manager 覆 盖 了 compareTo, 就 必 须 要 有 经 理 与 雇 员 进 行 比 较 的 思 想 准 备， 绝 不 能 仅 仅 将 雇 员 转 换 成 经 理。

```java
class Manager extends Employee {
	public int compareTo(Employee other) {
		Manager otherManager = (Manager)other; // NO
		. . .
	}
	. . .
}
```

### 这 不 符 合“ 反 对 称” 的 规 则。如 果 x 是 一 个 Employee 对 象，y 是 一 个 Manager 对 象， 调 用 x.compareTo(y) 不 会 抛 出 异 常， 它 只 是 将 x 和 y 都 作 为 雇 员 进 行 比 较。 但 是 反 过 来， y.compareTo(x) 将 会 抛 出 一 个 ClassCastException。

### 这 种 情 况 与 第 5 章 中 讨 论 的 equals 方 法 一 样， 修 改 的 方 式 也 一 样 ， 有 两 种 不 同 的 情 况。

### 如 果 子 类 之 间 的 比 较 含 义 不 一 样， 那 就 属 于 不 同 类 对 象 的 非 法 比 较。 每 个 compareTo 方 法 都 应 该 在 开 始 时 进 行 下 列 检 测：

```java
if (getClass() != other.getClass()) throw new ClassCastException()；
```

---

### 如 果 存 在 这 样 一 种 通 用 算 法， 它 能 够 对 两 个 不 同 的 子 类 对 象 进 行 比 较， 则 应 该 在 超 类 中 提 供 一 个 compareTo 方 法，并 将 这 个 方 法 声 明 为 final 。

### 例 如， 假 设 不 管 薪 水 的 多 少 都 想 让 经 理 大 于 雇 员， 像 Executive 和 Secretary 这 样 的 子 类 又 该 怎 么 办 呢？ 如 果 一 定 要 按 照 职 务 排 列 的 话， 那 就 应 该 在 Employee 类 中 提 供 一 个 rank 方 法,， 每 个 子 类 覆 盖 rank， 并 实 现 一 个 考 虑 rank 值 的 compareTo 方 法。

### -> P216

## 6.1.2 接口的特性

### 205. 接口不是类，尤其不能使用 new 运算符实例化一个接口：

```java
x = new Comparable(. . .); // ERROR
```

### 然而， 尽管不能构造接口的对象，却能声明接口的变量：

```java
Comparable x; // OK
```

### 接口变量必须弓I用实现了接口的类对象：

```java
x = new Employee(. . .); // OK provided Employee implements Comparable
```

### 如同使用 instanceof检查一个对象是否属于某个特定类一样， 也可以使用 instance 检查一个对象是否实现了某个特定的接口：

```java
if (anObject instanceof Comparable) { . . . }
```

### -> P217

---

### 206. 与可以建立类的继承关系一样，接口也可以被扩展。这里允许存在多条从具有较高通用 性的接口到较高专用性的接口的链。例如，假设有一个称为 Moveable 的接口：

```java
public interface Moveable
{
	void move(double x, double y);
}
```

### 然后， 可以以它为基础扩展一个叫做 Powered 的接口：

```java
public interface Powered extends Moveable
{
	double milesPerCallon();
}
```

### -> P217

---

### 207. 虽然在接口中不能包含实例域或静态方法，但却可以包含常量。例如：

```java
public interface Powered extends Moveable
{
	double milesPerCallon();
	double SPEED_LIMIT = 95; // a public static final constant
}
```

### 与接口中的方法都自动地被设置为 public—样，接口中的域将被自动设为 public static final。

### -> P217

### 208. 可以将接口方法标记为 public, 将域标记为 public static final。有些程序员出于习 惯或提高清晰度的考虑， 愿意这样做。但 Java 语言规范却建议不要书写这些多余的关键 字， 本书也采纳了这个建议。 -> P217  ✴

### 209. 有些接口只定义了常量， 而没有定义方法。

### 例如，在标准库中有一个 SwingConstants 就是这样一个接口， 其中只包含 NORTH、 SOUTH 和 HORIZONTAL 等常量。 任何实现 SwingConstants 接口的类都自动地继承了这些常量，并可以在方法中直接地引用 NORTH, 而不必采用 SwingConstants.NORTH 这样的繁琐书写形式。

### 然而，这样应用接口似乎有点偏 离了接口概念的初衷， 最好不要这样使用它。 ✡

### -> P217

### 210. 尽管每个类只能够拥有一个超类， 但却可以实现多个接口。

### 这就为定义类的行为提供了极大的灵活性。

### 例如， Java 程序设计语言有一个非常重要的内置接口，称为 Cloneable (将在 6.2.3 节中给予详细的讨论。) 如果某个类实现了这个 Cloneable 接口，Object 类中的 clone 方 法就可以创建类对象的一个拷贝。如果希望自己设计的类拥有克隆和比较的能力，只要实现 这两个接口就可以了: 使用逗号将实现的各个接口分隔开。

```java
class Employee implements Cloneable, Comparable
```

### -> P218

## 6.1.3 接口与抽象类

### 211. 有些程序设计语言允许一个类有多个超类， 例如 C++。我们将此特性称为多重继承 ( multiple inheritance )。 而 Java 的设计者选择了不支持多继承，其主要原因是多继承会让语言 本身变得非常复杂（如同 C++ )， 效率也会降低（如同 Eiffel )。 -> P218

### 212. 实际上，接口可以提供多重继承的大多数好处，同时还能避免多重继承的复杂性和低效性。 -> P218 ✳

### 213. C++ 具有多重继承特性， 随之带来了一些诸如虚基类、控制规则和横向指针 类型转换等复杂特性 ， 很少有 C++ 程序员使用多继承， 甚至有些人说：就不应该使用多 继承。也有些程序员建议只对“ 混合” 风格的继承使用多继承。 在“ 混合” 风格中， 一 个主要的基类描述父对象， 其他的基类（ 因此称为混合）扮演辅助的角色这种风格类 似于 Java 类中从一个基类派生， 然后实现若干个辅助接口。 -> P218

## 6.1.4 静态方法

### 214. 在 Java SE 8 中，允许在接口中增加静态方法。理论上讲，没有任何理由认为这是不合法 的。只是这有违于将接口作为抽象规范的初衷。

### 目前为止， 通常的做法都是将静态方法放在伴随类中。在标准库中， 你会看到成对出现 的接口和实用工具类， 如 Collection/Collections 或 Path/Paths。

### -> P219

### 215. 下面来看 Paths 类， 其中只包含两个工厂方法。可以由一个字符串序列构造一个文件或 目录的路径， 如 Paths.get( "jdk1.8.0", "jre", "bin" )。 在 Java SE 8 中， 可以为 Path 接口增加以 下方法：

```java
public interface Path {
	public static Path get(String first, String... more) {
	return Fi1eSystems.getDefault().getPath(first, more);
	}
	. . .
}
```

### 这样一来， Paths 类就不再是必要的了。

### 不过整个 Java 库都以这种方式重构也是不太可能的， 但是实现你自己的接口时，不再需 要为实用工具方法另外提供一个伴随类。 ✡

### -> P219

### 6.1.5 默认方法

### 216. 可以为接口方法提供一个默认实现。 必须用 default 修饰符标记这样一个方法。

```java
public interface Comparable<T> {
	default int compareTo(T other) { return 0; }
	// By default, all elements are the same
}
```

### 当然， 这并没有太大用处， 因为 Comparable 的每一个实际实现都要覆盖这个方法。

### 不过 有些情况下， 默认方法可能很有用。

### 例如，在第 11 章会看到， 如果希望在发生鼠标点击事件时得到通知，就要实现一个包含 5 个方法的接口：

```java
public interface MouseListener
{
	void mouseClicked(MouseEvent event);
	void mousePressed(MouseEvent event);
	void mouseReleased(MouseEvent event);
	void mouseEntered(MouseEvent event);
	void mouseExited(MouseEvent event);
}
```

### 大多数情况下， 你只需要关心其中的 1、2 个事件类型。在 Java SE 8 中， 可以把所有方法声明为默认方法， 这些默认方法什么也不做。

```java
public interface MouseListener
{
	default void mouseClicked(MouseEvent event) {}
	default void mousePressed(MouseEvent event) {}
	default void mouseReleased(MouseEvent event) {}
	default void mouseEntered(MouseEvent event) {}
	default void mouseExited(MouseEvent event) {}
}
```

### 这样一来，实现这个接口的程序员只需要为他们真正关心的事件覆盖相应的监听器。 默认方法可以调用任何其他方法。

### 例如， Collection 接口可以定义一个便利方法：

```java
public interface Collection
{
	int size(); // An abstract method
	default boolean isEmpty()
	{
		return size() == 0;
	}
	. . .
}
```

### 这样实现 Collection 的程序员就不用操心实现 isEmpty 方法了。

### -> P220

### 217. 在 JavaAPI 中，你会看到很多接口都有相应的伴随类，这个伴随类中实现了相应接 口 的部分或所有方法，如 CoUection/AbstractCollectkm 或 MouseListener/MouseAdapter。在 JavaSE 8 中， 这个技术已经过时。现在可以直接在接口中实现方法。 -> P220 ❇

### 218. 后来， 在 JavaSE 8 中， 又为这个接口增加了一个 stream 方法。 

### 假设 stream 方法不是一个默认方法。那么 Bag 类将不能编译， 因为它没有实现这个新方法。为接口增加一个非默认方法不能保证 “ 源代码兼容 ” ( source compatible )。

### 不过， 假设不重新编译这个类，而只是使用原先的一个包含这个类的 JAR 文件。这个类仍能正常加载，尽管没有这个新方法。程序仍然可以正常构造 Bag 实例，不会有意外发生。 ( 为接口增加方法可以保证“ 二进制兼容 ”）。不过， 如果程序在一个 Bag 实例上调用 stream 方法，就会出现一个 AbstractMethodError。

### 将方法实现为一个默认方法就可以解决这两个问题。Bag 类又能正常编译了。另外如果没有重新编译而直接加载这个类， 并在一个 Bag 实例上调用 stream 方法， 将调用 Collection.stream 方法。 ✡

### -> P220

## 6.1.6 解决默认方法冲突

### 219. 如果先在一个接口中将一个方法定义为默认方法， 然后又在超类或另一个接口中定义了 同样的方法， 会发生什么情况？ 诸如 Scala 和 C++ 等语言对于解决这种二义性有一些复杂的 规则。幸运的是，Java 的相应规则要简单得多。规则如下：

1. 超类优先。如果超类提供了一个具体方法，同名而且有相同参数类型的默认方法会 被忽略。
2. 接口冲突。 如果一个超接口提供了一个默认方法，另一个接口提供了一个同名而且 参数类型（不论是否是默认参数）相同的方法， 必须覆盖这个方法来解决冲突。

### -> P220

### 220. 下面来看第二个规则。考虑另一个包含 getName 方法的接口：

```java
interface Named
{
	default String getName() { return getClass().getName() + "_" + hashCode() ; }
}
```

### 如果有一个类同时实现了这两个接口会怎么样呢？

```java
class Student implements Person, Named {
	. . .
}
```

### 类会继承 Person 和 Named 接口提供的两个不一致的 getName 方法。并不是从中选择一 个，Java 编译器会报告一个错误，让程序员来解决这个二义性。只需要在 Student 类中提供 一个 getName 方法。在这个方法中，可以选择两个冲突方法中的一个，如下所示：

```java
class Student implements Person, Named
{
	public String getName() { return Person.super.getName(); }
	. . .
}
```

### 现在假设 Named 接口没有为 getName 提供默认实现：

```java
interface Named
{
	String getName();
}
```

### Student 类会从 Person 接口继承默认方法吗？ 这好像挺有道理， 不过，Java 设计者更强 调一致性。两个接口如何冲突并不重要。如果至少有一个接口提供了一个实现，编译器就会 报告错误， 而程序员就必须解决这个二义性。 ❇

### -> P221

### 221. 当然，如果两个接口都没有为共享方法提供默认实现， 那么就与 Java SE 8之前的 情况一样，这里不存在冲突。 实现类可以有两个选择：实现这个方法，或者干脆不实现。 如果是后一种情况，这个类本身就是抽象的。 -> P221

### 222. 我们只讨论了两个接口的命名冲突。现在来考虑另一种情况，一个类扩展了一个超类， 同时实现了一个接口，并从超类和接口继承了相同的方法。

### 例如， 假设 Person 是一个类， Student 定义为：

```java
class Student extends Person implements Named { . . . }
```

### 在这种情况下， 只会考虑超类方法，接口的所有默认方法都会被忽略。在我们的例子 中， Student 从 Person 继承了 getName 方法， Named 接口是否为 getName 提供了默认实现并 不会带来什么区别。这正是“ 类优先” 规则。 ✡

### “ 类优先” 规则可以确保与 Java SE 7 的兼容性。如果为一个接口增加默认方法，这对于 有这个默认方法之前能正常工作的代码不会有任何影响。

### -> P221

### 223. 千万不要让一个默认方法重新定义 Object 类中的某个方法。例如，不能为 toString 或 equals 定义默认方法， 尽管对于 List 之类的接口这可能很有吸引力， 由于“ 类优先” 规则， 这样的方法绝对无法超越 Object.toString 或 Objects.equals。 -> P222 ✡

## 6.2 接口示例

## 6.2.1 接口与回调

### 224. 回调（ callback) 是一种常见的程序设计模式。在这种模式中，可以指出某个特定事件发生时应该采取的动作。 -> P222

### 225. 如何告之定时器做什么呢？ 在很多程序设计语言中，可以提供一个函数名， 定时器周期 性地调用它。 但是， 在 Java 标准类库中的类采用的是面向对象方法。它将某个类的对象传递 给定时器，然后，定时器调用这个对象的方法。由于对象可以携带一些附加的信息，所以传 递一个对象比传递一个函数要灵活得多。 -> P222

### 226. 需要注意， 这个程序除了导入 javax.swing.* 和 java.util.* 外， 还通过类名导入了 javax. swing.Timer。 这 就 消 除 了 javax.swing.Timer 与 java.util.Timer 之间产生的二义性。 这里的 java. util.Timer 是一个与本例无关的类， 它主要用于调度后台任务。 -> P223 ❇

## 6.2.2 Comparator 接口

### 227. 现在假设我们希望按长度递增的顺序对字符串进行排序，而不是按字典顺序进行排序。 肯定不能让 String 类用两种不同的方式实现 compareTo 方法—更何况，String 类也不应由 我们来修改。 -> P224

### 228. 要处理这种情况，Arrays.Sort 方法还有第二个版本， 有一个数组和一个比较器 ( comparator ) 作为参数， 比较器是实现了 Comparator 接口的类的实例。

```java
public interface Comparators
{
	int compare(T first, T second);
}
```

### 要按长度比较字符串，可以如下定义一个实现 Comparator 的类：

```java
class LengthComparator implements Comparator<String>
{
	public int compare(String first, String second) {
		return first.length() - second.length()；
	}
}
```

### 具体完成比较时，需要建立一个实例：

```java
Comparator<String> comp = new LengthComparator()；
if (comp.compare(words[i], words[j]) > 0) . . .
```

### 将这个调用与 words[i].compareTo(words[j]) 做比较。这个 compare 方法要在比较器对象 上调用，而不是在字符串本身上调用。 ✴

### -> P225

### 229. 尽管 LengthComparator 对象没有状态， 不过还是需要建立这个对象的一个实例。 我们需要这个实例来调用 compare 方法—— 它不是一个静态方法。 -> P225 ✡

### 230. 要对一个数组排序， 需要为 Arrays.sort 方法传人一个 LengthComparator 对象：

```java
String[] friends = { "Peter", "Paul", "Mary" };
Arrays,sort(friends, new LengthComparator());
```

### 现在这个数组可能是 ["Paul","Mary","Peter"] 或 ["Mary","Paul","Peter"]。 

### 在 6.3 节中我们会了解， 利用 lambda 表达式可以更容易地使用 Comparator。

### -> P225

## 6.2.3 对象克隆

### 231. 本节我们会讨论 Cloneable 接口，这个接口指示一个类提供了一个安全的 clone 方法。由 于克隆并不太常见，而且有关的细节技术性很强，你可能只是想稍做了解， 等真正需要时再 深人学习。 -> P225

### 232. 要了解克隆的具体含义，先来回忆为一个包含对象引用的变量建立副本时会发生什么。 原变量和副本都是同一个对象的引用（见图 6-1 )。这说明， 任何一个变量改变都会影响另一 个变量。

```java
Employee original = new Employee("John Public", 50000);
Employee copy = original;
copy.raiseSalary(lO); // oops--also changed original
```

### 如果希望 copy 是一个新对象，它的初始状态与 original 相同， 但是之后它们各自会有自 己不同的状态， 这种情况下就可以使用 clone 方法。

```java
Employee copy = original.clone();
copy.raiseSalary(10); // OK original unchanged
```

<img src="F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）拷贝和克隆.png" alt="Java核心技术（卷一）拷贝和克隆"  />

### 不过并没有这么简单。clone 方法是 Object 的一个 protected 方法，这说明你的代码不能 直接调用这个方法。只有 Employee 类可以克隆 Employee 对象。这个限制是有原因的。想想 看 Object 类如何实现 clone。它对于这个对象一无所知， 所以只能逐个域地进行拷贝。 如果 对象中的所有数据域都是数值或其他基本类型，拷贝这些域没有任何问题、 但是如果对象包 含子对象的引用，拷贝域就会得到相同子对象的另一个引用，这样一来，原对象和克隆的对 象仍然会共享一些信息。✡

### 为了更直观地说明这个问题， 考虑第 4 章介绍过的 Employee 类。 图 6-2 显示了使用 Object 类的 clone 方法克隆这样一个 Employee 对象会发生什么。可以看到， 默认的克隆操作 是“ 浅拷贝”，并没有克隆对象中引用的其他对象。（这个图显示了一个共享的 Date 对象。出 于某种原因（稍后就会解释这个原因，) 这个例子使用了 Employee 类的老版本，其中的雇用 日期仍用 Date 表示。）

### 浅拷贝会有什么影响吗？ 这要看具体情况。如果原对象和浅克隆对象共享的子对象是不 可变的， 那么这种共享就是安全的。如果子对象属于一个不可变的类， 如 String, 就 是 这 种 情况。或者在对象的生命期中， 子对象一直包含不变的常量， 没有更改器方法会改变它， 也 没有方法会生成它的引用，这种情况下同样是安全的。

![Java核心技术（卷一）浅拷贝](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）浅拷贝.png)

### 不过， 通常子对象都是可变的， 必须重新定义 clone 方法来建立一个深拷贝， 同时克隆 所有子对象。在这个例子中，hireDay 域是一个 Date , 这是可变的， 所以它也需要克隆。（出 于这个原因， 这个例子使用 Date 类型的域而不是 LocalDate 来展示克隆过程。如果 hireDay 是不可变的 LocalDate 类的一个实例，就无需我们做任何处理了。）

### 对于每一个类，需要确定：

1. 默认的 clone 方法是否满足要求；
2. 是否可以在可变的子对象上调用 clone 来修补默认的 clone 方法；
3. 是否不该使用 clone。

### 实际上第 3 个选项是默认选项。如果选择第 1 项或第 2 项，类必须：

1. 实现 Cloneable 接口；
2. 重新定义 clone 方法，并指定 public 访问修饰符。

### -> P227

### 233. Object 类中 clone 方法声明为 protected , 所以你的代码不能直接调用 anObject. clone(。) 但是， 不是所有子类都能访问受保护方法吗？ 不是所有类都是 Object 的子类 吗？ 幸运的是， 受保护访问的规则比较微妙（见第 5 章）。子类只能调用受保护的 clone 方法来克隆它自己的对象。 必须重新定义 clone 为 public 才能允许所有方法克隆对象。 -> P227

### 234. 在这里， Cloneable 接口的出现与接口的正常使用并没有关系。具体来说，它没有指定 done 方法，这个方法是从 Object 类继承的。这个接口只是作为一个标记，指示类设计者了 解克隆过程。对象对于克隆很“ 偏执”， 如果一个对象请求克隆， 但没有实现这个接口， 就 会生成一个受査异常。 -> P227 ❇

### 235. Cloneable 接口是 Java 提供的一组标记接口 ( tagging interface ) 之一。（有些程序员称之为记号接口 ( marker interface ) )。应该记得，Comparable 等接口的 通常用途 是确保一个类实现一个或一组特定的方法。标记接口不包含任何方法； 它唯一的作用就是允许 在类型查询中使用 instanceof:

```java
if (obj instanceof Cloneable) . . .
```

### 建议你自己的程序中不要使用标记接口。 ✡

### -> P228

### 236. 即使 clone 的默认（浅拷贝）实现能够满足要求， 还是需要实现 Cloneable 接口， 将 clone 重新定义为 public，再调用 super.clone(。) 下面给出一个例子：

```java
class Employee implements Cloneable {
	// raise visibility level to public, change return type
	public Employee clone() throws CloneNotSupportedException {
		return (Employee)super.clone();
	}
	. . .
}
```

### 在 Java SE 1.4 之前， clone 方法的返回类型总是 Object, 而现在可以为你的 clone 方法指定正确的返回类型。这是协变返回类型的一个例子（见第 5 章）。

### -> P228

### 237. 与 Objectxkme 提供的浅拷贝相比， 前面看到的 clone 方法并没有为它增加任何功能。这里 只是让这个方法是公有的。要建立深拷贝，还需要做更多工作，克隆对象中可变的实例域。

### 下面来看创建深拷贝的 done 方法的一个例子：

```java
class Employee implements Cloneable {
	. . .
	public Employee cloneO throws CloneNotSupportedException {
		// call Object.clone()
		Employee cloned = (Employee) super.clone();
		
		// clone mutable fields
		cloned.hireDay = (Date) hireDay.clone();
		
		return cloned;
	}
}
```

### 如果在一个对象上调用 clone, 但这个对象的类并没有实现 Cloneable 接口， Object 类 的 clone 方法就会拋出一个 CloneNotSupportedExceptionD 当然，Employee 和 Date 类实现了 Cloneable 接口，所以不会抛出这个异常。 不过， 编译器并不了解这一点，因此，我们声明了 这个异常：

```java
public Employee clone() throws CloneNotSupportedException
```

### 捕获这个异常是不是更好一些？

```java
public Employee clone() {
	try {
		Employee cloned = (Employee) super.clone();
	} catch (CloneNotSupportedException e) { return null; }
	// this won't happen, since we are Cloneable
}
```

### 这非常适用于 final 类。否则， 最好还是保留 throws 说明符。这样就允许子类在不支持 克隆时选择抛出一个 CloneNotSupportedException。 ✴

### -> P229

### 238. 必须当心子类的克隆。 ✡

### 例如，一旦为 Employee 类定义了 clone 方法，任何人都可以用它 来克隆 Manager 对象。Employee 克隆方法能完成工作吗？ 这取决于 Manager 类的域。在这里 是没有问题的， 因为 bonus 域是基本类型。但是 Manager 可能会有需要深拷贝或不可克隆的 域。不能保证子类的实现者一定会修正 clone 方法让它正常工作。出于这个原因，在 Object 类中 clone 方法声明为 protected。不过， 如果你希望类用户调用 clone, 就不能这样做。

### -> P229

### 239. 要不要在自己的类中实现 clone 呢？ 如果你的客户需要建立深拷贝，可能就需要实现这 个方法。有些人认为应该完全避免使用 clone, 而实现另一个方法来达到同样的目的。clone 相当笨拙， 这一点我们也同意，不过如果让另一个方法来完成这个工作， 还是会遇到同样的 问题。毕竟， 克隆没有你想象中那么常用。标准库中只有不到 5% 的类实现了 done。 ✳ -> P229

### 240. 所有数组类型都有一个 public 的 clone 方法， 而不是 protected: 可以用这个方法 建立一个新数组， 包含原数组所有元素的副本。例如：

```java
int[] luckyNumbers = { 2, 3, 5, 7, 11, 13 };
int[] cloned = luckyNumbers.clone();
cloned[5] = 12; // doesn't change luckyNumbers[5]
```

### ✡ -> P229

### 241. 卷 II 的第 2 章将展示另一种克隆对象的机制， 其中使用了 Java 的对象串行化特性。 这个机制很容易实现，而且很安全，但效率不高。❇

## 6.3 lambda 表达式

### 242. 这是这些年来 Java 语言最让人激动的一个变化。你会 了解如何使用 lambda 表达式采用一种简洁的语法定义代码块， 以及如何编写处理 lambda 表 达式的代码。 -> P231

## 6.3.1 为什么引入 lambda 表达式

### 243. compare 方法不是立即调用。 实际上， 在数组完成排序之前， sort 方法会一直调用 compare 方法，只要元素的顺序不正确就会重新排列元素。将比较元素所需的代码段放在 sort 方法中， 这个代码将与其余的排序逻辑集成（你可能并不打算重新实现其余的这部分逻辑）。

### 这两个例子有一些共同点，都是将一个代码块传递到某个对象（一个定时器， 或者一个 sort 方法。) 这个代码块会在将来某个时间调用。

### -> P232

### 244. 到目前为止，在 Java 中传递一个代码段并不容易， 不能直接传递代码段 。Java 是一种面 向对象语言，所以必须构造一个对象，这个对象的类需要有一个方法能包含所需的代码。 -> P232

### 245. 在其他语言中，可以直接处理代码块。Java 设计者很长时间以来一直拒绝增加这个特性。 毕竟，Java 的强大之处就在于其简单性和一致性。如果只要一个特性能够让代码稍简洁一些， 就把这个特性增加到语言中， 这个语言很快就会变得一团糟，无法管理。 不过， 在另外那些 语言中，并不只是创建线程或注册按钮点击事件处理器更容易；它们的大部分 API 都更简单、 更一致而且更强大。在 Java 中， 也可以编写类似的 AP丨利用类对象实现特定的功能，不过这 种 API 使用可能很不方便。 -> P232

## 6.3.2 lambda 表达式的语法

### 246. 你已经见过 Java 中的一种 lambda 表达式形式：参数， 箭头（->) 以及一个表达式。如 果代码要完成的计算无法放在一个表达式中，就可以像写方法一样，把这些代码放在 {丨中， 并包含显式的 return语句。例如：

```java
(String first, String second) ->
{
	if (first.length() < second.length()) return -1;
	else if (first.length() > second.length()) return 1;
	else return 0;
}
```

### 即使 lambda 表达式没有参数， 仍然要提供空括号，就像无参数方法一样： ✡

~~~java
0 -> { for (int i = 100;i >= 0;i-- ) System.out.println(i); }
~~~

### 如果可以推导出一个 lambda 表达式的参数类型，则可以忽略其类型。例如：

```java
Comparator<String> comp
= (first, second) // Same as (String first, String second)
	-> first.length() - second.length();
```

### 如果方法只有一 参数， 而且这个参数的类型可以推导得出，那么甚至还可以省略小括号：

```java
ActionListener listener = event ->
	System.out.println("The time is " + new Date());
		// Instead of (event) -> . . . or (ActionEvent event) -> . . .
```

### 无需指定 lambda 表达式的返回类型。lambda 表达式的返回类型总是会由上下文推导得 出。例如，下面的表达式

```java
(String first, String second) -> first.length() - second.length()
```

### 可以在需要 im 类型结果的上下文中使用。

### -> P233 ✡

### 247. 如果一个 lambda 表达式只在某些分支返回一个值， 而在另外一些分支不返回值， 这是不合法的。例如，（ int x )-> { if ( x >= 0 )  return 1; } 就不合法。 -> P233 ❇

## 6.3.3 函数式接口

### 248. 前 面 已 经 讨 论 过， Java 中 已 经 有 很 多 封 装 代 码 块 的 接 口， 如 ActionListener 或 Comparatorlambda 表达式与这些接口是兼容的。

### 对于只有一个抽象方法的接口， 需要这种接口的对象时， 就可以提供一个 lambda 表达 式。这种接口称为函数式接口 （ functional interface )。

### -> P234

### 249. 你可能想知道为什么函数式接口必须有一个抽象方法。不是接口中的所有方法都 是抽象的吗？ 实际上， 接口完全有可能重新声明 Object 类的方法， 如 toString 或 clone, 这些声明有可能会让方法不再是抽象的。（ Java API 中的一些接口会重新声明 Object 方法 来附加 javadoc 注释 Comparator AP丨就是这样一个例子。） 更重要的是， 正如 6.1.5 节所 述， 在 JavaSE 8 中， 接口可以声明非抽象方法。 -> P234

### 250. 为了展示如何转换为函数式接口，下面考虑 Arrays.sort 方法。它的第二个参数需要一个 Comparator 实例， Comparator 就是只有一个方法的接口， 所以可以提供一个 lambda 表达式：

```java
Arrays.sort(words, (first, second) -> first.length() - second.length());
```

### 在底层， Arrays.sort 方法会接收实现了 Comparator 的某个类的对象。 在这个对象上调用 compare 方法会执行这个 lambda 表达式的体。这些对象和类的管理完全取决于具 体实现， 与使用传统的内联类相比，这样可能要高效得多。最好把 lambda 表达式看作是一 个函数，而不是一个对象， 另外要接受 lambda 表达式可以传递到函数式接口。 ✡

### -> P235

### 251. lambda 表达式可以转换为接口， 这一点让 lambda 表达式很有吸引力。具体的语法很简 短。下面再来看一个例子：

```java
Timer t = new Timer(1000, event ->
{
	System.out.println("At the tone, the time is " + new Date());
	Toolkit.getDefaultToolkit().beep();
}；
```

### 与使用实现了 ActionListener 接口的类相比， 这个代码可读性要好得多。

### -> P235

### 252. 实际上，在 Java 中， 对 lambda 表达式所能做的也只是能转换为函数式接口。在其他支 持函数字面量的程序设计语言中，可以声明函数类型（如（String, String) -> int)、 声明这些类 型的变量，还可以使用变量保存函数表达式。不过，Java 设计者还是决定保持我们熟悉的接 口概念， 没有为 Java语言增加函数类型。 -> P235

### 253. 甚至不能把丨ambda 表达式赋■ 给类型为 Object 的变量，Object 不是一个函数式接口。 -> P235 ❇

### 254. Java API 在java.util.fimction 包中定义了很多非常通用的函数式接口。其中一个接口 BiFunction <T, U ,R> 描述了参数类型为 T 和 U 而且返回类型为 R 的函数。可以把我们的字符 串比较 lambda 表达式保存在这个类型的变量中：

```java
BiFunction<String, String, Integer> comp
= (first, second) -> first.length() - second.length();
```

### 不过，这对于排序并没有帮助。没有哪个 Arrays.sort 方法想要接收一个 BiFunction。

### 如 果你之前用过某种函数式程序设计语言，可能会发现这很奇怪。不过，对于 Java 程序员而 言，这非常自然。类似 Comparator 的接口往往有一个特定的用途， 而不只是提供一个有指定 参数和返回类型的方法。Java SE 8 沿袭了这种思路。想要用 lambda 表达式做某些处理，还 是要谨记表达式的用途，为它建立一个特定的函数式接口。 ✴

### -> P235

### 255. java.util.function 包中有一个尤其有用的接口 Predicate: ✳

```java
public interface Predicate<T>
{
	boolean test(T t);
	// Additional default and static methods
}
```

### -> P235

---

### 256. ArrayList 类有一个 removelf 方法， 它的参数就是一个 Predicate。这个接口专门用来传递 lambda 表达式。例如，下面的语句将从一个数组列表删除所有 null 值： ✡

```java
list.removeIf(e -> e == null);
```

### -> P235

---

## 6.3.4 方法引用

### 257. 有时， 可能已经有现成的方法可以完成你想要传递到其他代码的某个动作。

### 例如， 假设你希望只要出现一个定时器事件就打印这个事件对象。 当然，为此也可以调用:

```java
Timer t = new Timer(1000, event -> System.out.println(event)):
```

### 但是，如果直接把 println 方法传递到 Timer 构造器就更好了。具体做法如下：

```java
Timer t = new Timer(1000, Systei.out::println);
```

### 表达式 System.out::println 是一个方法引用（ method reference ), 它等价于 lambda 表达式 x 一> System.out.println(x) 。

### 再来看一个例子， 假设你想对字符串排序， 而不考虑字母的大小写。可以传递以下方法 表达式：

```java
Arrays.sort(strings，String::conpareToIgnoreCase)
```

### -> P236

---

### 258. 从这些例子可以看出， 要用：: 操作符分隔方法名与对象或类名。主要有 3 种情况：

- object::instanceMethod
- Class::staticMethod
- Class::instanceMethod

### 在前 2 种情况中，方法引用等价于提供方法参数的 lambda 表达式。前面已经提到， System.out::println 等价于 x -> System.out.println(x) 。 类似地，Math::pow 等价于（x，y) -> Math.pow(x, y)。

### 对于第 3 种情况， 第 1 个参数会成为方法的目标。例如，String::compareToIgnoreCase 等 同于 (x, y) -> x.compareToIgnoreCase(y) 。

### -> P236

### 259. 如果有多个同名的重栽方法， 编译器就会尝试从上下文中找出你指的那一个方法。 例如， Math.max 方法有两个版本， 一个用于整数， 另一个用于 double 值。选择哪一个版 本取决于 Math::max 转换为哪个函数式接口的方法参数。 类似于 lambda 表达式，方法引 用不能独立存在，总是会转换为函数式接口的实例。 -> P236

### 260. 可以在方法引用中使用 this 参数。例如，this::equals 等同于 x -> this.equals(x)。 使用 super 也是合法的。下面的方法表达式

```java
super::instanceMethod
```

### 使用 supper 作为目标，会调用给定方法的超类版本。

### -> P236

## 6.3.5 构造器引用

### 261. 构造器引用与方法引用很类似，只不过方法名为 new。例如，Person::new 是 Person 构造 器的一个引用。哪一个构造器呢？ 这取决于上下文。假设你有一个字符串列表。可以把它转 换为一个 Person 对象数组，为此要在各个字符串上调用构造器，调用如下：

```java
ArrayList<String> names = . . .;
Stream<Person> stream = names.stream().map(Person::new);
List<Person> people = stream.col1ect(Col1ectors.toList());
```

### -> P237

---

### 262. 可以用数组类型建立构造器引用。例如， int[]::new 是一个构造器引用，它有一个参数： 即数组的长度。这等价于 lambda 表达式 x -> new int[x]。 -> P237

### 263. Java 有一个限制，无法构造泛型类型 T 的数组。数组构造器引用对于克服这个限制很有 用。表达式 new T[n] 会产生错误，因为这会改为 new Object[n。] 对于开发类库的人来说，这 是一个问题。例如，假设我们需要一个 Person 对象数组。Stream 接口有一个 toArray 方法可 以返回 Object 数组：

```java
Object[] people = stream.toArray()；
```

### 不过，这并不让人满意。用户希望得到一个 Person 引用数组，而不是 Object 引用数组。 流库利用构造器引用解决了这个问题。可以把 Person[]::new 传入 toArray 方法：

```java
Person[] people = stream.toArray(PersonD::new):
```

### toArray方法调用这个构造器来得到一个正确类型的数组。然后填充这个数组并返回。

### -> P237

## 6.3.6 变量作用域

### 264. lambda 表达式有 3 个部分：

1. 一个代码块；
2. 参数;
3. 自由变量的值， 这是指非参数而且不在代码中定义的变量。

### -> P238

### 265. 可以看到，lambda 表达式可以捕获外围作用域中变量的值。 在 Java 中，要确保所捕获 的值是明确定义的，这里有一个重要的限制。在 lambda 表达式中， 只能引用值不会改变的 变量。例如， 下面的做法是不合法的：

```java
public static void countDown(int start, int delay)
{
	ActionListener listener = event ->
		{
			start ; // Error: Can't mutate captured variable
			System.out.println(start);
		}；
	new Timer(delay, listener),start();
}
```

### 之所以有这个限制是有原因的。如果在 lambda 表达式中改变变量， 并发执行多个动作 时就会不安全。对于目前为止我们看到的动作不会发生这种情况，不过一般来讲，这确实是 一个严重的问题。关于这个重要问题的更多内容参见第 14 章。

---

### 另外如果在 lambda 表达式中引用变量， 而这个变量可能在外部改变，这也是不合法的。 例如，下面就是不合法的：

```java
public static void repeat(String text, int count)
{
	for (int i = 1; i <= count; i++)
	{
		ActionListener listener = event ->
			{
				System.out.print1n(i + ": " + text);
					// Error: Cannot refer to changing i
			}；
		new Timer(1000, listener).start();
	}
}
```

### 这里有一条规则：lambda 表达式中捕获的变量必须实际上是最终变量 ( effectively final ) 。 实际上的最终变量是指， 这个变量初始化之后就不会再为它赋新值。在这里，text 总是指示 同一个 String 对象，所以捕获这个变量是合法的。不过，i 的值会改变，因此不能捕获 i 。 ✡

### -> P239

### 266. lambda 表达式的体与嵌套块有相同的作用域。这里同样适用命名冲突和遮蔽的有关规 则。在 lambda 表达式中声明与一个局部变量同名的参数或局部变量是不合法的。

```java
Path first = Paths.get("/usr/bin");
Couparator<String> comp =
	(first, second) -> first.length() - second.length();
	// Error: Variable first already defined
```

### 在方法中，不能有两个同名的局部变量， 因此， lambda 表达式中同样也不能有同名的局 部变量。

### -> P239

### 267. 在一个 lambda 表达式中使用 this 关键字时， 是指创建这个 lambda 表达式的方法的 this 参数。 例如，考虑下面的代码：

```java
public class Application()
{
	public void init()
	{
		ActionListener listener = event ->
			{
				System.out.println(this.toString());
				. . .
			}
		. . .
	}
}
```

### 表达式 this.toStringO 会调用 Application 对象的 toString方法， 而不是 ActionListener 实 例的方法。在 lambda 表达式中， this 的使用并没有任何特殊之处。lambda 表达式的作用域嵌 套在 init 方法中，与出现在这个方法中的其他位置一样， lambda 表达式中 this 的含义并没有 变化。

### -> P239

## 6.3.7 处理 lambda 表达式

### 268. 使用 lambda 表达式的重点是延迟执行 deferred execution ) 。✡ -> P240

### 269. 毕竟， 如果想耍立即执行代 码，完全可以直接执行， 而无需把它包装在一个 lambda 表达式中。之所以希望以后再执行 代码， 这有很多原因， 如：

- 在一个单独的线程中运行代码；
- 多次运行代码；
- 在算法的适当位置运行代码（例如， 排序中的比较操作 )；
- 发生某种情况时执行代码（如， 点击了一个按钮， 数据到达， 等等 )；
- 只在必要时才运行代码。

### -> P240

### 270. ![Java核心技术（卷一）常用函数式接口](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）常用函数式接口.png)

### 表 6-2 列出了基本类型 int、 long 和 double 的 34 个可能的规范。 最好使用这些特殊 化规范来减少自动装箱。出于这个原因， 我在上一节的例子中使用了 IntConsumer 而不是 ConsumeKlnteger〉 。 ❇

![Java核心技术（卷一）基本类型的函数式接口](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）基本类型的函数式接口.png)

### 最好使用表 6-1 或表 6-2 中的接口。 例如， 假设要编写一个方法来处理满足 某个特定条件的文件。 对此有一个遗留接口 java.io.FileFilter, 不过最好使用标准的 Predicate , 只有一种情况下可以不这么做， 那就是你已经有很多有用的方法可以生 成 FileFilter 实例。✡

### -> P241

### 271. 大多数标准函数式接口都提供了非抽象方法来生成或合并函数。 例如， Predicate. isEqual(a) 等同于 a::equals, 不过如果 a 为 null 也能正常工作。已经提供了默认方法 and、 or 和 negate 来合并谓词。 例如， Predicate.isEqual(a).or(Predicate.isEqual(b)) 就等同于 x -> a.equals(x) || b.equals(x)。 -> P241

### 272. 如果设计你自己的接口，其中只有一个抽象方法，可以用 @FunctionalInterface 注 解来标记这个接口。这样做有两个优点。 如果你无意中增加了另一个非抽象方法， 编译 器会产生一个错误消息。 另外 javadoc 页里会指出你的接口是一个函数式接口。

### 并不是必须使用注解根据定义，任何有一个抽象方法的接口都是函数式接口。不 过使用 @FunctionalInterface 注解确实是一个很好的做法。

### -> P241

## 6.3.8 再谈 Comparator

### 273. 这些方法有很多变体形式。可以为 comparing 和 thenComparing 方法提取的键指定一个 比较器。例如，可以如下根据人名长度完成排序：

```java
Arrays.sort(people, Comparator.companng(Person::getName,
(s, t) -> Integer.compare(s.length(), t.length())))；
```

### 另外， comparing 和 thenComparing 方法都有变体形式，可以避免 int、 long 或 double 值 的装箱。要完成前一个操作， 还有一种更容易的做法： ✡

```java
Arrays.sort(people, Comparator.comparinglnt(p -> p.getName().length()));
```

### 如果键函数可以返回 null, 可 能 就 要 用 到 nullsFirst 和 nullsLast 适配器。这些静态方 法会修改现有的比较器，从而在遇到 null 值时不会抛出异常， 而是将这个值标记为小于或 大于正常值。例如， 假设一个人没有中名时 getMiddleName 会返回一个 null, 就 可 以 使 用 Comparator.comparing(Person::getMiddleName(), Comparator.nullsFirst(… )。

### nullsFirst 方法需要一个比较器，在这里就是比较两个字符串的比较器。naturalOrder 方法可以 为任何实现了 Comparable 的类建立一个比较器。在这里，Comparator. <String>naturalOrder() 正是 我们需要的。下面是一个完整的调用， 可以按可能为 null 的中名进行排序。这里使用了一个静态 导人 java.util.C0mparator. *， 以便理解这个表达式。注意 naturalOrder 的类型可以推导得出。

```java
Arrays.sort(people, comparing(Person::getMiddleName , nulIsFirst(naturalOrder())));
```

### -> P242

---

### 274. 静态 reverseOrder 方法会提供自然顺序的逆序。要让比较器逆序比较， 可以使用 reversed 实例方法c 例如 naturalOrder().reversed() 等同于 reverseOrder() 。 -> P242

## 6.4 内部类

### 275. 为什么需要使用内部类呢？ 其主要原因有以下三点：

- 内部类方法可以访问该类定义所在的作用域中的数据， 包括私有的数据。
- 内部类可以对同一个包中的其他类隐藏起来。
- 当想要定义一个回调函数且不想编写大量代码时，使用匿名 （anonymous) 内部类比较 便捷。

### -> P243

### 276. 匿名内部类：在 Java 有 lambda 表达式之前用于实现回调的基本方法。 -> P243

### 277. C++ 有嵌套类。一个被嵌套的类包含在外围类的作用域内。下面是一个典型 的例子，一个链表类定义了一个存储结点的类和一个定义迭代器位置的类。

```C++
class LinkedList
{
public:
	class Iterator // a nested class
	{
	public:
		void insert(int x);
		int erase();
		. . .
	};
	. . .
private:
	class Link // a nested class
	{
	public:
		Link* next;
		int data;
	};
	. . .
};
```

### 嵌套是一种类之间的关系， 而不是对象之间的关系。一个 LinkedList 对象并不包含 Iterator 类型或 Link 类型的子对象。 ❇

### 可以将 Link 的数据域设计为公有的， 它仍然是安全的。这些数据域只能被 LinkedList 类 （具有访问这些数据域的合理需要）中的方法访问， 而不会暴露给其他的代 码。在 Java 中， 只有内部类能够实现这样的控制。 ✡

### 然而， Java 内部类还有另外一个功能，这使得它比 C++ 的嵌套类更加丰富， 用途更 加广泛。 内部类的对象有一个隐式引用， 它引用了实例化该内部对象的外围类对象。通 过这个指针， 可以访问外围类对象的全部状态。 ✴

### 在 Java 中，static 内部类没有这种附加指针， 这样的内部类与 C++ 中的嵌套类很相似。

### -> P244

## 6.4.1 使用内部类访问对象状态

### 278. 内部类的语法比较复杂。 -> P244

### 279. 

```java
public class TalkingClock
{
	private int interval:
	private boolean beep;
	
	public TalkingClock(int interval, boolean beep) { . . . }
	public void start() { . . . }
	
	public class TimePrinter implements ActionListener
		// an inner class
	{
	. . .
	}
}
```

### 需要注意， 这里的 TimePrinter 类位于 TalkingClock类内部。这并不意味着每个 TalkingClock 都有一个 TimePrinter 实例域 ， 如前所示， TimePrinter 对象是由 TalkingClock类的方法构造。 ✡

### -> P244

### 280. 下面是 TimePrinter 类的详细内容。需要注意一点，actionPerformed 方法在发出铃声之前 检查了 beep 标志。

```java
public class TimePrinter implements ActionListener
{
	public void actionPerformed(ActionEvent event)
	{
		System.out.println("At the tone, the time is " + new Date());
		if (beep) Toolkit.getDefaultToolkit().beep();
	}
}
```

### 令人惊讶的事情发生了。 TimePrinter 类没有实例域或者名为 beep 的变量，取而代之的是 beep 引用了创建 TimePrinter 的 TalkingClock 对象的域。 这是一种创新的想法。从传统意义 上讲，一个方法可以引用调用这个方法的对象数据域。内部类既可以访问自身的数据域，也 可以访问创建它的外围类对象的数据域。

### 为了能够运行这个程序， 内部类的对象总有一个隐式引用， 它指向了创建它的外部类对 象。如图 6-3 所示。

![Java核心技术（卷一）内部类对象拥有一个外围类对象的引用](F:\笔记\Java核心技术\Java核心技术（卷Ⅰ）\Java核心技术（卷一）内部类对象拥有一个外围类对象的引用.png)

### 这个引用在内部类的定义中是不可见的。然而， 为了说明这个概念， 我们将外围类对象 的引用称为 outer。于是 actionPerformed 方法将等价于下列形式：

```java
public void actionPerformed(ActionEvent event)
{
	System.out.println("At the tone, the time is " + new Date());
	if (outer.beep) Toolkit.getDefaultToolkit().beep();
}
```

### 外围类的引用在构造器中设置。编译器修改了所有的内部类的构造器， 添加一个外围类 引用的参数。因为 TimePrinter 类没有定义构造器，所以编译器为这个类生成了一个默认的构 造器，其代码如下所示：

```java
public TimePrinter(TalkingClock clock) // automatically generated code
{
	outer = clock;
}
```

### 请再注意一下， outer 不是 Java 的关键字。我们只是用它说明内部类中的机制。 ✡

### 当在 start 方法中创建了 TimePrinter 对象后， 编译器就会将 this 引用传递给当前的语音 时钟的构造器：

```java
ActionListener listener = new TimePrinter(this); // parameter automatically added
```

### -> P245

---

### 281. 下面我们再看一下访问控制。如果有 一个 TimePrinter 类是一个常规类，它就需要通过 TalkingClock 类的公有方法访问 beep 标志， 而使用内部类可以给予改进， 即不必提供仅用于访问其他类的访问器。 ❇

### 282. TimePrinter 类声明为私有的。这样一来， 只有 TalkingClock 的方法才能够构造 TimePrinter 对象。只有内部类可以是私有类，而常规类只可以具有包可见性，或公有可见性。 ✴ -> P245

## 6.4.2 内部类的特殊语法规则

### 283. 事实上，使用外围类引用的 正规语法还要复杂一些。表达式

```java
OuterClass.this
```

### 表示外围类引用。例如，可以像下面这样编写 TimePrinter 内部类的 actionPerformed方法：

```java
public void actionPerformed(ActionEvent event)
{
	. . .
	if (TalkingClock.this.beep) Toolkit.getDefaultToolkit().beep();
}
```

### 反过来，可以采用下列语法格式更加明确地编写内部对象的构造器：

```java
outerObject.new InnerClass(construction parameters)
```

### 例如，

```java
ActionListener listener = this.new TimePrinter();
```

### 在这里，最新构造的 TimePrinter 对象的外围类引用被设置为创建内部类对象的方法中的 this 引用。这是一种最常见的情况。通常，this 限定词是多余的。不过，可以通过显式地命名 将外围类引用设置为其他的对象。

### 例如， 如果 TimePrinter 是一个公有内部类，对于任意的语 音时钟都可以构造一个 TimePrinter：

```java
TalkingClock jabberer = new TalkingClock(1000, true);
TalkingClock.TimePrinter listener = jabberer.new TimePrinter()；
```

### 需要注意， 在外围类的作用域之外，可以这样引用内部类：✡

```java
OuterClass.InnerClass
```

### -> P247

---

### 284. 内部类中声明的所有静态域都必须是 final。原因很简单。我们希望一个静态域只 有一个实例， 不过对于每个外部对象， 会分别有一个单独的内部类实例。如果这个域不 是 final , 它可能就不是唯一的。 ❇ -> P247

### 285. 内部类不能有 static 方法。Java 语言规范对这个限制没有做任何解释。也可以允许有 静态方法，但只能访问外围类的静态域和方法。显然，Java 设计者认为相对于这种复杂 性来说， 它带来的好处有些得不偿失。 ✴ -> P247

## 6.4.3 内部类是否有用、必要和安全

### 286. 当在 Java 1.1 的 Java语言中增加内部类时，很多程序员都认为这是一项很主要的新特性， 但这却违背了 Java 要比 C++ 更加简单的设计理念。内部类的语法很复杂（可以看到，稍后介 绍的匿名内部类更加复杂 )。它与访问控制和安全性等其他的语言特性的没有明显的关联。 -> P248

### 287. 内部类是一种编译器现象， 与虚拟机无 关。编译器将会把内部类翻译成用 $ (美元符号）分隔外部类名与内部类名的常规类文件， 而 虚拟机则对此一无所知。 -> P248 ✳

### 288. 由于内部类拥有访问特权， 所以与常规类比较起来功能更加强大。 ✡ -> P249

### 289. 这样做不是存在安全风险吗？ 这种担心是很有道理的。任何人都可以通过调用 accessSO 方法很容易地读取到私有域 beep。当然， access$0 不是 Java 的合法方法名。但熟悉类文件结 构的黑客可以使用十六进制编辑器轻松地创建一个用虚拟机指令调用那个方法的类文件。由 于隐秘地访问方法需要拥有包可见性，所以攻击代码需要与被攻击类放在同一个包中。

### 总而言之，如果内部类访问了私有数据域， 就有可能通过附加在外围类所在包中的其他类访问它们，但做这些事情需要高超的技巧和极大的决心。程序员不可能无意之中就获得对 类的访问权限，而必须刻意地构建或修改类文件才有可能达到这个目的。

### -> P250

## 6.4.4 局部内部类

### 290. 如果仔细地阅读一下 TalkingClock 示例的代码就会发现， TimePrinter 这个类名字只在 start 方法中创建这个类型的对象时使用了一次。

### 当遇到这类情况时， 可以在一个方法中定义局部类。

```java
public void start()
{
	class TimePrinter implements ActionListener
	{
		public void actionPerformed(ActionEvent event)
		{
			System.out.println("At the tone, the time is " + new Date())；
			if (beep) Toolkit.getDefaultToolkit().beep();
		}
	}
	ActionListener listener = new TimePrinter();
	Timer t = new Timer(interval, listener);
	t.start();
}
```

### 局部类不能用 public 或 private 访问说明符进行声明。它的作用域被限定在声明这个局部 类的块中。

### 局部类有一个优势， 即对外部世界可以完全地隐藏起来。 即使 TalkingClock 类中的其他 代码也不能访问它。除 start 方法之外， 没有任何方法知道 TimePrinter 类的存在。 ✡

### -> P250

## 6.4.5 由外部方法访问变量

### 291. 与其他内部类相比较，局部类还有一个优点。它们不仅能够访问包含它们的外部类， 还 可以访问局部变量。不过，那些局部变量必须事实上为 final。这说明， 它们一旦赋值就绝不 会改变。 ✡-> P250

### 292. 局部类的方法只可以引用定义为 final 的局部变量。 -> P252 ❇

### 293. 有时，final 限制显得并不太方便。例如，假设想更新在一个封闭作用域内的计数器。这 里想要统计一下在排序过程中调用 compareTo 方法的次数。

```java
int counter = 0;
Date[] dates = new Date[100];
for (int i = 0; i < dates.length; i++)
	dates[i] = new Date()
		{
			public int compareTo(Date other)
			{
				counter++; // Error
				return super.conpareTo(other);
			}
		}；
Arrays.sort(dates);
System.out.println(counter + " comparisons.");
```

### 由于清楚地知道 counter 需要更新， 所以不能将 counter 声明为 final。 由于 Integer 对象 是不可变的， 所以也不能用 Integer 代替它。补救的方法是使用一个长度为 1 的数组：

```java
int[] counter = new int[1];
for (int i = 0; i < dates.length; i++)
	dates[i] = new Date()
		{
			public int compareTo(Date other)
			{
				counter[0]++;
				return super.compareTo(other);
			}
		}；
```

### 在内部类被首次提出时，原型编译器对内部类中修改的局部变量自动地进行转换。不 过， 后来这种做法被废弃。毕竟， 这里存在一个危险。同时在多个线程中执行内部类中的代 码时， 这种并发更新会导致竞态条件—有关内容参见第 14 章。 ✴

### -> P252

## 6.4.6 匿名内部类

### 294. 将局部内部类的使用再深人一步。 假如只创建这个类的一个对象，就不必命名了。这种类被称为匿名内部类（anonymous inner class)。

```java
public void start(int interval, boolean beep)
{
	ActionListener listener = new ActionListener()
	{
		public void actionPerformed(ActionEvent event)
		{
			System.out.println("At the tone, the time is " + new Date())；
			if (beep) Toolkit.getDefaultToolkit().beep();
		}
	}；
	Timer t = new Timer(interval, listener);
	t.start()；
}
```

### 这种语法确实有些难以理解。它的含义是：创建一个实现 ActionListener 接口的类的新 对象，需要实现的方法 actionPerformed 定义在括号 {  } 内。

### 通常的语法格式为：

```java
new SuperType(construction parameters)
	{
		inner class methods and data
	}
```

### 其中， SuperType 可以是 ActionListener 这样的接口， 于是内部类就要实现这个接口。 SuperType 也可以是一个类，于是内部类就要扩展它。 ✡

### 由于构造器的名字必须与类名相同， 而匿名类没有类名，所以，匿名类不能有构造器。 取而代之的是，将构造器参数传递给超类（ superclass) 构造器。尤其是在内部类实现接口的 时候， 不能有任何构造参数。不仅如此，还要像下面这样提供一组括号：

```java
new InterfaceType()
	{
		methods and data
	}
```

### 请仔细研究一下，看看构造一个类的新对象与构造一个扩展了那个类的匿名内部类的对 象之间有什么差别。 ❇

```java
Person queen = new Person("Mary");
	// a Person object
Person count = new Person("Dracula") { . . . };
	// an object of an inner class extending Person
```

### 如果构造参数的闭小括号后面跟一个开大括号， 正在定义的就是匿名内部类。 ✴

### -> P253

### 295. 多年来，Java 程序员习惯的做法是用匿名内部类实现事件监听器和其他回调。如今最好 还是使用 lambda 表达式。 ✡ -> P253

### 296. 下面的技巧称为“ 双括号初始化” （double brace initialization), 这里利用了内部类 语法。假设你想构造一个数组列表，并将它传递到一个方法：

```java
ArrayList<String> friends = new ArrayListo()；
friends.add("Harry")；
friends.add("Tony");
invite(friends);
```

### 如果不再需要这个数组列表，最好让它作为一个匿名列表。不过作为一个匿名列表， 该如何为它添加元素呢？ 方法如下：

```java
invite(new ArrayList<String>() {{ add("Harry"); add("Tony"); }});
```

### 注意这里的双括号。外层括号建立了 ArrayList 的一个匿名子类。内层括号则是一个 对象构造块（见第 4 章)。

### -> P255

### 297. 建立一个与超类大体类似（但不完全相同）的匿名子类通常会很方便。不过，对 于 equals 方法要特别当心。第 5 章中， 我们曾建议 equals 方法最好使用以下测试：

```java
if (getClass() != other.getClass()) return false;
```

### 但是对匿名子类做这个测试时会失败。

### -> P255 ✡

### 298. 生成曰志或调试消息时， 通常希望包含当前类的类名， 如：

```java
Systen.err.println("Something awful happened in " + getClass())；
```

### 不过，这对于静态方法不奏效。毕竟， 调用 getClass 时调用的是 this.getClass( ), 而 静态方法没有 this。所以应该使用以下表达式：

```java
new Object(){}.getCIass().getEnclosingClass() // gets class of static method
```

### 在这里，newObject0{} 会建立 Object 的一个匿名子类的一个匿名对象，getEnclosingClass 则得到其外围类， 也就是包含这个静态方法的类。

### -> P255 ✡

## 6.4.7 静态内部类

### 299. 有时候， 使用内部类只是为了把一个类隐藏在另外一个类的内部，并不需要内部类引用 外围类对象。为此，可以将内部类声明为 static, 以便取消产生的引用。 -> P255 ✡

### 300. 然而， 这个方法必须返冋两个数值， 为此， 可以定义一个包含两个值的类 Pair:

### 当然， Pair 是一个十分大众化的名字。在大型项目中， 除了定义包含一对字符串的 Pair 类之外， 其他程序员也很可能使用这个名字。这样就会产生名字冲突。解决这个问题的办法 是将 Pair 定义为 ArrayAlg 的内部公有类。此后， 通过 ArrayAlg.Pair 访问它：

### 不过， 与前面例子中所使用的内部类不同， 在 Pair 对象中不需要引用任何其他的对象， 为此， 可以将这个内部类声明为 static:

### -> P256

### 301. 当然， 只有内部类可以声明为 static。静态内部类的对象除了没有对生成它的外围类对象 的引用特权外， 与其他所冇内部类完全一样。在我们列举的示例中， 必须使用静态内部类， 这是由于内部类对象是在静态方法中构造的：

```java
public static Pair minmax(double[] d)
{
	. . .
	return new Pair(min, max);
}
```

### 如果没有将 Pair 类声明为 static, 那么编译器将会给出错误报告： 没有可用的隐式 ArrayAIg 类型对象初始化内部类对象。 ✡

### -> P257

### 302. 在内部类不需要访问外围类对象的时候， 应该使用静态内部类。 有些程序员用嵌 套类 （nested class) 表示静态内部类。 -> P257 ✡

### 303. 与常规内部类不同，静态内部类可以有静态域和方法。 -> P257 ✡

### 304. 声明在接口中的内部类自动成为 static 和 public 类。 -> P257 ✡

## 6.5 代理

### 305. 利用代理可以在运行时创建一个实现了一组给 定接口的新类 : 这种功能只有在编译时无法确定需要实现哪个接口时才冇必要使用。对于应用程序设计人员来说， 遇到这种情况的机会很少。然而，对于系统程序设计人员来说，代理带来的灵活性却十分重要。 -> P259 ✡

## 6.5.1 何时使用代理

### 306. 假设有一个表示接口的 Class 对象（有可能只包含一个接口，) 它的确切类型在编译时无 法知道。这确实有些难度。要想构造一个实现这些接口的类，就需要使用 newlnstance 方法 或反射找出这个类的构造器。但是， 不能实例化一个接口，需要在程序处于运行状态时定义 一个新类。

### 为了解决这个问题， 有些程序将会生成代码；将这些代码放置在一个文件中；调用编译 器；然后再加载结果类文件。很自然， 这样做的速度会比较慢，并且需要将编译器与程序放 在一起。而代理机制则是一种更好的解决方案。代理类可以在运行时创建全新的类。这样的 代理类能够实现指定的接口。尤其是，它具有下列方法：

- 指定接口所需要的全部方法。
- Object 类中的全部方法， 例如， toString、 equals 等。

### 然而，不能在运行时定义这些方法的新代码。而是要提供一个调用处理器（ invocation handler)。调用处理器是实现了 InvocationHandler 接口的类对象。在这个接口中只有一个方法： ✡

```java
Object invoke(Object proxy, Method method, Object[] args)
```

### 无论何时调用代理对象的方法，调用处理器的 invoke 方法都会被调用， 并向其传递 Method 对象和原始的调用参数。 调用处理器必须给出处理调用的方式。 ✡

### -> P259

## 6.5.2 创建代理对象

### 307. 要想创建一个代理对象， 需要使用 Proxy 类的 newProxylnstance 方法。 这个方法有三个 参数：

- 一个类加栽器（class loader ）。 作为 Java 安全模型的一部分， 对于系统类和从因特网 上下载下来的类，可以使用不同的类加载器。有关类加载器的详细内容将在卷 Ⅱ 第 9 章中讨论。目前， 用 null 表示使用默认的类加载器。
- 一个 Class 对象数组， 每个元素都是需要实现的接口。
- 一个调用处理器。

### 还有两个需要解决的问题。如何定义一个处理器？ 能够用结果代理对象做些什么？ 当 然， 这两个问题的答案取决于打算使用代理机制解决什么问题。使用代理可能出于很多原 因，例如：

- 路由对远程服务器的方法调用。
- 在程序运行期间，将用户接口事件与动作关联起来。
- 为调试， 跟踪方法调用。

### -> P259✡

### 308. 代理对象属于在运行时定义的类（它 有一个名字， 如 $Proxy0 ) 这 个 类 也 实 现 了 Comparable 接口。然而，它的 compareTo 方法调用了代理对象处理器的 invoke 方法。 -> P260 ✡

### 309. 前面已经讲过， 在 Java SE 5.0 中， Integer 类实际上实现了 Comparable 。然 而， 在运行时， 所有的泛型类都被取消， 代理将它们构造为原 Comparable 类的类对象。 -> P261 ✡

### 310. binarySearch 方法按下面这种方式调用：

```java
if (elements[i].compareTo(key) < 0) . . .
```

### 由于数组中填充了代理对象， 所以 compareTo 调用了 TraceHander 类中的 invoke 方法。 这个方法打印出了方法名和参数， 之后用包装好的 Integer 对象调用 compareTo。 -> P261 ✡

### 311. 注意， 即使不属于 Comparable 接口， toString 方法也被代理。在下一节中会看到， 有相当一部分的 Object 方法都被代理。 -> P261 ✡

## 6.5.3 代理类的特性

### 312. 需要记住， 代理类是在程序运行过程中创建的。然而， 一旦被创建， 就变成了常规类，与虚拟机中的任何其他 类没有什么区别。 -> P263 ✡

### 313. 没有什么区别。 所有的代理类都扩展于 Proxy 类。一个代理类只有一个实例域—调用处理器，它定义 在 Proxy 的超类中。 为了履行代理对象的职责，所需要的任何附加数据都必须存储在调用处 理器中。 -> P263

### 314. 所有的代理类都覆盖了 Object 类中的方法 toString、 equals 和 hashCode。如同所有的代 理方法一样，这些方法仅仅调用了调用处理器的 invoke。Object 类中的其他方法（如 clone 和 getClass) 没有被重新定义。 -> P263 ✡

### 315. 没有定义代理类的名字，Sun 虚拟机中的 Proxy类将生成一个以字符串 SProxy 开头的类名。 -> P263

### 316. 对于特定的类加载器和预设的一组接口来说，只能有一个代理类。 也就是说，如果使用 同一个类加载器和接口数组调用两次 newProxylustance方法的话， 那么只能够得到同一个类 的两个对象，也可以利用 getProxyClass方法获得这个类：

```java
Class proxyClass = Proxy.getProxyClass(null, interfaces);
```

### -> P263 ✡

### 317. 代理类一定是 public 和 final。如果代理类实现的所有接口都是 public， 代理类就不属于 某个特定的包；否则， 所有非公有的接口都必须属于同一个包，同时，代理类也属于这个包。 ->P263 ✡

### 318. 可以通过调用 Proxy 类中的 isProxyClass 方法检测一个特定的 Class 对象是否代表一个代 理类。 -> P263

## 第六章总结：

### 319. 接口、lambda 表达式和内部类是 经常使用的几个概念。然而，前面已经提到过，克隆和代理是库设计者和工具构造者感兴趣 的高级技术， 对应用程序员来说，它们并不十分重要。  -> P263 ✡

## 第七章、异常、断言和日志

### 320. 当程序遇到错误时，至少应该做到以下几点：

- 向用户通告错误；
- 保存所有的工作结果；
- 允许用户以妥善的形式退出程序。

### -> P264

## 7.1 处理错误

### 321. 如果由于出现错误而使得某些操作没有完成， 程序应该：

- 返回到一种安全状态，并能够让用户执行一些其他的命令；或者
- 允许用户保存所有操作的结果，并以妥善的方式终止程序。

### -> P264

### 322. 为了能够在程序中处理异常情况， 必须研究程序中可能会出现的错误和问题， 以及哪类 问题需要关注。

1. 用户输入错误。
2. 设备错误。
3. 物理限制：磁盘满了，可用存储空间已被用完。
4. 代码错误：硬件并不总是让它做什么，它就做什么。打印机可能被关掉了。网页可能临时性地不能浏 览。在一个任务的处理过程中，硬件经常出现问题。例如，打印机在打印过程中可能没有纸了。

### -> P265

---

# -> 从此开始，为我自己精心制作的笔记。 ★

## 7.1.1 异常分类

![Java核心技术（卷一）异常结构层次](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）异常结构层次.png)

### 323. 我的异常笔记

![异常笔记（ Myself ）](F:\笔记\Java核心技术\Java核心技术（卷一）\异常笔记（ Myself ）.png)

### Error补充：很少出现，如果出现，除了告知用户，并尽力安全的终止程序外，再也无能为力。 ★

### -> P266-267

### 324. 派生于 RuntimeException 的异常包含下面几种情况：

- 错误的类型转换。
- 数组访问越界。
- 访问 null 指针。

### 不是派生于 RuntimeException 的异常包括：

- 试图在文件尾部后面读取数据。
- 试图打开一个不存在的文件。
- 试图根据给定的字符串查找 Class 对象， 而这个字符串表示的类并不存在。

### “ 如果出现 RuntimeException 异常， 那么就一定是你的问题” 是一条相当有道理的规则。 ★

### -> P266

## 7.1.2 声明受查异常

### 325. 在方法的首部声明此方法可能抛出的异常

```java
class MyAnimation
{
	. . .
	public Image loadImage(String s) throws IOException
	{
		. . .
	}
}
```

### 若可能抛出多个异常，则需列出所有异常 ★

```java
class MyAnimation
{
	. . .
	public Image loadImage(String s) throws FileNotFoundException, EOFException
	{
		. . .
	}
}
```

### -> P268

---

### 326. 受查异常 -> 必须声明

### 		 非受查异常 -> 不可控制（Error）或者 应该避免发生（RuntimeException）

### -> P268

### 327. 如果基类声明了一个异常，那么他的派生类只能声明该异常或者该异常的子类，不能声明该异常的基类。特别是，如果超类方法没有声明异常，那么子类也不能声明任何异常。-> P269 ★

### 328. 抛出的异常可能是他本身，也可能是他的子类。 -> P269

### 329. 在 Java 中，没有 throws 说明符的方法将不能抛出任何受查异常。 -> P269 ★

## 7.1.3 如何抛出异常

### 330. 若是已经存在的异常类：

1. 找到一个合适的异常类。
2. 创建这个类的一个对象。
3. 将对象抛出。

### -> P270

### 331. 在 Java 中，只能抛出 Throwable 子类的对象。 -> P270 ★

## 7.1.4 创建异常类

### 332. 自定义异常类：只需定义一个派生于库中异常类的一个派生类，应该拥有一个默认构造器和一个带有详细信息的构造器（在调试中有用，超类 Throwable 中的 toString 方法可以打印出这些信息）。 -> P270

## 7.2 捕获异常

### 333. 能处理异常：捕获它；不能处理：传递它。 -> P272

### 334. 一个 try 语句块后面可以跟多个 catch 子句，若两个异常类的处理方法一样，则可以合并这两个 catch 子句。

```java
try
{
	code that might throw exceptions
}
catch (FileNotFoundException | UnknownHostException e)
{
	emergency action for missing files and unknown hosts
}
catch (IOException e)
{
	emergency action for all other I/O problems
}
```

### 这种情况下，异常变量隐含为 final 变量，并且异常类型彼此之间不存在子类关系。 ★

### 合并 catch 会使代码更简单、高效。

### -> P274

## 7.2.3 再次抛出异常与异常链

### 335. 若需再次抛出异常，强烈建议使用此包装技术 -> 将原始异常设置为新异常的 “ 原因 ” ： ★

```java
try
{
	access the database
}
catch (SQLException e)
{
	Throwable se = new ServletException ("database error");
	se.initCause(e);
	throw se;
}
```

### 优点：

1. 抛出新异常，并且不会丢失原异常的细节。
2. 若一个方法中发生了一个受查异常，而不允许抛出它，则可以捕获此异常，并用此方法将它包装成一个运行时异常。 ★

### -> P275

## 7.2.4 finally 子句

### 336. finally 子句的作用：解决资源回收问题。 -> P275

### 337. 不管是否有异常被捕获，finally 子句中的代码都被执行。 -> P275 ★

### 338. try 语句块执行流程 （ 我的笔记 ）

![try 语句块的执行流程（Myself）](F:\笔记\Java核心技术\Java核心技术（卷一）\try 语句块的执行流程（Myself）.png)

### -> P276

### 339. 建议的 try 语句块写法：

```java
InputStrean in = . . .;
try
{
	try
	{
		code that might throwexceptions
	}
	finally
	{
		in.close();
	}
}
catch (IOException e)
{
	show error message
}
```

### 内层 try 语句块的作用：确保关闭输入流。

### 外层 try 语句块的作用：报告错误。

### 优点：

1. 清楚。
2. 会报告 finally 子句中的错误。

### -> P277

### 340. 

```java
public static int f(int n)
{
	try
	{
		int r = n * n;
		return r;
	}
	finally
	{
		if (n == 2) return 0;
	}
}
```

### 在执行 try 语句中的 return 语句前，会执行 finally 子句， finally 中的 return 语句的返回值会覆盖掉原来的返回值。 ★

### -> P277

## 7.2.5 带资源的 try 语句 -> 需要关闭资源时尽可能的采用

### 341. 

```java
try (Resource res = . . .)
{
	work with res
}
```

### try块退出时，会自动调用 res.close() ，就好像使用了 finally 语句一样。 -> P279 ★

### 指定多个资源：

```java
try (Scanner in = new Scanner(new FileInputStream("usr/share/dict/words", "UTF-8"));
	PrintWriter out = new PrintWriter("out.txt"))
{
	while (in.hasNext())
		out.println(in.next().toUpperCase());
}
```

### -> P279

### 342. 带资源的 try 语句的作用：

- 当 try 语句块抛出一个异常， close 方法也抛出一个异常时，原来的异常将会丢失，而抛出 close 方法的异常。而采用带资源的 try 语句，原来的异常将被抛出，而 close 方法的异常会 “ 被抑制 ” 。 ★
- 那些 “ 被抑制 ” 的异常将被自动捕获，由 addSuppressed 方法增加到原来的异常，可以用 getSuppressed 方法查看。

### -> P279

### 343. 若带资源的 try 语句拥有 catch 子句和 finally 子句，它们将在资源关闭后执行。实际中一般不添加这些子句。 -> P279 ★

## 7.3 使用异常机制的技巧：

1. 异常处理不能代替简单的测试：小测试的效率更高。

小测试：646ms

```java
if (!is.empty()) s.pop();
```

异常处理：21739ms

```java
try
{
	s.pop();
}
catch (EmptyStackException e)
{
}
```

---

2. 不过分细化异常：将整个任务包装在 try 语句块中，出问题时，整个任务都可以取消；如果将任务细分，分别装入一个 try 语句块中，如果其中一个小任务出了问题，又会导致其他的一连串不应该发生的逻辑问题，代码也不够清晰。

3. 利用异常层次结构：寻找最适合的异常类。

4. 不要压制异常：不重要的异常将它关闭，重要的异常则处理。

```java
public Image loadImage(String s)
{
	try
	{
		// code that threatens to throw checked exceptions
	}
	catch (Exception e)
	{} // so there
}
```

---

5. “ 早抛出，晚捕获 ”。

### -> P283-285

## 7.4 使用断言

### 344. 断言的优点：在测试期间插入检查语句，代码发布时将这些语句自动删除。 -> P285

### 345. 断言的两种形式：

1. 

```java
assert 条件; // 若结果为 false ，抛出一个 AssertionError 异常。
```

2. 

```java
assert 条件 : 表达式; // 若结果为 false ，表达式被传入 AssertionError 的构造器，并转换成一个消息字符串
```

### 346. AssertionError 对象不储存表达式的值，所以不可能在以后得到它，“ 表达式 ” 部分的唯一目的是产生一个消息字符串。 -> P286 ★

## 7.4.2 启动和禁用断言：

- 启动：有类加载器的类：使用命令 -enableassertions 或 -ea ；没有类加载器的类（ “ 系统类 ” ）：-enablesystemassertions / -esa 。

- 禁用：有类加载器的类：使用命令 -disableassertions 或 -da ；没有类加载器的类（ “ 系统类 ” ）：-disenablesystemassertions / -dsa 。

### -> P286

## 7.4.3 使用断言完成参数检查

### 347. Java 中的 3 种处理系统错误的机制：

1. 抛出一个异常
2. 日志
3. 使用断言

### -> P287

### 348. 断言使用的时机：

1. 断言只应该用于在测试阶段确定程序内部的错误位置。 -> P287 ★
2. 当对此方法的约定存在前置条件时：

在方法注释中：

```java
@param a the array to be sorted (must not be null). // 括号中的内容即前置条件
```

此时应在方法的开头使用断言：

```java
assert a != null;
```

### 断言的缺点：当上述方法断言失败时，会出现难以预料的结果：有时抛出一个断言错误，有时产生一个 null 指针异常，这取决于类加载器的配置。 -> P288 ★

### 349. 断言和日志的总结：断言 是一种测试和调试阶段所使用的战术性工具; 而日志记录是一种在程序的整个生命周期都可 以使用的策略性工具。 -> P288

## 7.5 记录日志

### 350. 记录日志的作用：开销小，方便关闭和开启，能够过滤等，便于调试。 -> P289

### 351. 日志记录器级别：

- SEVERE
- WARNING
- INFO
- CONFIG
- FINE
- FINER
- FINEST

### 默认只记录前三个，记录其他级别需要设置。 -> P290 ★

### 352. 如果虚拟机对执行过程进行了优化，就得不到准确的调用信息，需要用 logp 方法获取调用类的方法的确切位置。 -> P290 ★

### 353. 日记记录的常见用途：记录那些不可预料的异常。 -> P291 ★

## 7.5.3 修改日志管理器配置

### 354. 日志系统的各种属性都可以通过编辑配置文件来修改。 -> P291 ★

## 7.6 调试技巧

1. 打印或记录任意变量的值：

```java
System.out.println("x=" + x);
或
Logger.getGlobal().info("x=" + x);
```

2. 在每一个类中放置一个单独的 main 方法。
3. JUnit 单元测试框架：http://junit.org
4. 用日志代理（ logging proxy ）截获方法调用，并记录日志，调用超类中的方法。例如，如果在调用 Random 类的 nextDouble 方法时出现了问 题， 就可以按照下面的方式，以匿名子类实例的形式创建一个代理对象：

```java
Random generator = new
	Random()
	{
		public double nextDouble()
		{
			double result = super.nextDouble()；
			Logger.getClobal().info("nextDouble: " + result);
			return result;
		}
	}；
```

5. 获得堆栈轨迹：

```java
try
{
	. . .
}
catch (Throwable t)
{
	t.printStackTrace()；
	throw t;
}
也可以不捕获异常，在代码的任意位置插入下面这条语句来获得堆栈轨迹
Thread.dumpStack();
```

6. 堆栈轨迹一般显示在 System.err 上，可以用 printStackTrace( PrintWriter s ) 方法将它发送到一个文件中，也可以用下面的方式将他捕获到一个字符串中：

```java
StringWriter out = new StringWriter();
new Throwable().printStackTrace(new PrintWriter(out));
String description = out.toString()；
```

7. 用下面的命令捕获错误流：

```bash
java MyProgram 2> errors.txt
```

​	   在同一个文件中同时捕获 System.err 和 System.out

```bash
java MyProgram 1> errors.txt 2>&1
```

8. 让堆栈轨迹出现在 System.err 中不太好，因为在客户端偶然看到这些消息会感到迷惑。应该将其记录到一个文件中。

    调用静态的 Thread.setDefaultUncaughtExceptionHandler 方法改变非捕获异常的处理器：

```java
Thread.setDefaultUncaughtExceptionHandler(
	new Thread.UncaughtExceptionHandler()
	{
		public void uncaughtException(Thread t, Throwable e)
		{
			save information in logfile
		}；
	})；
```

9. 用 -verbose 命令启动 Java 虚拟机，诊断由于类路径引发的问题。
10. 用 -Xlint 命令告诉编译器对一些普遍容易出现的代码问题进行检查。
11. 在 UNIX/Linux 环境下， 运行 ps 实用工具， 在 Windows 环境下，使用任务管理器。运行 jconsole 程序：

```bash
jconsole processID
```

www.oracle.com/technetwork/articles/java/jconsole-1564139.html

12. 用 jmap 获得一个堆的转储：

```bash
jmap -dump:format=b,file=dumpFileName processID
jhat dumpFileName
```

然后，通过浏览器进入 localhost:7000。

13. 用 -Xprof 标志运行 Java 虚拟机，剖析经常被调用的方法，将剖析信息发送给 System.out ，并显示哪些方法是由即时编译器编译的。

### -> P305-308

### 355. 编译器的 -X 选项并没有正式支持， 而且在有些 JDK 版本中并不存在这个选项。 可以运行命令 java -X 得到所有非标准选项的列表。 -> P308

## 第八章、泛型程序设计

### 356. 类型参数的优点：使程序具有更好的可读性和安全性。-> P310

### 357. 在 Java 库中， 使用变量 E 表示集合的元素类型， K 和 V 分别表示表的关键字与值的类型。T ( 需要时还可以用临近的 字母 U 和 S) 表示“ 任意类型”。 -> P312

## 8.3 泛型方法

```java
class ArrayAlg
{
	public static <T> T getMiddle(T... a)
	{
		return a[a.length / 2];
	}
}
```

### 358. 注意，类型变量放在修饰符（这里是 public static) 的 后面，返回类型的前面。 -> P313 ★

### 359. 当调用一个泛型方法时’ 在方法名前的尖括号中放人具体的类型：

```java
String middle = ArrayAlg.<String>getMiddle("]ohn", "Q.", "Public");
```

### 大多数情况下可以省略 <String> ，因为编译器能够推断。 ★

### -> P313

### 360. 获得编译器推断泛型方法类型的一个窍门：有目的地引入一个错误，然后研究错误信息。 -> P314 ★

## 8.4 类型变量的限定

### 361. 对类型变量 T 设置限定（bound）使其只接受实现了 Comparable 接口的类：

```java
public static <T extends Comparable> T min(T[] a) . . .
```

### 可以有多个限定：( 用 & 分隔限定类型 ) ★

```java
T extends Comparable & Serializable
```

### 限定中至多只有一个类，且必须是限定列表中的第一个。★

### -> P314-315

## 8.5 泛型代码和虚拟机

## 8.5.1 类型擦除

### 362. 虚拟机为泛型类型自动提供一个相应的原始类型（raw type）：删去类型参数后的泛型类型名。原始类型用第一个限定的类型变量来替换，如果没有限定就用 Object 替换。 -> P317 ★

### 363. 应将标签（tagging）接口（即没有方法的接口）放在边界列表的末尾来提高效率。（避免强制类型转换） -> P317 ★

## 8.5.3 翻译泛型方法

### 364. 编译器会合成桥方法来保持多态。-> P318-319

## 8.5.4 调用遗留代码

### 365. 可以方法之前利用注解（annotation）消除警告，关闭对方法中代码的检查。 -> P320

## 8.6  约束与局限性

## 8.6.1 不能用基本类型实例化类型参数

### 366. 没有 Pair<double>，只有 Pair<Double>。因为类型擦除后，Pair 类含有 Object 类型的域，而 Object 不能储存 double 值。-> P320 ★

## 8.6.2 运行时类型查询只适用于原始类型

### 367. 所有的类型查询只产生原始类型，因为虚拟机中的对象总有一个特定的非泛型类型。 -> P321 ★

```java
if (a instanceof Pair<String>) // Error
if (a instanceof Pair<T>) // Error
Pair<String> p = (Pair<String>) a; // Warning--can only test that a is a Pair
```

### 用 instanceof 或者强制类型转换只能测试 a 是否为任意类型的一个Pair。

### getClass 方法也总是返回原始类型：

```java
Pair<String> stringPair = . . .;
Pair<Employee> employeePair = . . .;
if (stringPair.getClass() == employeePair.getClass()) // they are equal
```

### 结果为 true ，因为都返回 Pair.class。

### -> P321

## 8.6.3 不能创建参数化类型的数组

```java
Pair<String>[] table = new Pair<String>[10]; // Error
```

### 擦除后，table 类型为 Pair[ ] 。可以转换为 Object[ ]。

### 因为数组会记住它的元素类型，如果试图储存其他类型的元素，就会抛出 ArrayStoreException 异常，所以不能创建参数化类型的数组。 -> P321 ★

### 368. 收集参数化类型对象的安全而有效的方法：使用 ArrayList：

```java
ArrayList<Pair<String>>
```

## 8.6.4 Varagrs 警告

### 369. 可以使用 @SafeVaragrs 标注来消除创建泛型数组的有关限制。 -> P322

```java
@SafeVarargs
public static <T> void addAll(Collection<T> coll, T... ts)
```

---

## 8.6.5 不能实例化类型变量

### 370. 不能使用像 new T(...) newT[...] 或 T.class 这样的表达式：(T被擦除为 Object，而本意肯定不希望调用 new Object())

```java
public Pair() { first = new T(); second = new T(); } // Error
```

### 解决办法：提供一个构造器表达式。

```java
Pair<String> p = Pair.makePairCString::new);
```

### makePair 方法接收一个 Supplier<T>，这是一个函数式接口，表示一个无参数而且返回 类型为 T 的函数：

```java
public static <T> Pair<T> makePair(Supplier<T> constr)
{
	return new Pair<>(constr.get(), constr.get())；
}
```

## 8.6.6 不能构造泛型数组

### 371.

```java
public static <T extends Comparable> T[] minmax(T[] a) { T[] mm = new T[2]; . . . } // Error
```

### 类型擦除会让这个方法永远构造 Comparable[2] 数组。 -> P323

### 如果数组仅仅作为一个类的私有实例域， 就可以将这个数组声明为 Object[]，并且在获 取元素时进行类型转换。

```java
public class ArrayList<E>
{
	private Object[] elements;
	. . .
	@SuppressWarnings("unchecked") public E get(int n) { return (E) elements[n]; }
	public void set(int n , E e) { elements[n] = e; } // no cast needed
}
```

### 实际的实现没有这么清晰：

```java
public class ArrayList<E>
{
	private E[] elements;
	. . .
	public ArrayList() { elements = (E[]) new Object[10]; }
}
```

### 这里， 强制类型转换 E[ ] 是一个假象， 而类型擦除使其无法察觉。 -> P324 ★

## 8.6.7 泛型类的静态上下文中类型变量无效

### 372. 

```java
public class Singleton<T>
{
	private static T singleInstance; // Error
	
	public static T getSingleInstance() // Error
	{
		if (singleinstance == null) construct new instance of T
		return singleInstance;
	}
}
```

### 类型擦除 之后， 只剩下 Singleton 类，它只包含一个 singlelnstance 域。 -> P325

## 8.6.8 不能抛出或捕获泛型类的实例

### 373. 甚至泛型类扩展 Throwable 都是不合法的。 -> P325 ★

```java
public class Problem<T> extends Exception { /* . . . */ } // Error--can't extend Throwable
```

### catch 子句中不能使用类型变量。

```java
public static <T extends Throwable> void doWork(Class<T> t)
{
	try
	{
		do work
	}
	catch (T e) // Error--can 't catch type variable
	{
		Logger.global.info(...)
	}
}
```

### 不过， 在异常规范中使用类型变量是允许的。

```java
public static <T extends Throwable> void doWork(T t) throws T // OK
{
	try
	{
		do work
	}
	catch (Throwable realCause)
	{
		t.initCause(real Cause);
		throw t;
	}
}
```

### -> P326

## 8.6.9 可以消除对受查异常的检查

### 374. 

```java
@SuppressWamings("unchecked")
public static <T extends Throwable> void throwAs(Throwable e) throws T
{
	throw (T) e;
}
```

### 假设这个方法包含在类 Block 中， 如果调用

```java
Block.<RuntimeException>throwAs(t);
```

### 编译器就会认为 t 是一个非受查异常。

### -> P326

## 8.6.10 注意擦除后的冲突

### 375. 下述代码是非法的：(合成的桥方法会冲突)

```java
class Employee implements Coinparab1e<Emp1oyee> { . . . }
class Manager extends Employee implements Comparable<Manager>
	{ . . . } // Error
```

### Manager 会实现 Comparable 和 Comparable, 这是同一接口的不同参数化。

### -> P328

## 8.7 泛型类型的继承规则

### 376. Pair<Manager> 与 Pair<Employee> 没有关系，不能将 Pair<Manager> 转换为(赋值给) Pair<Employee>。-> P328 ★

![Java核心技术（卷一）pair 类之间没有继承关系](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）pair 类之间没有继承关系.png)

---

### 377. 泛型与 Java 数组之间的重要区别：★

### 可以将一个 Manager□ 数组賦给一个 类型为 Employee[] 的变量，然而，数组带有特别的保护。如果试图将一个低级别的雇员存储到 employeeBuddies[0]， 虚拟机将会抛出 ArrayStoreException 异常。 -> P329 ★

### 378. 泛型类可以扩展或实现其他的泛型类：例如，ArrayList<T> 类实现 List<T> 接口(即一个 ArrayList<T> 可以被转换为一个 List<Manager>)。

![Java核心技术（卷一）泛型列表类型中子类型间的关系](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）泛型列表类型中子类型间的关系.png)

---

## 8.8 通配符类型

### 379. 通配符的子类型限定：Pair<? extends Employee>，其方法似乎是这样的，

```java
? extends Employee getFirst()
void setFirst(? extends Employee)
```

### 将不能调用 setFirst 方法，因为编译器只知道需要某个 Employee 的子类型，但不知道 具体是什么类型。它拒绝传递任何特定的类型。比如，如果传入的参数类型为 Manager ，？可能是 Manager 的子类，会抛出类型转换异常。★

### 使用 getFirst 方法就不存在这个问题：无论 getFirst 的返回值是什么类型，都是 Employee 的子类，虽然不确定，但完全可以将其赋值给一个 Employee 的引用。★

### -> P331

### 380. 通配符的超类型限定(supertype bound)：Pair<? super Manager> 有方法

```java
void setFirst(? super Manager)
? super Manager getFirst()
```

### 与其子类型限定相反：编译器无法知道 setFirst 方法 的具体类型， 因此调用这个方法时不能接受类型为 Employee 或 Object 的参数（？的类型可能是它们的子类，会发生类型转换异常），因此只能传递 Manager 类型的对象，或者某个子类型（如 Executive) 对象。★

### 如果调用 getFirst, 不能 保证返回对象的类型。只能把它赋给一个 Object。

### 381. 通配符限定的总结：带有超类型限定的通配符可以向泛型对象写人，带有子类型限定的通配符可 以从泛型对象读取。 -> P332 ★

## 8.8.3 无限定通配符

### 382. Pair<?> 有以下方法：

```java
? getFirst()
void setFirst(?)
```

### getFirst 的返回值只能赋给一个 Object。

### setFirst 方法不能被调用， 甚至不能用 Object 调 用。(？可能是你传递任意一个参数的类型的子类，会引发类型转换异常)。

### 可以调用 setFirst(null)。

### -> P334

### 383. Pair<?> 和 Pair 本质的不同：可以用任意 Object 对象调用原始 Pair 类的 setObject 方法。 -> P334

### 384. 对于一些简单的操作，使用通配符的版本可读性比使用泛型更强。

```java
public static boolean hasNulls(Pair<?> p)
{
	return p.getFirst() == null || p.getSecond() == null;
}
```

```java
public static <T> boolean hasNulls(Pair<T> p)
```

---

## 8.8.4 通配符捕获

### 385. 通配符不是类型变量， 因此， 不能在编写代码中使用 “ ？” 作为一种类型。 也就是说， 下述 代码是非法的：

```java
public static void swap(Pair<?> p) {
	? t = p.getFirst(); // Error
	p.setFirst(p.getSecond();
	p.setSecond(t);
}
```

### 解决方法：写一个辅助方法 swapHelper，用类型参数捕获通配符。

```java
public static <T> void swapHelper(Pair<T> p)
{
	T t = p.getFirst();
	p.setFirst(p.getSecond());
	p.setSecond(t);
}
```

### 由 swap 调用 swapHelper：

```java
public static void swap(Pair<?> p) { swapHelper(p); }
```

### 386. 通配符捕获只有在有许多限制的情况下才是合法的。编译器必须能够确信通配符表达的 是单个、 确定的类型。 例如， ArrayList<Pair<//T>> 中的 T 永远不能捕获 ArrayList<Pair</?>>中的通配符。数组列表可以保存两个 Pair<?>， 分别针对 ？的不同类型。 -> P335 ★

### 387. 获取更多关于泛型的信息：http://angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html -> P343 ★

## 第九章、集合

### 388. 使用接口类型存放集合的引用：当改变想法时，方便使用另一种实现。 -> P346 ★

### 389. 有一组以 Abstract 开头的类，如，AbstractQueue，是为类库的实现者设计的。如果想实现自己的队列类，就可以扩展 AbstactQueue 类，这比实现 Queue 接口中的所有方法要轻松得多。 -> P346

### 390. 集中不允许有重复的对象。 -> P347 ★

## 迭代器：

### 391. 遍历集合可以用迭代器，还可以用 “ for each ”循环（编译器将“ for each ”循环翻译为带有迭代器的循环）★。 在 Java SE 8中，还可以用迭代器调用 forEachRemaining 方法，需要提供一个 lambda 表达式。-> P348

### 392. 应该将 Java 迭代器认为是位于两个元素之间。 当调用 next 时，迭代器就越过下 一个元素，并返回刚刚越过的那个元素的引用（见图 9-3 ) 。 -> P348 ★

![Java核心技术（卷一）向前移动迭代器](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）向前移动迭代器.png)

---

### 393. 要想调用 remove 方法，必须先调用 next 方法越过该元素，不能连续两次调用 remove 方法。 -> P349 ★

### 394. 向集合中插入或删除元素（使用 add ，remove 方法等）是在迭代器位置的前面插入或删除。★

### 395. 在映射中需要用 put 方法插入，get 方法读取元素。 -> P352 ★

### 396. 可以用标记接口 RandomAccess 来测试一个集合是否支持高效的随机访问。 ★

```java
if (c instanceof RandomAccess)
{
	use random access algorithm
}
else
{
	use sequential access algorithm
}
```

### -> P353

---

### 397. 定义 equals 方法的注意事项：只要两个集包含同样的元素就认 为是相等的，而不要求这些元素有同样的顺序。

### 				 定义 hashcode 方法的注意事项：要保证包含相同元素的 两个集会得到相同的散列码。

### -> P353

## 具体的集合：

![Java核心技术（卷一）Java库中具体的集合](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）Java库中具体的集合.png)

![Java核心技术（卷一）集合框架中的类](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）集合框架中的类.png)

### -> P354

---

## 链表

### 355. 在 Java 中，所有链表实际上都是双向链接的 (doubly linked) ——即每个结点还存放着指向前驱结点的引用。 -> P355

### 356. 使用迭代器的规则（避免发生并发修改的异常）：可以根据需要给容器附加许多的 迭代器，但是这些迭代器只能读取列表。另外，再单独附加一个既能读又能写的迭代器。 -> P358 ★

### 357. 对于并发修改列表的检测有一个奇怪的例外：链表只负责跟踪对列表的结构性修 改，例如，添加元素、 删除元素。set 方法不被视为结构性修改。可以将多个迭代器附加 给一个链表，所有的迭代器都调用 set 方法对现有结点的内容进行修改。 -> P359

### 358. 绝对不应该使用这种让人误解的随机访问方法来遍历链表。下面这段代码的效率极低：

```java
for (int i = 0; i < list.size()；i++)
	do something with list.get(i);
```

### 每次査找一个元素都要从列表的头部重新开始搜索。LinkedList 对象根本不做任何缓存 位置信息的操作。

### -> P359 ★

### 359. get 方法做了微小的优化：如果索引大于 size() / 2 就从列表尾端开始搜索元素。 -> P359

### 360. previousIndex 和 nextIndex 方法的效率高，list.listIterator(n) 的效率低。 -> P359

## 数组列表

### 361. 在不需要同步时使用 ArrayList ，因为 Vector 的方法是同步的，可以由两个线程安全地访问一个 Vector 对象，但是，如果只有一个线程，代码要在同步操作上耗费大量的时间。 而 ArrayList 的方法不是同步的。 -> P363 ★

## 树集

### 362. 将一个元素添加到树中要比添加到散列表中慢，但是，与检查数 组或链表中的重复元素相比还是快很多。 -> P366

### 363. 如果不需要对数据进行排序， 就没有必要付出排序的开销。更重要的是，对于某些数据来说，对其排序要比散列函数更加困难。散列函数只是将对象适当地打乱存放， 而比 较却要精确地判别每个对象。 -> P367

## NavigableSet 接口

### 364.  这个接口增加了几个便于 定位元素以及反向遍历的方法。 -> P367

## 优先级队列

### 365. 元素可以按照任意的顺序插入，却总是按照排序的顺序 进行检索。 -> P371

## 映射

### 366. 散列或比较函数只能作用于键。与键关联的值不能进行散列或比较。 -> P372 ★

### 367. 要想检索一个对象， 必须使用（因而，必须记住）一个键。 -> P372

### 368. 键必须是唯一的。不能对同一个键存放两个值。如果对同一个键两次调用 put 方法， 第二个值就会取代第一个值。实际上，put 将返回用这个键参数存储的上一个值。 -> P372-373 ★

### 369. 要迭代处理映射的键和值， 最容易的方法是使用 forEach 方法。可以提供一个接收键和 值的 lambda 表达式。映射中的每一项会依序调用这个表达式。 -> P373 ★

```java
scores.forEach((k, v) ->
	System.out.println("key=" + k + ", value=" + v));
```

---

### 370. 键可以为 null ， 但值不能为 null 。-> P374 ★

## 更新映射项（难点）：

### 371. 例子：使用一个映射统计一个单词在文件中出现的频度。看到一个单词（word) 时，我 们将计数器增 1，如下所示：

```java
counts.put(word, counts.get(word) + 1);
```

### 这是可以的， 不过有一种情况除外：就是第一次看到 word 时。在这种情况下，get 会返 回 null, 因此会出现一个 NullPointerException 异常。

### 解决办法：

1. 使用 getOrDefault 方法：

```java
counts.put(word, counts.getOrDefault(word, 0)+ 1);
```

2. 首先调用 putlfAbsent 方法。只有当键原先存在时才会放入一个值。

```java
counts.putIfAbsent(word, 0);
counts.put(word, counts.get(word) + 1); // Now we know that get will succeed
```

3. 不过还可以做得更好。merge 方法可以简化这个常见的操作。如果键原先不存在，下面 的调用：

```java
counts.merge(word, 1, Integer::sum);
```

​	   将把 word 与 1 关联，否则使用 Integer::sum 函数组合原值和 1 (也就是将原值与 1 求和 )。

### -> P375

## 映射视图

### 372. 集合框架不认为映射本身是一个集合。（其他数据结构框架认为映射是一个键 / 值对 集合， 或者是由键索引的值集合。） 

###  不过， 可以得到映射的视图（ view ) —这是实现了 Collection 接口或某个子接口的对象。

### 有 3 种视图： 键集、 值集合（不是一个集） 以及键 / 值对集。键和键 / 值对可以构成一个 集， 因为映射中一个键只能有一个副本。

### 下面的方法会分别返回这 3 个视图。（条目集的元素是实现 Map.Entry 接口的类的对象。）

```java
Set<K> keySet()
Collection<V> values()
Set<Map.Entry<K, V>> entrySet()
```

### 如果在键集视图上调用迭代器的 remove方法， 实际上会从映射中删除这个键和与它关 联的值。不过，不能向键集视图增加元素。另外， 如果增加一个键而没有同时增加值也是没 有意义的。如果试图调用 add方法， 它会抛出一个 UnsupportedOperationException。条目集 视图有同样的限制，尽管理论上增加一个新的键 / 值对好像是有意义的。 ★

## 弱散列映射

### 373. 垃圾回收器跟踪活动的对象。只要映射对象是活动的， 其中的所有桶也是活动的， 它们不能被回收。因此， 需要由程序负责从长期存活的映射表中 删除那些无用的值。 或者使用 WeakHashMap 完成这件事情。当对键的唯一引用来自散列条目时， 这一数据结构将与垃圾回收器协同工作一起删除键 / 值对。 -> P377-378

## 链接散列集与映射

### 374. LinkedHashSet 和 LinkedHashMap类用来记住插人元素项的顺序。 -> P378 ★

### 375. 链接散列映射将用访问顺序， 而不是插入顺序， 对映射条目进行迭代。每次调用 get 或 put, 受到影响的条目将从当前的位置删除， 并放到条目链表的尾部（只有条目在链表中的位 置会受影响， 而散列表中的桶不会受影响。一个条目总位于与键散列码对应的桶中）。要项 构造这样一个的散列映射表， 请调用：

```java
LinkedHashMapcK, V>(initialCapacity, loadFactor, true)
```

### 访问顺序对于实现高速缓存的“ 最近最少使用” 原则十分重要。例如， 可能希望将访问 频率高的元素放在内存中， 而访问频率低的元素则从数据库中读取。当在表中找不到元素项 且表又已经满时， 可以将迭代器加入到表中， 并将枚举的前几个元素删除掉。这些是近期最 少使用的几个元素。

### 甚至可以让这一过程自动化。即构造一 LinkedHashMap 的子类，然后覆盖下面这个方法：

```java
protected boolean removeEldestEntry(Map.Entry<K， V> eldest)
```

### 每当方法返回 true 时，就添加一个新条目，从而导致删除 eldest 条目。例如，下面的高 速缓存可以存放 100 个元素：

```java
Map<K, V> cache = new
	LinkedHashMap<>(128, 0.75F, true)
	{
		protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
		{
			return size() > 100;
		}
	}();
```

### 另外，还可以对 eldest 条目进行评估，以此决定是否应该将它删除。例如，可以检査与 这个条目一起存在的时间戳。

### -> P379

## 枚举集与映射

### 376. EnumSet 是一个枚举类型元素集的高效实现。 由于枚举类型只有有限个实例， 所以 EnumSet 内部用位序列实现。如果对应的值在集中， 则相应的位被置为 1。

### EnumSet 类没有公共的构造器。可以使用静态工厂方法构造这个集：

```java
enum Weekday { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY };
EnumSet<Weekday> always = EnumSet.allOf(Weekday.class);
EnumSet<Weekday> never = EnumSet.noneOf(Weekday.class);
EnumSet<Weekday> workday = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);
EnumSet<Weekday> mwf = EnumSet.of(Weekday.MONDAY, Weekday.WEDNESDAY, Weekday.FRIDAY);
```

### 可以使用 Set 接口的常用方法来修改 EnumSet。

### -> P379

### 377. EnumMap 是一个键类型为枚举类型的映射。它可以直接且高效地用一个值数组实现。 在使用时， 需要在构造器中指定键类型：

```java
EnumMap<Weekday, Employee> personInCharge = new EnumMap<>(Weekday.class);
```

## 标识散列映射

### 378. 类 IdentityHashMap 有特殊的作用。在这个类中， 键的散列值不是用 hashCode 函数计算 的， 而是用 System.identityHashCode 方法计算的。 这是 Object.hashCode 方法根据对象的内 存地址来计算散列码时所使用的方式。而且， 在对两个对象进行比较时， IdentityHashMap 类 使用 ==, 而不使用 equals。

### 也就是说， 不同的键对象， 即使内容相同， 也被视为是不同的对象。 在实现对象遍历算 法（如对象串行化）时， 这个类非常有用， 可以用来跟踪每个对象的遍历状况。

## 视图与包装器

### 379. 通过使用视图 ( views) 可以获得其他的实现了 Collection 接口和 Map 接口的对象。

### 初看起来， 好像这个方法创建了一个新集， 并将映射中的所有键都填进 去，然后返回这个集。但是， 情况并非如此。取而代之的是：keySet 方法返回一个实现 Set 接口的类对象， 这个类的方法对原映射进行操作。这种集合称为视图。

## 轻量级集合包装器

### 380. Arrays 类的静态方法 asList 将返回一个包装了普通 Java 数组的 List 包装器。这个方法可 以将数组传递给一个期望得到列表或集合参数的方法。例如：

```java
Card[] cardDeck = new Card[52];
. . .
List<Card> cardList = Arrays.asList(cardDeck):
```

### 返回的对象不是 ArrayList。它是一个视图对象， 带有访问底层数组的 get 和 set 方 法。改变数组大小的所有方法（例如，与迭代器相关的 add 和 remove 方法）都会抛出一个 Unsupported OperationException 异常。

### -> P382

### 381. 视图的储存代价很小。 -> P382 ★

## 二分查找算法

### 382. 只有采用随机访问，二分査找才有意义。如果必须利用迭代方式一次次地遍历链表的一 半元素来找到中间位置的元素，二分査找就完全失去了优势。因此，如果为 binarySearch 算 法提供一个链表， 它将自动地变为线性查找。 -> P392 ★

## 简单算法

### 383. Java 库提供一些简单算法的原因：增加可读性。 -> P392 ★

## 集合与数组的转换

- 将数组转换为集合：可以使用 Arrays.asList 包装器，

```java
String() values = . . .;
HashSet<String> staff = new HashSet<>(Arrays.asList(values));
```

- 从集合得到数组会更困难一些。当然，可以使用 toArray 方法：

```java
Object[] values = staff.toArray();
```

​	  不过，这样做的结果是一个对象数组。尽管你知道集合中包含一个特定类型的对象，但 不能使用强制类型转换：★

```java
String[] values = (String[])staff.toArray()；// Error!
```

​	  实际上，必须使用 toArray 方法的一个变体形式，提供一个所需类型而且长度为 0 的数组。这样一来， 返回的数 组就会创建为相同的数组类型：★

```java
String[] values = staff.toArray(new String[0]);
```

​	  如果愿意，可以构造一个指定大小的数组，在这种情况下，不会创建新数组：

```java
staff.toArray(new String[staff.size()]);
```

### -> P395

### 384. ： 你可能奇怪为什么不能直接将一个 Class 对象（如 String.class) 传递到 toArray 方 法。原因是这个方法有“ 双重职责”， 不仅要填充一个已有的数组（如果它足够长)， 还 要创建一个新数组。 -> P395

## 第十四章、 并发

## 多线程及多线程程序的概念：

### 385. 一个程序同时执行多个任务。通常， 每一个任务称为一个线程（ thread), 它是线程控制的简称。可以同时运行一个以上线程的程 序称为多线程程序（multithreaded)。 -> P624

## 多进程与多线程：( myself ) ★

![Java核心技术（卷一）多线程与多进程的本质区别](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）多线程与多进程的本质区别.png)

### -> P624

### 386. 不要调用 Thread 类或 Runnable 对象的 run 方法。 直接调用 run 方法， 只会执行同 一个线程中的任务， 而不会启动新线程。应该调用 Thread.start 方法。这个方法将创建一 个执行 ran 方法的新线程。 -> P630 ★

### 387. 如果线程被阻塞，就无法检测中断状态，这就是产生 InterruptedException 异常的地方：当在一个被阻塞的线程（调用 sleep 或 wait) 上调用 interrupt 方法时，阻塞调用将会被 Interrupted Exception 异常中断。（存在不能被中断的阻塞 I/O 调用， 应该考虑选择可中断的调 用。有关细节请参看卷 n 的第 1 章和第 3 章。） -> P633 ★

### 388. 没有可以强制终止线程的方法，但可以用 interrupted 方法来请求终止线程。 -> P633 ★

### 389. 当线程的 run 方法执行方法体中最后一条语句后， 并经由执行 return 语句返冋时，或者出现了在方法中没有捕获的异常时，线程将终止。 -> P632-633

### 390. 如果在中断状态被置位时调用 sleep 方法，它不会休眠。相反，它将清除这一状态（ 中断状态 ）并拋出 IntemiptedException。 -> P633 ★

### 391. 有两个非常类似的方法，interrupted 和 islnterrupted。Interrupted 方法是一个静态方法， 它检测当前的线程是否被中断，并且清楚该线程的中断状态；islnterrupted 方法是一个实例方法，可用来检验是否有线程被中断。调 用这个方法不会改变中断状态。 -> P634 ★

### 392. 不应该将 InterruptedException 异常抑制在很低的层次上：

```java
void mySubTask()
{
	. . .
	try { sleep(delay); }
	catch (InterruptedException e) {} // Don't ignore!
	. . .
}
```

### 有两个更合理的选择：

1. ```java
    void mySubTask()
    {
    	. . .
    	try { sleep(delay); }
    	catch (InterruptedException e) { Thread.currentThread().interrupt(); } // 若捕获了此异常，说明在线程中断的状态下调用了 sleep 方法，休眠失败，并且清除了中断状态，可以使用该 interrrupt 方法来使线程重新进入中断状态。 ★
    	. . .
    }
    ```

2. 更好的选择：

    ```java
    void mySubTask() throws InterruptedException {
    	. . .
    	sleep(delay);
    	. . .
    }
    ```

## 线程状态

### 393. 一个可运行的线桿可能正在运行也可能没 有运行， 这取决于操作系统给线程提供运行的时间。 -> P635

### 394. 当线程处于被阻塞或等待状态时，它暂时不活动。它不运行任何代码且消耗最少的资 源。直到线程调度器重新激活它。细节取决于它是怎样达到非活动状态的。 -> P636

![Java核心技术（卷一）线程状态](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）线程状态.png)

---

## 线程属性

## 线程优先级：

### 395. 线程的优先级高度依赖系统。在 Oracle 为 Linux 提供的 Java 虚拟机中，线程的优先级被忽略——所有线程具有相同的优先级。 -> P638 ★

### 396. 不要将程序构建 为功能的正确性依赖于优先级。 -> P638 ★

### 397. 如果有几个高优先级的线程没有进入非活动状态，低优先级的线程可能永远也不会执行。 -> P638

## 守护线程：

### 398. 守护线程唯一的用途：为其他线程提供服务。  -> P639 ★

### 399. 当只剩下守护线程时， 虚拟机就退出了，由于如果只 剩下守护线程， 就没必要继续运行程序了。 -> P639

### 400. 守护线程应该永远不去访问固有资源， 如文件、 数据库，因为它会在任何时 候甚至在一个操作的中间发生中断。 -> P639 ★

## 同步

## 竞争条件详解

### 401. 不是原子操作的指令可能会被如下处理：

1. 将 accounts[to] 加载到寄存器。
2. 增 加 amount。
3. 将结果写回 accounts[to]。

### 现在，假定第 1 个线程执行步骤 1 和 2, 然后， 它被剥夺了运行权。假定第 2 个线程被 唤醒并修改了 accounts 数组中的同一项。然后，第 1 个线程被唤醒并完成其第 3 步。

### 这样， 这一动作擦去了第二个线程所做的更新。于是， 总金额不再正确。

![Java核心技术（卷一）同时被两个线程访问](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）同时被两个线程访问.png)

### -> P644-645

### 402. 我们的语句（ 如增值 ）会被翻译成若干个指令，执行它们的线程可以在任何一条指令点上被中断。 -> P645 ★

## 锁对象

### 403. 两种防止代码块受并发访问干扰的机制：

1. ReentrantLock 类：

    ```java
    myLock.lock(); // a ReentrantLock object
    try
    {
    	critical section
    }
    finally
    {
    	myLock.unlock()；// make sure the lock is unlocked even if an exception is thrown
    }
    ```

    把解锁操作括在 finally 子句之内是至关重要的。如果在临界区的代码抛出异常， 锁必须被释放。否则， 其他线程将永远阻塞。 -> P646 ★

    如果使用锁， 就不能使用带资源的 try 语句。首先， 解锁方法名不是 close。不过， 即使将它重命名， 带资源的 try 语句也无法正常工作。它的首部希望声明一个新变量。但 是如果使用一个锁， 你可能想使用多个线程共享的那个变量（而不是新变量）。 -> P646 ★

    ![Java核心技术（卷一）非同步线程与同步线程的比较](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）非同步线程与同步线程的比较.png)

    注意每一个 Bank 对象有自己的 ReentrantLock 对象。如果两个线程试图访问同一个 Bank 对象，那么锁以串行方式提供服务。但是， 如果两个线程访问不同的 Bank 对象， 每 一个线程得到不同的锁对象， 两个线程都不会发生阻塞。本该如此，因为线程在操纵不同的 Bank 实例的时候， 线程之间不会相互影响。 -> P647 ★

条件对象：现在，当账户中没有足够的余额时， 应该做什么呢？ 等待直到另一个线程向账户中注入 了资金。但是，这一线程刚刚获得了对 bankLock 的排它性访问， 因此别的线程没有进行存 款操作的机会。这就是为什么我们需要条件对象的原因。 -> P649

2. sychronized 关键字：

    ```java
    public synchronized void method()
    {
    	method body
    }
    
    // 等价于
    
    public void method()
    {
    	this.intrinsicLock.lock();
    	try
    	{
    		method body
    	}
    	finally { this.intrinsicLock.unlock(); }
    }
    ```

    理解这一代码的关键：必须了解每一个对象有一个内部锁， 并且该锁有一个内部条件。由锁来管理那些试图进入 synchronized 方法的线程，由条件来管理那些调用 wait 的线程。 -> P654 ★

    若将静态方法声明为 synchronized ，调用它，该方法获得相关的类对 象的内部锁。例如，如果 Bank 类有一个静态同步的方法，那么当该方法被调用时，Bankxlass 对象的锁被锁住。因此，没有其他线程可以调用同一个类的这个或任何其他的同步静态方法。 -> P654

    内部锁和条件的局限性：

    - 不能中断一个正在试图获得锁的线程。
    - 试图获得锁时不能设定超时。
    - 每个锁仅有单一的条件， 可能是不够的。

    一些建议：

    - 尽量不用 Lock/Condition 和 synchronized 关键字。
    - 如果非要用，若 synchronized 关键字适合你的程序，则使用它，可读性高，减少出错的机率。
    - 特别需要 Lock/Condition 结构的独有特性时才使用它。

### -> P654

## 同步阻塞

### 404. 有时程序员使用一个对象的锁来实现额外的原子操作，称为客户端锁定（ client-side locking) 。客户端锁定是非常脆弱的，通常不推荐使用。 -> P457

## Volatile 域

### 405. Brian Goetz 的 ”同步格言“ ：“ 如果向一个变量写入值， 而这个变量接下 来可能会被另一个线程读取， 或者，从一个变量读值， 而这个变量可能是之前被另一个 线程写入的， 此时必须使用同步”。 -> P658 ★

### 406. volatile 关键字为实例域的同步访问提供了一种免锁机制。如果声明一个域为 volatile , 那么编译器和虚拟机就知道该域是可能被另一个线程并发更新的。 -> P658

## final 变量

### 407. 

```java
final Map<String, Double> accounts = new HashMap<>()；
```

### 如果不使用 final，就不能保证其他线程看到的是 accounts 更新后的值，它们可能都只是 看到 null , 而不是新构造的 HashMap。 -> P659

## 线程局部变量

### 408. 有时可能要避免共享变量， 使用 ThreadLocal 辅助类为各个线程提供各自的实例，因为有时为一个变量单独使用同步开销很大。 -> P664 ★

### 409. 在多个线程中生成随机数也存在类似的问题。java.util.Random 类是线程安全的。但是如 果多个线程需要等待一个共享的随机数生成器， 这会很低效。可以使用 ThreadLocal 辅助类为各个线程提供一个单独的生成器， 不过 Java SE 7 还另外 提供了一个便利类：ThreadLocalRandom 。 -> P664

## 锁测试与超时

### 410. 线程在调用 lock 方法来获得另一个线程所持有的锁的时候，很可能发生阻塞。应该更加 谨慎地申请锁。tryLock 方法试图申请一个锁， 在成功获得锁后返回 true, 否则， 立即返回 false, 而且线程可以立即离开去做其他事情。 -> P665

### 411. lock 方法不能被中断。如果一个线程在等待获得一个锁时被中断，中断线程在获得锁之 前一直处于阻塞状态。如果出现死锁， 那么，lock 方法就无法终止。

### 然而， 如果调用带有用超时参数的 tryLock, 那么如果线程在等待期间被中断，将抛出 InterruptedException 异常。这是一个非常有用的特性，因为允许程序打破死锁。 ★

### lockInterruptibly 方法相当于一个将超时设为无限的 tryLcok 方法。

### -> P665

## 读/写锁：ReentrantReadWriteLock

### 412. 如果很多线程从一个数据结构读取数据而很少线程修改其中数据，它十分有用。在这种情况下， 允许对读者线程共享访问是合适的。 -> P666 ★

### 使用步骤：

1. 构 造 一 个 ReentrantReadWriteLock 对象：

    ```java
    private ReentrantReadWriteLock rwl = new ReentrantReadWriteLock():
    ```

2. 抽取读锁和写锁：

    ```java
    private Lock readLock = rwl.readLock();
    private Lock writeLock = rwl.writeLock();
    ```

3. 对所有的获取方法加读锁：

    ```java
    public double getTotalBalance()
    {
    	readLock.lock()；
    	try { . . . }
    	finally { readLock.unlock(); }
    }
    ```

4. 对所有的修改方法加写锁：

    ```java
    public void transfer(. . .)
    {
    	writeLock.lock();
    	try { . . . }
    	finally { writeLock.unlock(); }
    }
    ```

## 弃用 stop 和 suspend 方法的原因：

- stop：该方法终止所有未结束的方法， 包括 run方法。当线程被终止，立 即释放被它锁住的所有对象的锁。这会导致对象处于不一致的状态。例如， 假定 TransferThread 在从一个账户向另一个账户转账的过程中被终止，钱款已经转出，却没有转人目标账户，现在银 行对象就被破坏了。因为锁已经被释放，这种破坏会被其他尚未停止的线程观察到。

    当线程要终止另一个线程时， 无法知道什么时候调用 stop 方法是安全的， 什么时候导致 对象被破坏。因此，该方法被弃用了。在希望停止线程的时候应该中断线程， 被中断的线程 会在安全的时候停止。

- suspend：可能会导致死锁，当一个线程在条件锁中未达到条件而被阻塞，此时另一个线程企图进入该锁，如果对进入该锁的线程调用 suspend 方法将其挂起，就会导致该程序死锁 （myself）：被挂起的线程等着被恢复，而将其 挂起的线程等待获得锁。 ★

## 阻塞队列

![Java核心技术（卷一）阻塞队列的方法](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）阻塞队列的方法.png)

### 413. 如果将队列当作线程管理的工具来使用，使用 put 和 take。 -> P669

### 414. 通常，使用公平性会降低性能。 -> P669

## 线程安全的集合

### 415. 如果多线程要并发地修改一个数据结构， 例如散列表， 那么很容易会破坏这个数据结构。 -> P673

## 较早的线程安全集合

### 416. 从 Java 的初始版本开始，Vector 和 Hashtable 类就提供了线程安全的动态数组和散列表的 实现。现在这些类被弃用了， 取而代之的是 AnayList 和 HashMap 类。这些类不是线程安全 的，而集合库中提供了不同的机制。任何集合类都可以通过使用同步包装器（synchronization wrapper) 变成线程安全的：

```java
List<E> synchArrayList = Collections,synchronizedList(new ArrayList<E>());
Map<K, V> synchHashMap = Col1ections.synchronizedMap(new HashMap<K, V>())；
```

### 如果在另一个线程可能进行修改时要对集合进行迭代，仍然需要使用“ 客户端” 锁定：

```java
synchronized (synchHashMap)
{
	Iterator<K> iter = synchHashMap.keySet().iterator();
	while (iter.hasNext()) . . .
}
```

### 如果使用“ foreach” 循环必须使用同样的代码， 因为循环使用了迭代器。注意：如果在 迭代过程中，别的线程修改集合，迭代器会失效，抛出 ConcurrentModificationException 异 常。同步仍然是需要的， 因此并发的修改可以被可靠地检测出来。

### 最好使用 java.Util.COnciirrent 包中定义的集合， 不使用同步包装器中的。特别是， 假如它 们访问的是不同的桶， 由于 ConcurrentHashMap 已经精心地实现了，多线程可以访问它而且 不会彼此阻塞。有一个例外是经常被修改的数组列表。在那种情况下，同步的 ArrayList 可 以胜过 CopyOnWriteArrayList 。

### -> P680

## Callable 与 Future

### 417. Runnable 封装一个异步运行的任务，可以把它想象成为一个没有参数和返回值的异步方 法。Callable 与 Runnable 类似，但是有返回值。Callable 接口是一个参数化的类型， 只有一 个方法 call。

### 类型参数是返回值的类型。例如， Callable<\Integer> 表示一个最终返回 Integer 对象的异 步计算。

### Future 保存异步计算的结果。可以启动一个计算，将 Future 对象交给某个线程，然后忘 掉它。Future 对象的所有者在结果计算好之后就可以获得它。

### FutureTask 包装器是一种非常便利的机制， 可将 Callable转换成 Future 和 Runnable, 它 同时实现二者的接口。例如：★

```java
Callable<Integer> myComputation = . . .;
FutureTask<Integer> task = new FutureTask<Integer>(myConiputation);
Thread t = new Thread(task); // it's a Runnable
t.start()；
Integer result = task.get()；// it's a Future
```

### -> P681

## 执行器

### 418. 构建一个新的线程是有一定代价的， 因为涉及与操作系统的交互。如果程序中创建了大 量的生命期很短的线程，应该使用线程池（ thread pool)。将 Runnable 对象交给线程池， 就会有一个线程调用 run 方法。 当 run 方法退出 时，线程不会死亡，而是在池中准备为下一个请求提供服务。

### 另一个使用线程池的理由是减少并发线程的数目。创建大量线程会大大降低性能甚至使 虚拟机崩溃。

### -> P685

![Java核心技术（卷一）执行器工厂方法](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）执行器工厂方法.png)

## 线程池

### 419. 连接线程池时应该做的事：

1. 调用 Executors 类中静态的方法 newCachedThreadPool 或 newFixedThreadPool。
2. 调用 submit 提交 Runnable 或 Callable 对象。
3. 如果想要取消一个任务， 或如果提交 Callable 对象， 那就要保存好返回的 Future 对象。
4. 当不再提交任何任务时，调用 shutdown。

## 预订执行

### 420. ScheduledExecutorService 接口具有为预定执行（ Scheduled Execution) 或 重 复 执 行 任 务而设计的方法。它是一种允许使用线程池机制的 java.util.Timer 的泛化。

### 可以预定 Runnable 或 Callable 在初始的延迟之后只运行一次。也可以预定一个 Runnable 对象周期性地运行。

### -> P689

## Fork-Join 框架

### 421. 有些应用使用了大量线程， 但其中大多数都是空闲的。举例来说， 一个 Web 服务器可能 会为每个连接分别使用一个线程。另外一些应用可能对每个处理器内核分别使用一个线程， 来完成计算密集型任务， 如图像或视频处理。Java SE 7中新引入了 fork-join 框架，专门用来 支持后一类应用。假设有一个处理任务， 它可以很自然地分解为子任务， 如下所示：

```java
if (problemSize < threshold)
	solve problem directly
else
{
	break problem into subproblems
	recursively solve each subproblem
	combine the results
}
```

### -> P691 ★

### 422. 在后台， fork-join 框架使用了一种有效的智能方法来平衡可用线程的工作负载，这种方 法称为工作密取（work stealing)。每个工作线程都有一个双端队列 ( deque ) 来完成任务。一 个工作线程将子任务压人其双端队列的队头。（只有一个线程可以访问队头，所以不需要加 锁。）一个工作线程空闲时，它会从另一个双端队列的队尾“ 密取” 一个任务。由于大的子任 务都在队尾， 这种密取很少出现。 -> P692

## 可完成 Future

### 423. 利用可完成 fiiture，可以指定你希望做什么， 以及希望以什么顺序执行这些工作。当然， 这不会立即发生，不过重要的是所有代码都放在一处。 -> P694

## 同步器

### 424. java.util.concurrent 包包含了几个能帮助人们管理相互合作的线程集的类。如果有一个相互合作的线程集满足这些行为模式之一， 那么应该直接 重用合适的库类而不要试图提供手工的锁与条件的集合。 -> P696

![Java核心技术（卷一）同步器](F:\笔记\Java核心技术\Java核心技术（卷一）\Java核心技术（卷一）同步器.png)









