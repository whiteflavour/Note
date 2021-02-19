# Java 经验 ( myself )

## Java 基础

记得写main函数。

Java 中的按字典排序问题：大写字母排在前面（大写字母比小写字母小）例如：

```java
String[] words = {"Mary", "had", "a", "little", "lamb"};
// words[0].compareTo(words[2]) < 0

String[] words = {"mary", "had", "a", "little", "lamb"};
// words[0].compareTo(woeds[3]) > 0
```

---

Java 中 printf() 格式化 %n 的作用:

> 换行符，与 \n 不同，%n 具有跨平台的特性：★
>
> > 它告诉 Java 使用 System.getProperty("line.separator") 返回的值，这是当前系统的行分隔符。

> 在 Unix 系统中，换行符为 \n，在 Winows 中为 \r 或 \n，在 Mac 中为 \r。★

---

## IO 流：

使用 FileInuputStream 和 FileOutputStream 来复制一个文件时，FileOutputStream 的 write 方法不能使用 write(byte[])，否则文件打开会遇到错误：

```java
package com.google.demo.io_test;

import org.junit.Test;

import java.io.*;

public class IOTest {
	@Test
	public void copyTest() throws IOException {
		FileInputStream fileInputStream = new FileInputStream("F:\\1.docx");
		FileOutputStream fileOutputStream = new 		FileOutputStream("src\\com\\google\\demo\\io_test\\1.docx");
		byte[] buffer = new byte[1024];
		int bt;
		while ((bt = fileInputStream.read(buffer)) != -1) {
			// 不能使用 write(byte[]) 方法，否则打开文件时将会遇到错误。假设最后一次循环，一般不会刚好读完1024个字节数组的元素，即此缓冲未被填满，所以此时 bt 不为1024。如果不传入偏移量和长度，那么 write 方法会直接读取全部的缓冲，但是缓冲只有前一部分才有数据。
			fileOutputStream.write(buffer, 0, bt);
		}
		fileInputStream.close();
		fileOutputStream.close();
		}
}
```

---

使用缓冲区的方式读写文件的时候要记得刷新缓冲区，关闭流也行，不然就可能出现程序运行完之后数据还在缓冲区中的情况，这样的话要写入的数据就无法显示在目标文件中，因为它们还在缓冲区中。

---

## 多线程：

关于 run 与 start 方法：

run 方法并不会新开启一个线程，如果调用某线程的 run 方法，仅执行该方法而已；而 start 方法会新开启一个线程，并自动调用 run 方法。

---

## Lombok

lombok 包导入 IDEA 后无法使用的解决方法：利用搜索引擎找到官方 github 文档，里面有详细的 IDEA 如何设置的问题。

## Java Collections Frameworks

`Collections.copy()`方法，参数的 dest.size() 必须比 src.size() 大或者相等。

根据 Java 官方文档，Stack 类为 LIFO ( last-in-first-out )，而有一个更健全的类能够提供 LIFO ，即 ArrayDeque：

```java
Deque<Integer> stack = new ArrayDeque<>();
```

### LinkedList 问题

根据官方 JDK9 文档：

​		LinkedList `offer()`方法在超出容量限制的条件下，会比`add()`方法更可取，因为`add()`方法只能通过引发异常而无法插入元素。★

​		同理：在没有元素的情况下，`poll()`比`remove()`更好，此时`poll()`会返回 null ，而`remove()`直接报错——NoSuchElementException 。★

## Stream 问题

```java
// 这种情况下不会有任何的输出，此时应该用 forEach() 方法。★
Stream<String> stream = Stream.of("Go", "Fuck", "Yourself", "!!!");
stream.peek(e -> System.out.print(e + " "));
```

peek 不是终结操作，其返回值还是Stream，这种情况应该用`forEach()`。

Stream 分 **中间操作** 和 **终端操作**，（ foreach, collect count ） 属于终端操作。Java8 流中所有的操作都是**蓄而不发的**，只有执行`foreach`，`collect`等终结操作时，流的操作才会执行，而执行完终结性操作之后，流会自动关闭，不能再进行操作。★

`peek`会生成一个包含原Stream的所有元素的新Stream，同时会提供一个消费函数（Consumer实例），新 Stream 每个元素被消费的时候都会执行给定的消费函数。

就相当于我们只从流中取需要操作的那部分出来，然后只对那一部分进行操作。

### peek() 与 map() 的区别

`peek()`方法接受 Consumer，而`map()`接受 Function，而 Consumer 与 Function 的区别就是 Consumer 没有返回值，而 Function 有返回值，这也是`peek()`与`map()`的区别。即`map()`可以使用 Stream 的`collect()`方法来接收。★

















