# CSAPP (2022.1.4)

> 学习系统的唯一方法就是做(do)系统。

## 开始：

### 第一章、计算机系统漫游：

#### 1.9.1 Amdahl定律：

`Tnew = (1 - α)Told + (αTold) / k = Told[(1 - α) + α / k]`

加速比：`S = Told / Tnew = 1 / ((1 - α) + a / k)`

`Tnew`为改进后该部分程序运行的时间；`α`为该部分花的时间与总时间的比值。

> 该例子告诉我们：要想有整体的大幅改善，必须将整体都大幅改善，只做部分的大幅改善，整体的改善就相对小了。有点短板效应的意思。★★

## 第一部分：程序结构和执行：

### 第二章：信息的表示和处理：

#### 2.1.3 寻址和字节顺序：

计算机存储16进制数时有两种方法：如存储`0x01234567`

1. 大端法：
   | 地址范围 | 0x100 | 0x101 | 0x102 | 0x103 |      |
   | :------: | :---: | :---: | :---: | :---: | :--: |
   |   ...    |  01   |  23   |  45   |  67   | ...  |
   
2. 小端法：

   | 地址范围 | 0x100 | 0x101 | 0x102 | 0x103 |      |
   | :------: | :---: | :---: | :---: | :---: | :--: |
   |   ...    |  67   |  45   |  23   |  01   | ...  |

**可以通过强制类型转换(cast)或联合(union)来允许一种类型引用与它不同类型的对象。虽然大多应用编程不推荐，但是这对系统级编程非常重要：**

show_bytes.c:

```c
#include <stdio.h>

typedef  unsigned char *byte_pointer;

void show_bytes(byte_pointer start, size_t len) {
    size_t i;
    for (i = 0; i < len; ++i) {
        printf(" %.2x", start[i]);
    }
    printf("\n");
}

void show_int(int x) {
    show_bytes((byte_pointer) &x, sizeof(int));
}

void show_float(float x) {
    show_bytes((byte_pointer) &x, sizeof(float));
}

void show_pointer(void *x) {
    show_bytes((byte_pointer) &x, sizeof(void *));
}

void test_show_bytes(int val) {
    int ival = val;
    float fval = (float) ival;
    int *pval = &ival;
    show_int(ival);
    show_float(fval);
    show_pointer(pval);
}

int main() {
    test_show_bytes(12345);
}

/*
 * 输出结果：
 * 39 30 00 00
 * 00 e4 40 46
 * c8 18 e2 b5 f7 7f 00 00
 */
```

调用`show_bytes()`的那三个函数向其传送一个`&x`指针，它被强制类型转换了。

这种类型转换告诉编译器，程序应该把该指针看成指向一个**字节序列**，而非指向一个原始数据类型的对象。然后，这个指针会被看成是对象使用的最低字节地址。

**结果分析：**

`12345`十六进制表示为`003039`，可见 Mac 上是小端法表示。

#### 2.1.4 表示字符串：

文本数据比二进制数据有更强的平台独立性（跨平台）（同一编码下）。

#### 2.1.9 C语言中的位移运算：

1. 算术右移：负数时填`1`，正数时填`0`
2. 逻辑右移：填`0`

#### 2.2.3 补码编码：

用函数B2Tᴡ(Binary to Two's-complement)表示，长度为w。

**举例：**

```matlab
B2T₄([0001]) = -0*2³ + 0*2² + 0*2¹ + 1*2⁰ = 1
B2T₄([0101]) = -0*2³ + 1*2² + 0*2¹ + 1*2⁰ = 5
B2T₄([1011]) = -1*2³ + 0*2² + 1*2¹ + 1*2⁰ = -5
B2T₄([1111]) = -1*2³ + 1*2² + 1*2¹ + 1*2⁰ = -1
```

##### 反码：

最高位有效位的权是`-(2ᵂ⁻¹ - 1)`而不是`-2ᵂ⁻¹`，其他和补码一样。

##### 原码：

最高位是符号位。

#### 2.2.5 C 语言中的有符号数与无符号数:

在运算中，若一个参数为**有符号数**，而另一个为**无符号数**，那么有符号数会**隐式转换**为无符号数，并假设他们都是非负的。★

##### C语言中TMin的写法：

我们小心的将TMin₃₂写成`-2147483647-1`，而不是`-2147483647`或者`0x80000000`。

**C中的头文件<limits.h>：**

limits.h:

```c
#define INT_MAX 2147483647
#define INT_MIN (-INT_MAX - 1)
```

**原因：**

补码表示的不对称性和C语言的转换规则之间奇怪的交互。

#### 2.2.6 扩展一个数字的位表示：

**举例：**

```mathematica
[101] = -4 + 1 = -3
// 对他进行符号扩展：
[1101] = -8 + 4 + 1 = -3
```

**为什么？**

可以通过定义证明，将定义式展开，证明任意多个符号扩展等于不扩展。

> 关键点：`2ʷ - 2ʷ⁻¹ = 2ʷ⁻¹ `。★

**相当于：**

```mathematica
// 原来：
-2ʷ⁻¹ + ...

// 现在：
-2ʷ + 2ʷ⁻¹ + ...

// 就等于：
-2ʷ⁻¹

// 可以看到和原来相等
```

这就是二进制的神奇之处啊！！

##### 进制转换：short -> unsigned

先改变大小，再转换符号，即：`(unsigned) sx -> (unsigned)(int) sx`。

这个规则是C语言标准要求的。

#### 无符号数总结：

**避免使用无符号数：**

无符号运算容易出错，并且难以察觉。其实除C外很少有语言支持无符号整数，显然语言作者认为他的麻烦比好处要多得多。★

**无符号数的意义：**

当想把字仅仅看作是位的集合而没有数字意义时，它非常有用。

举例：

1. 布尔条件标记
2. 地址（对系统程序员很有帮助）
3. 实现模运算和多精度运算的数学包时，数字由字的数组表示

### 2.3 整数运算

#### 2.3.1 无符号加法：

**检测溢出：**

```mathematica
// 若：
s = x + y

// 当且仅当 s < x || s < y 时发生溢出
```

#### 2.3.3 补码的非：

##### 补码非的位级表示：

1. 全部取反，末尾加1(`-x = ~x + 1`)
2. 最后一个1前面全部取反

#### 2.3.6 乘以常数：

##### 编译器对乘法的优化：

以位移、加法和减法的组合来代替。

**原因：**乘法的代价比位移和加法要大得多

**举例：**

```c
y = x * 14;

// 14 = 2³ + 2² + 2¹
// =>

y = (x << 3) + (x << 2) + (x << 1);

// 或者 14 = 2⁴ - 2¹
// =>

y = (x << 4) - (x << 1);
```

### 2.4 浮点数：

浮点数不会关注太多精确性，把实现的速度和简便性看得更重要。

#### 2.4.2 IEEE浮点表示：

**1. 规格化的值：**

阶码：`E = e - Bias`

e：无符号数

Bias（偏置值）：`2ᴷ⁻¹ - 1`

尾数：`M = f + 1`（隐含1开头）

**2. 非规格化的值：（阶码域全为0）**

阶码：`E = 1 - Bias`

尾数：`M = f`（不隐含1开头）

**非规格化值的两个功能：**

1. 表示0，有+0.0（全0）和-0.0（符号位为1，其他为0），他们在某些方面被认为不同，而其他方面相同。
2. 表示非常接近于0.0的数。可能的数值分布均匀的接近于0.0

**3. 特殊值：（阶码全1）**

情况1. 小数域全0:

1. s=0, -> +∞
2. s=1, -> -∞

情况2. 小数域非0:

NaN。（结果不能是实数或无穷），如：√-1或∞-∞

#### 2.4.5 浮点运算：

可交换，但不可结合，也不可分配，如：

```mathematica
// 舍入
(3.14 + 1e10) - 1e10 = 0.0

3.14 + (1e10 - 1e10) = 3.14
```

### 第三章、程序的机器级表示：

#### 3.2.1 机器级代码：

**虚拟地址**提供的内存模型看上去是一个非常大的数组。

#### 3.2.3 关于格式的注解：

汇编代码有两种格式：

1. ATT
2. Intel

#### 3.4.1 操作数指示符：

操作数：

1. 立即数(immediate) -> `$+C语言整数`：表示常数
2. 寄存器 -> `rₐ表示任意寄存器a，R[rₐ]表示他的值`（将寄存器看作数组）：表示寄存器的内容
3. 内存引用 -> `Mb[Addr]表示从地址 Addr 开始的b个字节值的引用`：使用计算出来的地址访问某个内存位置。

#### 3.4.3 数据传送示例：

**C与汇编：**

1. 指针就是地址
2. 局部变量不在内存中，而在寄存器中。而访问寄存器要快得多。（利用好局部变量，可以提升程序性能，启下）

#### 3.6.5 用条件控制来实现条件分支：

##### 使用`goto`语句时不好的编程风格？

它会使代码难以阅读和调试。

##### C与汇编的`if-else`：

```c
if (test-expr)
  then-statement
else 
  else-statement
```

```assembly
t = test-expr
if (!t)
 goto false;
then-statement
goto done;
false:
 else-statement
done:
```

#### 3.6.6 用条件传送来实现条件分支

原始的条件操作：

控制的条件转移：条件满足，走一条路；不满足，走另一条。

但是在现代处理器上很**低效。**

**替代？**

数据的条件转移：计算条件操作的两种结果。

**举例：**

```c
long cmovdiff(long x, long y)
{
  // 数据替换
  long rval = y - x;
  long eval = x - y;
  
  long ntest = x >= y;
  
  // 数据替换
  if (ntest) rval = eval;
  return rval;
}

// 等价于 if (test) ...
//  			else ...
```

#### 3.7.1 运行时栈：

x86-64 的栈向低地址增长，即：上面是栈底，地址从下往上增大。★

#### 3.7.6 递归过程：

过程调用在栈中有自己的私有空间，不会相互影响。

**递归：**

先把已有的值保存在栈上，随后在返回前恢复。

递归调用自己与调用其他函数是一样的。★

#### 3.9 异质的数据结构：

1. 结构(structure)，即：结构体：将多个对象集合到一个单位中。
2. 联合(union)：允许用几种不同的类型来引用一个对象。

#### 3.9.2 联合：

**作用：**

能规避C的类型系统。

**举例：**

```c
union U3 {
  char c;
  int i[2];
  double v;
}
```

**各部分大小与对应的结构体：**

| 类型 | c | i | v | 大小 |
| :---: | :---: | :---: | :---: | :---: |
| S3 | 0 | 4 | 16 | 24 |
| U3 | 0 | 0 | 0 | 8 |

**原因：**

union U3* 的指针 p，p -> c、p -> i[0] 和 p->v 引用的都是数据结构的起始位置。★

联合的总大小等于最大的字段大小。★

#### 3.9.3 数据对齐：

Intel 建议数据对齐以提高系统性能。

**对齐原则：**任何K字节的基本对象的地址是K的倍数。

**强制对齐：**某些型号的Intel和AMD处理器对有些实现多媒体操作的SSE指令，若不对齐则不能正确执行。（不满足对齐要求的地址访问内存会导致异常，默认行为是终止程序）

#### 3.10.1 理解指针：

指针不是机器代码的一部分：是C提供的抽象，帮助程序员避免寻址错误。

#### 3.10.2 应用：使用GDB调试器：

**使用步骤：**

1. `objdump -d prog`
2. `gdb prog`

> DDD 是 GDB 的图形界面版本。

#### 3.10.3 内存越界引用和缓冲区溢出：（也是一种攻击方式）

使用C语言的库函数时要注意。

#### 3.10.4 对抗缓冲区溢出攻击：

##### 1. 栈随机化：

**原理：**

程序开始时，在栈上分配一段 0~n 字节之间的随机大小的空间。

**作用：**

使得攻击者不容易立马猜中某程序所使用的栈空间，增加了攻击难度。

**常见攻击方式：**

在攻击代码前面添加nop(读作"no op", no operation 的缩写 -> 作用：使程序计数器加一)，挨个个程序起始地址枚举；若猜中，程序滑过这个序列，到达攻击代码。（空操作雪橇(nop sled)，即程序滑过该序列(nop)。）

##### 2. 栈破坏检测：

**原理：**

在栈帧中任何局部缓冲区与栈状态之间存储一个特殊的**金丝雀(canary)值**，即**哨兵值(guard value)**；它随机产生，在恢复寄存器状态和从函数返回之前，检查它是否改变，若改变，则程序异常终止。

**优点：**

性能损失小。

##### 3. 限制可执行代码区域：

**优点：**

由硬件完成，效率上没有损失。

##### 总结：

**3种方法的共同点：**

1. 不需要程序员做任何特殊的努力
2. 带来的性能代价小。

> 记住，只能降低被攻击率，而不能防止，毕竟道高一尺，魔高一丈。

#### 3.10.5 支持变长栈帧：

`%rbp`中bp的由来：为了管理变长栈帧，x86-64代码使用寄存器`%rbp`作为帧指针（有时称基指针(**base pointer**))。

#### 3.11 浮点代码：

一些支持图形和图像处理的**媒体指令**，其**本意**是允许多个操作以并行模式执行。

### 第三章、处理器体系结构：

> 现代微处理器可以称得上时人类创造的最复杂的系统之一。

HCL(Hardware Control Language)硬件控制语言：用以描述处理器设计。

#### 4.1.3 指令编码：

每条指令的第一个字节表明指令的类型：高四位是代码部分，低四位时功能(function)部分。

**寄存器的编码：**不需要访问寄存器时，将寄存器ID置为0xF。

**整数的编码：**小端法。

**指令集的性质：**字节编码要有唯一的解释。**作用：**确保执行代码无二义性。

**RISC与CISC指令集：**

x86-64 -> 复杂指令集计算机 -> CISC（读作"sisk"）；精简指令集计算机 -> RISK (读作"risk")。

#### 4.1.5 Y86-64 程序：

**Y86-64 汇编代码中：**

以`.`开头的词是汇编器伪指令(assembler directives)，他们告诉汇编器调整地址，以便在那产生代码或插入数据。

#### 4.1.6 一些Y86-64指令的详情：

**注意：**

`pushq`指令会把栈指针减8，并将一个寄存器值写入内存中，因此，执行`pushq %rsp`时，处理器的行为是不确定的，因为要入栈的寄存器会被同一条指令修改。

此时有两种**约定：**

1. 压入`%rsp`的原始值
2. 压入它减8后的值

这与x86处理器型号有关。

**缺点：**

1. 降低了代码的可移植性
2. 增加了文档的复杂性

**总结：**

长远看来，提前了解细节，力争保持一致，能省去很多麻烦。

#### 4.2 逻辑设计和硬件控制语言HCL

电路设计的演变：**

画逻辑电路图(纸、笔) -> ...(计算机图形终端) -> 硬件描述语言(Hardware Description Language, HDL)。

**对比：编程的演变：**

汇编 -> 高级语言，用编译器产生机器代码。

**HDL：（最常用的是 Verilog，语法类似C；VHDL，类似Ada）**

描述硬件结构，而不是程序行为。（虽然看上去和编程语言类似）

现在已经有了将HCL直接翻译成Verilog的工具。

> 控制逻辑是设计微处理器最难的部分。

#### 4.2.2 组合电路和HCL布尔表达式：

**HCL与C的区别：**

**1. `=`：**

C：执行将结果存入内存中

HCL：给表达式一个名字

**2. 逻辑表达式：**

C：部分求值

HCL：简单的响应输入的变化（不部分求值）

#### 4.2.5 存储器和时钟：

**寄存器的区别：**

硬件：寄存器直接将它的输入和输出线连接到电路的其他部分 -> 物体

机器级编程：CPU中为数不多的可寻址的字，地址是寄存器ID。这些字通常存在寄存器文件中 -> CPU中寻址空间的地址

**时钟寄存器的作用：**

保存程序计数器（PC）、条件代码（CC）和程序状态（Stat）。

#### 4.3.3 SEQ的时序：

**原则：从不回读：**

处理器只读有关该指令的内容，该指令做了什么在执行该指令时不用管，以后需要用到时再读取。

**SEQ的缺点：**

太慢。(时钟必须非常慢，才能使一个信号在一个周期内传播所有的阶段)

#### 4.4 流水线通用原理：

**流水线的重要特性：**

提高了系统的吞吐量（单位时间内服务的顾客总数）

**缺点：**

轻微地增加了延迟（服务一个用户所需的时间）-> 多开了几个窗口，每个窗口都需要排队了，并且只能按特定顺序，一个个窗口挨着来，切换窗口也许要时间。

#### 4.4.1 计算流水线：

**增加吞吐量的代价：**

硬件增加，延迟增加（因为增加了寄存器，经过它也许要时间）

#### 4.4.3 流水线的局限性：

##### 1. 不一致的划分：

**硬件设计的挑战：**

因为流水线每个部分延迟不同的话，会导致延迟短的部分一直空闲，而延迟长的部分一直工作，效率就不高，所以应该将系统划分为具有相同延迟的阶段。但是并不容易，因为某些硬件，如ALU和内存，不能被划分为多个延迟较小的单元。

##### 2. 流水线过深：

会导致收益下降，因为延迟太高，而吞吐量相对没有翻倍。

**现代处理器：**

1. 每阶段延迟小 -> 处理器架构师将指令划分为非常简单的步骤。
2. 硬件延迟小 -> 电路设计者小心设计流水线处理器
3. 时钟延迟小 -> 芯片设计者小心设计时钟传播网络，保证时钟在整个芯片上同时改变

#### 4.5.1 SEQ+：重新安排计算阶段：

**SEQ+的特色：**

没有硬件寄存器来存放程序计数器，根据前一条指令保存下来的信息动态计算PC。

#### 4.5.2 插入流水线寄存器：

**流水线寄存器标号：（保存一条指令的各个阶段的状态）**

- F：作用：保存程序计数器的预测值
- D：作用：保存关于最新取出指令的信息，阶段：位于取值和译码阶段间，处理：由译码阶段处理
- E：作用：保存关于最新译码的指令和从寄存器文件读出的值的信息，阶段：位于译码和执行阶段之间，处理：由执行阶段处理
- M：作用：保存最新执行的指令的结果、关于用于处理条件转移的分支条件和分支目标的信息，阶段：位于执行和访存阶段之间，处理：由访存阶段处理
- W：作用：反馈路径将计算出来的值提供给寄存器文件写、当完成`ret`指令时，向PC选择逻辑提供返回地址，阶段：位于访存阶段和反馈路径之间

#### 4.5.4 预测下一个PC

**技术：**

分支预测。

研究表明，**总是选择分支**的预测策略，成功率约为60%。

**使用栈的返回地址预测：**

大多程序，预测返回值很容易，因为过程调用和返回成对出现，大多函数调用，会返回到调用后的那条指令。所以，可以利用这个属性，在取指单元中放入一个硬件栈，保存过程调用指令产生的返回地址，每次执行，将返回地址压栈，当取出返回地址时，弹栈作为预测值。高性能处理器会运用这个属性。★

#### 4.5.5 流水线冒险：

1. 数据相关：下一条指令会用到这一条指令计算出的结果
2. 控制相关：一条指令要确定下一条指令的位置，如：在执行跳转、调用或返回指令时。

##### 解决：

**1. 暂停：**

优点：简单

缺点：性能不好

**2. 转发：**

在寄存器间另开一条路，直接将需要的数据转发给那个阶段。

优点：不用等待，性能好

缺点：需要在基本的硬件结构中增加一些额外的数据连接和逻辑控制，操作复杂。

**3. 加载/使用数据冒险：（不能用转发解决，但是将转发和暂停结合就好了）**

在下一个周期才产出本周期需要使用的值，转发不能将值传送回过去的时间。

**加载互锁：**用暂停来处理加载/使用冒险。

将加载互锁和转发结合足以处理所有的数据冒险。★

**4. 避免控制冒险：**

**控制冒险：**处理器无法确定下一条指令的地址。（只会发生在`ret`指令和跳转指令，并且后一种只有在预测错误时才会造成麻烦）

**解决：**

1. ret：暂停
2. 跳转：在指令阶段中插入气泡，并取出跳转指令后面的指令，就能将预测错误的指令取消，并且保存了状态，使程序得以继续运行。

#### 4.5.6 异常处理：

**基本原则：**流水线中最深的指令引起的异常，优先级最高。（先把后面的解决了，如果成功，就完事儿了；否则，再解决前面的。若先把前面的解决了后面的大概率还是会报错）

**异常返回方式：**

状态码：在每个流水线寄存器中包括一个状态码stat，随着流水线传播，指到写回阶段被控制逻辑发现，停止执行。

#### 4.5.7 PIPE各阶段的实现：

流水线化的实现应该总是给处于最早流水线阶段中的转发源以较高的优先级，因为它离要用它的阶段最近。画一下流水线的图就明白了，同一周期中前面的阶段离下面的阶段最近。★

#### 4.5.8 流水线控制逻辑：

没有办法在流水线的取指阶段插入气泡。