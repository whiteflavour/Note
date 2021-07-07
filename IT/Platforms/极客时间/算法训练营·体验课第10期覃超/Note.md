# Note

对抗更新极快的技术，我们只有学习那些不怎么变化的基础，学起那些新技术来才游刃有余。但是往往那些不变的基础都是难啃的硬骨头，所以需要花点时间钻研。这就是为什么厂喜欢考算法。

## 复杂度分析

### 时间复杂度：

**O(logn) 的理解：**

```java
for (int i = 0; i < n; i = i * 2) {
    ...
}
```

假设 n 取 8，那么 for 语句只执行 3 次，即 log2(8)；同理，n 取 1024 ，则执行 log2(1024) = 10 次。

**O(k^n) —— 递归的时间复杂度计算：**

时间复杂度主要就是看程序执行了多少次，这里就是看递归执行了多少次。

**解决办法：**

我们将递归执行的过程展开，画成一个递归树：

![递归树](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\递归树.png)

```java
// fibonacci 数列的判断，求第 n 项
int fib(int n) {
    if (n < 2) {
        return n;
    }
    return fib(n - 1) + fib(n - 2);
}
```

> 注意：可以发现递归树中有许多重复的节点，所以性能极差，复杂度就是 O(2^n) 了，是指数级的，非常恐怖，所以在面试中千万不要这么写，可以直接循环或者用缓存把重复的节点保存下来。★★

#### 主定理：★

解决所有时间复杂度的求解。

数学证明非常复杂，了解一下就行。

**主要记住四种：**

![主定理中的四种方法](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\主定理中的四种方法.png)

面试可能会问一下二叉树（图）的遍历结果，然后顺便搞个时间复杂度，你就说 O(n)，可以说是通过主定理得到的，也可以说每个节点都遍历一次。★

#### 反思：

根据时间复杂度的曲线图，可以发现，优化时间复杂度得到的收益是非常高的。

1. 写完程序要下意识的分析它们的时间复杂度。
2. 用顶尖的时间复杂度来写程序，是顶尖选手的职业素养。（如果你时间复杂度写砸了的话，对公司的成本和资源消耗是很大的）

**面试解题四件套：**

1. 明白面试官和这道题的意思，要考察的点
2. 思考所有的解决方法
3. 比较时间复杂度，寻找最优方案
4. 测试结果

### 空间复杂度：

**规则：**

1. 数组的长度：一维数组，就是 n ；二维就是 n^2
2. 递归的深度，若递归中开了数组，则是两者间的最大值。

### 总结：

- 常用工具 —— 要把常用的工具玩儿熟。（工欲善其事，必先利其器）
- 基本功和编程指法
- 常见的时间、空间复杂度

[如何理解算法时间复杂度的表示法](http://www.zhihu.com/question/21387264)

## 数组、链表、跳表：

### 1. 实现和特性：

#### 跳表：

**要求：**只能用于链表有序的情况。

**作用：**用来取代平衡树的二分查找。★

**思想：**一维的数据结构要加速，一般就要升维，多提供一些信息，就能加速。★★

> 升维思想，空间换时间。★

**缺点：**维护成本高，每次增加或者删除元素需要将它的索引也更新一遍，而且可能出错，就是说可能索引会多跨两步，或者少跨两步。★

**运用：**Redis、LRU Cache 等。

> 跳表面试的时候不会让你手写，主要是理解和看响应的文章为主。★

![跳表的时间复杂度](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\跳表的时间复杂度.png)

![跳表的空间复杂度](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\跳表的空间复杂度.png)

![提高链表查找效率](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\提高链表查找效率.png)

- [ Java 源码分析（ArrayList）](http://developer.classpath.org/doc/java/util/ArrayList-source.html)
- [Linked List 的标准实现代码](http://www.geeksforgeeks.org/implementing-a-linked-list-in-java-using-class/)
- [Linked List 示例代码](http://www.cs.cmu.edu/~adamchik/15-121/lectures/Linked Lists/code/LinkedList.java)
- [Java 源码分析（LinkedList）](http://developer.classpath.org/doc/java/util/LinkedList-source.html)
- LRU Cache - Linked list：[ LRU 缓存机制](http://leetcode-cn.com/problems/lru-cache)
- Redis - Skip List：[跳跃表](http://redisbook.readthedocs.io/en/latest/internal-datastruct/skiplist.html)、[为啥 Redis 使用跳表（Skip List）而不是使用 Red-Black？](http://www.zhihu.com/question/20202931)

### 2. 实战题目解析：移动零

#### 题目练习步骤：

1. 5-10分钟：读题和思考（可以将自己的所有的思路想法记录在下面，然后比较，得出最优解）
2. 有思路，自己开始做和写代码；不然，马上看题解

> 这些算法本来就不是死磕能够想出来的，不要说我再挣扎一下，或者磕个两天，如果能够从无到有想出这些算法，然后再写一篇文章的话，就能拿图灵奖了。我们要培养的不是图灵奖获得者，所以只需要理解并且熟练运用即可。

3. 默写背诵，熟练（？？？）
4. 开始自己写，闭卷（若发现这种操作不太熟练，可以多写几遍，熟悉一下）

> 然后在 LeetCode 上测试结果，输入的样例可以改。★★
>
> 提交之后内存基本不用看，主要看时间。★
>
> 然后看看官方题解，别人的代码和题解。有时候官方的题解写的并不好。★★★
>
> 官方题解：如果字太多可以不用看，直接看代码。如果感觉写的不好，可以直接跳过。与其去理解它的解法，不如看下面的最优解。★★★
>
> 最后，去国际站，看别人的题解和评论，看 voted 最高的。★★

**刷题误区：**

刷题只刷一遍。（要刷 5 遍）★★★★★

- [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

- [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

## 树、二叉树、二叉搜索树：（二维）

### 1. 基本实现和特性：

**实际中的应用：**

斐波拉契数的递归展开是一个树形状；AlphaGo 棋盘展开是一个树形:

![AlphaGo棋盘展开](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\AlphaGo棋盘展开.png)

还有很多，人生也是，可以选择各种节点，然后展开，可以选择出国深造或者进厂。

#### 遍历：

树这种结构写循环比较麻烦，主要是递归。树的遍历要爱上递归，拥抱递归。★★

#### 删除：

删除根节点之后，要从叶子节点中拉一个垫背的起来当作新的根节点，一般来说我们找右子树中第一个大于要删除元素的叶子。（也可以选择左子树中第一个小于要删除根节点的节点。

- [二叉搜索树 Demo](https://visualgo.net/zh/bst)

### 2. 实战题目解析：二叉树的中序遍历

将二叉树的定义和前中后序遍历的递归代码熟悉起来，记下来。★★

![前中后序遍历模板](F:\Note\IT\Platforms\极客时间\算法训练营·体验课第10期覃超\Pictures\前中后序遍历模板.png)

**递归的误区：**

递归并不是效率低，而是你代码写的不合理，该用缓存的地方没有缓存。★★

> 如果递归得很深的话，效率低就是会多开一些栈，但是现在编译器对于递归的优化，可以认为递归的效率是和循环一样的。

> 这些只能自己去写，自己去试，不然没办法真正提高的。★★★

其实很多非递归的题解就是模拟递归，自己去维护了一个栈。★★★★

- [N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)
- [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
- [树的遍历 Demo](https://visualgo.net/zh/bst)

## 递归：

### 1. 实现、特性及思维要点：

**递归与循环：**本质就是汇编的指令不断跳到那个地方去执行，递归与循环相似。

**理解：**相当于盗梦空间中的进入多层梦境，只能一层一层的进，一层一层的出，每一层的环境不受影响（主角除外，可以理解为函数中的参数），但是人的状态可以带入其他层。

**递归模板：**

Java:

```java
// Java
public void recur(int level, int param) {   
    // terminator   
    if (level > MAX_LEVEL) {     
        // process result     
        return;   
    }  
    // process current logic   
    process(level, param);  
    // drill down   
    recur(level: level + 1, newParam);   
    // restore current status  
}
```

C/C++:

```c++
// C/C++
void recursion(int level, int param) {   
    // recursion terminator  
    if (level > MAX_LEVEL) {     
    // process result     
        return ;   
    }  // process current logic   
    process(level, param);  
    // drill down   
    recursion(level + 1, param);  
    // reverse the current level status if needed
}
```

JS:

```js
// JavaScript
const recursion = (level, params) =>{  
    // recursion terminator   
    if(level > MAX_LEVEL){     
        process_result     
        return    
    }   // process current level   
    process(level, params)   
    //drill down   
    recursion(level+1, params)   
    //clean current level status if needed   
}
```

Python:

```python
# Python
def recursion(level, param1, param2, ...):     
    # recursion terminator     
    if level > MAX_LEVEL: 	   
        process_result 	   
        return     
    # process logic in current level     
    process(level, data...)     
    # drill down     
    self.recursion(level + 1, p1, ...)     
    # reverse the current level status if needed
```

#### 思维要点：

1. 不要人肉进行递归（最大误区）—— 熟练之后摒弃它，刚开始学可以在纸上画一下状态树，到后面直接看函数本身就开始写，不然永远无法有效的掌握和熟练使用递归。
2. 找到最近最简方法，将其拆解成可重复解决的问题（重复子问题）—— 我们的递归函数中只包括 if else, for and while loop 。
3. 数学归纳法

[递归代码模板](https://shimo.im/docs/EICAr9lRPUIPHxsH)

### 2. 实战题目解析：爬楼梯、括号生成等问题：

> 对于递归问题，牢记思维要点。★★

注：如果题目本身没有重复性，那么复杂度是客观存在的，只能一条条写出来，从 n=1 开始，一直写完。但是，所有的面试题都是在 5 行，10 行，最多 20 行以下是能够完成的，说明它肯定有重复性。★★★

#### 爬楼梯：

**思路：**数学归纳法（但是不要挨个列出来人肉递归，太复杂了，到 4 就会很复杂了）。

可以这样想，到三的时候，可以从第 1 阶，跨两阶上去；或者从第 2 阶，跨 1 阶上去。★★

**括号生成：**

**思路：**先搞个递归，把所有的情况都搞出来，忽略括号合不合法的判断，最后再加上判断合不合法的逻辑 —— 要放右括号，前面必须要有左括号，并且左括号的数量要比右括号多。

> 实际上生活中的各种问题，基本上都有某种重复性。★★

> 国际站上的有个头像是黄色的光头个，代码很优雅，但是晦涩，有兴趣的可以看看，提高自己代码的阅读能力。★

> 要学会阅读别人的代码，若看到别人写的很漂亮，可以将他们的方法学到手。★★

**验证二叉搜索树：**

二叉搜索树（BST）-> 中序遍历结果为递增。★★

**二叉树深度：**

思路：maxDepth(左子树，右子树) + 1

## 面试：

### 1. 如何高效准备大厂算法面试

简历突出亮点。

**面试考点：**

- 项目经验：要点、深度
- 基础知识：语言、数据库、并发、框架知识等——问广度，知识点比较广，且杂
- 算法与数据结构：（重点）60-70%
- 系统设计（少量）——面架构师

**好的笔记：**

Github 搜索：

1. JavaGuide
2. CS-Notes（若时间有限，此为最优）★

**进公司之后对付几十万行代码：**

不要信公司的文档，直接看代码。找到写的那个人，让他跟你说说最外面的每个重要的模块的功能是什么，这样他是愿意的，如果每行问或者几行看不懂去问，他会不耐烦。

**学习方法：**

- 总结 Mind Map + 费曼学习法
- 练习（五毒神掌）——题不要只做一遍，特别是高频题，多做几遍，根据遗忘曲线的规律拉开每次做的时间。（注：并不是排前面的题解就是最好的，易懂的题解可能在后面，可以多看几个）
- 环境（类似于 Frank 的付费群打卡群）

**最大误区：**

- 光看，不练，且追求一次理解：

如何理解知识？

看知乎回答——花一晚上也无法理解非递归遍历二叉树，我该继续学下去吗？

> 重复，增加大脑突触。因为它会生长，就跟肌肉一样，所以会感觉累。★

- 只练一遍
- 没有反馈

**关于系统设计——架构师：**

github 搜 —— system-design-primer

**正确认识面试：**

- 作为和未来同事的一次合作
- 并肩作战、解决问题
- 减少压力

> 所以一定要积极沟通和表达——不会就说不会，然后他给你建议你要说建议很好，这个题目出的非常漂亮。★

> 摒弃之前的习惯，用新的方法来学习。——如果你作为一个职业的选手，在某专业，你会发现那些业余的选手会有一堆坏习惯。★★

### 2. 我是怎么拿到大厂Offer的？

**不要着急写代码：**★

1. 确认好要解决的问题——特殊情况？边界？数据的规模？
2. 与面试官交流自己的解法，他或许会给到一些提示
3. 写完不要马上提交，检查并测试一下

> 可以锻炼一下白板写代码，面试之前。★