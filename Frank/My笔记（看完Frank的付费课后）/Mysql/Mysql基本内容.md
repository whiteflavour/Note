# MySQL —— 完成时间：2020.6

## 零、开场吹逼

数据库：储存海量信息的仓库

把信息保存到内存里 -> 瞬时性

把信息保存到文件里 -> 持久性

数据库：瞬时性 -> 持久性 （特殊数据库除外 -> Redis、mongoDB ...）

关系型数据库 -> 通过一个公共的数字来管理数据

特点：

1. 分开管理，各管各的，互不影响

2. 能找到与上一层或下一层的关系

MySQL -> C/S架构软件

->    Client客户端：通过命令去访问/操作数据库 （Terminal cmd powershell）

Server服务端：MySQL Server (MySQL 服务端)

乱码 -> 字符编码 ( 常用：GBK, UTF-8 ( 国际通用 ) )

-> Windows下用GBK，MAC 或者 Linux 上用UTF-8 ✬

-> 在实际开发过程中，用UTF-8  ✥

仓库 -> 数据库 -> 里面存放的表 ✱

## 一、安装、连接以及配置

### 1. 两种方式安装，入门推荐第二种

#### MySQL 版本的选择

MySQL 的版本主要根据公司来，根据前两个月的业务使用的版本来。如果上一次使用的版本是 5.7 ，有些数据还和这次有关系，那就用 5.7 。★

如果没有公司，那就使用最新的 稳定版 。这是历代以来的规矩。不能选 Develop 版的，什么开发版、什么实验版。★

这里使用 5.7 的，够用了。

#### MySQL 的安装

第一种方式：（二进制文件的方式，比较适合 Linux ，新手不会配，不建议）

官网 Download -> MySQL Community Server -> 查看以前的版本 -> 找到 5.7.29 ，选择 64 位的 -> 找到 ZIP Archive -> Download

第二种方式：

...... （省略号除与上一个方式一样）-> 点击 MySQL Installer for Windows -> 5.7.29，64 位 -> 下载大的那个

#### MySQL 的安装

卸载杀软，开发人员不用杀毒软件。★

选择 Server Only -> Next -> Execute -> 安装完成后 Next -> Execute -> 一路 Next -> 输入密码 -> 一路 Next -> Windows Service Name: MySQL57 ：等会它会在我们系统中的服务中创建一个服务，名叫 MySQL57 -> 一路 Next -> Execute -> Finish

安装完成后就能在服务中找到 MySQL57 ，可以看一下，不要去乱动。

#### 要在 cmd 连接 MySQL，需要配置环境变量：

开始菜单中的 MySQL 5.7 Command Line Client ，右击 -> 更多 -> 打开文件位置 -> 右击 -> 打开文件所在位置 -> 里面应该有 mysql.exe 文件，拷贝文件夹路径 -> 右击 此电脑 -> 属性 -> 高级系统设置 -> 环境变量 -> 在 PATH 中新建一个环境变量 -> 一路 确定

此时进入 cmd ，输入命令：`mysql -u root -p 刚刚设置的密码`，即可连接。

### 2. 更改终端

使用 Hyper 。

### 3. 服务的启动和停止

如果把 MySQL57 这个服务 停止，就不能连接到数据库了。

client ：通过命令去 访问/操作 数据库

server ：MySQL Server

所以 MySQL 是典型的 C/S 架构软件。

停止服务就相当于 LOL 维护。

#### 使用 二进制 的方式安装 启动 / 停止 服务：

以管理员身份运行 Hyper -> net stop mysql57 (停止) -> net start mysql57 (开启)

对大小写不敏感。★

---

一般直接就在 Windows 服务中 咔咔咔 点击 启动 / 停止 就完事儿。★

### 4. 连接mysql

现在市面上主流的 关系型数据库，就三个：MySQL, SQL Server, Oracle. 这些数据库使用不同的语言，但基本上都是一致的。

#### 两种方式连接 MySQL：

1. mysql -u root -p
2. mysql -u root -p123456 (p 后面直接接密码，不推荐，密码 露出来了。)

#### 退出数据库：

1. exit (推荐，比较通用)
2. quit
3. \q
4. 暴力关闭，直接 关掉 Hyper

---

一定要 ：

1. 开启服务
2. 以管理员身份运行 Hyper
3. 配置 MySQL 的环境变量

### 5.创建data文件夹

进入目录`C:\Program Files\MySQL\MySQL Server 5.7`：

bin 文件夹：放一些 二进制文件 ，有一些命令。

include ：是一些头文件，MySQL 本来就是 C/C++ 写的。

share ：字符集编码。

MySQL 少了一个文件夹，还应该有一个 data ，用来存放数据。后来 MySQL 默认不创建了。

#### 创建 data 文件夹：

Hyper 进入`C:\Program Files\MySQL\MySQL Server 5.7` -> `mysqld --initialize-insecure --user=root`。

然后去 该目录 看一下，这样就创建好了，就能用了。

---

不能直接在那个目录 右击，新建，这样是没用的，需要使用我们在 bin 文件夹中看到的那个 mysqld 这个命令。★

版本非常重要，版本不同可能什么都不同。★

---

才安装完 MySQL 后在为 自己创建 任何的 数据库 时，使用`show databases;`命令展示出来的那 四个 库，即为默认的数据库 (可能是配置文件) ，不能去动它。★

## 二、数据库的基本操作 （重点）✿

### 1. 展示数据库 -> 

```mysql
show databases;
```

### 2. 创建数据库 -> 

1. 普通创法：

   ```mysql
   create database xxx;
   ```
   
2. 进阶创法:

   ```mysql
   create database if not exists xxx;
   ```

3. 装逼创法:

   ```mysql
   create database if not exists `xxx`;
   ```

### 3. 删除数据库 -> 

1. ...:

2. ...:

3. 装逼创法：

   ```mysql
   drop database if exists `xxx`;
   ```

### 4.数据库设置默认字符编码 -> 

```mysql
create database if not exists `xxx` charset=utf8;
```

### 5. 更改数据库默认字符编码 -> 

```mysql
alter database xxx charset=gbk;
```

### 6. 查看创建的数据库 -> 

```mysql
show create database xxx;
```

### 7. 使用数据库 -> 

```mysql
use xxx
```

## 三、表的基本操作

### 1. 创建表 -> 

1. 普通创法:

   ```mysql
   create table student(
   id int,
   name varchar(30),
   age int
   );
   ```

2. 逼格创法 （实用创法，企业中的创法）★:

   ```mysql
   create table if not exists student(
   id int auto_increment primary key comment '主键id',
   name varchar(30) not null comment '姓名',
   phone varchar(20) comment '电话',
   address varchar(100) default '暂时未知' comment '住址'
   )engine=innodb;
   ```

### 2.查看表 -> 

1. 查看表创建时的详情

   ```mysql
   show create table xxx;
   ```

2. 查看表的详情

   ```mysql
   desc xxx;
   ```

### 3.展示表 -> 

```mysql
show tables;
```

### 4. 修改表 -> 

1. 增加字段

   1. 添加到表的最后

   ```mysql
   alter table xxx add xxx varchar(20);
   ```

   2. 添加到某字段之后

   ```mysql
   alter table xxx add xxx varchar(20) after xxx;
   ```

   3. 添加到表的最前面

   ```mysql
   alter table xxx add xxx varchar(20) first;
   ```

2. 删除字段

   ```mysql
   alter table xxx drop xxx;
   ```

3. 修改字段

   1. 修改字段的名字及类型

      ```mysql
      alter table xxx change phone tel_phone int(10);
      ```
      
   2. 修改字段类型
   
      ```mysql
      alter table xxx modify 某字段 varchar(20);
      ```
4. 修改表名

   ```mysql
   alter table xxx rename to xxx;
   ```

### 表中的基本概念

| 字段：  | 关键字：                                              |
| ------- | :---------------------------------------------------- |
| id      | auto_increment  (自动增长)                            |
| name    | primary key （主键）-> 最主要的，靠它来区分学生这张表 |
| age     | comment (注释)                                        |
| phone   | not null (不能为空)                                   |
| address | default (默认值)                                      |
| . . .   | engine=innodb (数据库引擎，innodb 是目前用得最多的) ✡ |

## 四、数据操作

### 1.插入数据

1. 插入一条数据

    ```mysql
    insert into xxx (... -> 一些字段) values (... -> 与前面对应的字段的字段名);
    ```

2. 插入多条数据

    ```mysql
    insert into xxx (... -> 一些字段) values (... -> 与前面对应的字段的字段名), (... -> 与前面对应的字段的字段名), ... , (... -> 与前面对应的字段的字段名);
    ```

### (varchar 类型用单引号) ★

### 2.删除数据

```mysql
delete from xxx where xxx -> (某字段名) = xxx;
```

### 3.清空表中的数据

1. 低性能 (不推荐使用) -> (for 语句遍历表中的数据 )

    -> (并且清空完后新创建数据的 id 会接着清空之前的 id ) ★

    ```mysql
    delete from xxx;
    ```

2. 高性能 (推荐使用) ❀ -> (直接销毁表，然后创建一个一模一样的空表 )

    -> (清空完后重置 id ) ★

    ```mysql
    truncate table xxx;
    ```

### 4.更新表中的数据

```mysql
update xxx set xxx=xxx, ( xxx=xxx, ... ) where xxx=xxx (or xxx=xxx);
```

### 5.查询表中的数据

1. 查询部分数据 (按字段查询)

```mysql
select xxx(, xxx, xxx, ... ) -> (字段名) from xxx;
```

2. 查询全部数据

```mysql
select * from xxx;
```

### 6.SQL语句区分 (概念)

1. DDL -> data definition language -> 数据库定义语言 -> create alter drop show

2. DML -> data manipulation language -> 数据操纵语言 -> insert update delete select

3. DCL -> data control language -> 数据库控制语言 

### 7.字符集编码问题

1. 展示字符编码

```mysql
show variables like 'character_set_%';
```

2. 修改字符编码 ( 主要修改 character_set_client 和 character_set_results ) ❄

```mysql
set xxx -> (Variable_name)=xxx;
```

## 五、数据类型

### 1.数据库的数据类型问题

- 大厂对数据类型的把控非常严格，由DBA（数据库管理员，数据库架构师）来确定应该用什么数据类型。 -> 由产品逻辑定义。

### 2.整型数

- 无符号整型数定义举例

```mysql
create table xxx (
xxx int unsigned ...
);
```

### 3.浮点数

- 整型可以超过自己规定的宽度，但不能超过本身的范围。但是浮点数超过自己规定的宽度会四舍五入。

- 浮点数定义举例

```mysql
create table xxx (
xxx float(5,2) ...
);

(float括号中的5代表总位数，2代表小数点后的位数)
```

- 浮点型和双精度浮点型会丢失精度
- 浮点型不会用来存金钱和关键数据
- 浮点型一般不会用，除非特殊要求

### 4.定点数 -> 可以变长的数

- 定点数不会丢失精度 -> 小数和整数是分开存的 -> 占用更多资源
- 每9个数字（字符）用4个字节来存储
- 用来存金钱
- 支持无符号

### 5.字符串与文本类型

#### 1. 字符串类型

- varchar (可变长字符串) -> 会回收后面不用的空间 -> 但效率不如 char 高
- 字符的大小与字符集编码有关

#### 2.文本类型

- 用来存文章，博客

### 6.枚举类型

- 举例

```mysql
create table xxx (
gender enum('man', 'woman', '?', 'nothing', 'it')
);
```

- 只能取括号中定义的类型
- 枚举的储存方式 -> 枚举中的第一个存的是1，第二个为2 .   .   .   .   .   .  不是从0开始
- 创表的时候可以用对应的数字代替
- 速度快，比字符串快
- 节省空间
- 限制数据

### 7.set 类型

- 枚举是从括号中取一个数据，set 类型取多个
- set 定义举例

```mysql
create table xxx (
hobby set('数学', '经济学', '哲学', 'IT', '文学')
);
```

- set 集合中的每一个元素都应该分配一个固定的数字 -> 分配方式：从左向右按2⁰，2¹，2².  .  .  .  .  .
- 括号中的数据多少个字节有多少个选项？换算成位，有多少位就有多少个选项

### 8.日期和时间类型

- 规定每一张表都必须要有日期和时间类型
- 实际运用datetime（一定要按照规定的格式来）
- 一般情况不手动插入时间，程序自动插入

## 六、列属性完整性

### 1.列属性问题

- 根据项目的要求来确定该字段是否应该存在？是否应该为空？是否应该有默认值？等。

- auto_increment （自动增长）从1开始，是唯一的（如果将某条数据删除，比如 id 为3的某学生，那么该 id 就不能再使用列），不能为零，可以自己插入负数，但是让他自己自增，就从1开始。一旦一个字段为 auto_increment ，该字段必须为 primary key。但是 primary key 不一定一定要为 auto_increment。 ★

### 2.主键的作用及企业用途

**主键**：有唯一性，能够确认这项数据的存在性。在某表中必须要有主键。

**作用**：标识该字段是用来区分各项数据的，比如人的身份证号。保证了数据的完整性。便于查询（加快了查询某项数据的速度）。

- 一个表里只能有一个主键，但这个主键可以有多个字段。
- 主键可能与其他的数据关联，出现在另一个表中，作为查询的依据。但在其他表中它可能不是主键。
- 主键不能为 null ，除非设置了 auto_increment （设置之后可以填入 null ，它自动增长）。

**后期添加主键**：

```mysql
alter table xxx add primary key (字段名);
```

### 3.删除、组合键、选择主键

**删除主键**：

```mysql
alter table xxx drop primary key
```

**添加组合键**：（作用不大）尽量选择一个主键，选择那种改动比较少的（基本不会更改的那种），许多人选择用数字作为主键（有规律，方便查询，比如查到了1，下一条就很可能是2，很容易查到下一条数据）。★

```mysql
alter table xxx add primary key (字段名，字段名)
```

**组合键的缺点**：不易维护。扩容性（扩展性）不好。

### 4.复合主键究竟有什么用

可以用来解决网站 id ，昵称都要唯一的问题。

### 5.唯一键的作用和添加介绍

**唯一键与主键的区别**：唯一键不是用来区分数据的。与其他的表没有关联，并且可以为空。一个表中可以有多个唯一键。

**创建唯一键**：

```mysql
create table xxx (
id int primary key,
phone varchar(20) unique
);
```

**添加唯一键**：

```mysql
alter table xxx add unique (字段名);
```

### 6.唯一键扩展

**添加组合唯一键**：（意义不大）

```mysql
alter table xxx add unique (字段名，字段名);
```

**删除唯一键**：

```mysql
alter table xxx drop index 字段名;
```

### 7.主键和唯一键的区别

前面已总结。

### 8.sql 内注释和代码注释

**代码注释**：（一般不用）在代码中看，可以不写。

1. 单行注释

```mysql
create table xxx(
id int, # xxxx
name varchar(20) -- xxxx
);
```

2. 多行注释

```mysql
create table xxx(
id int
/*
xxxx
xxxx
xxxx
*/
);
```

**sql 内注释**（字段注释）：（常用）给管理员看的，最好写上。

```mysql
create table xxx(
id int comment 'xxxx'
);
```

**代码注释与sql内注释的区别**：`show create table xxx;` 不能看到代码注释，但可以看到sql内注释。

### 9.数据库完整性

**设计数据库的约束**：

1. 保证字段的完整性，一张表里应当要有一个主键约束。
2. 保证数据类型的正确性，能否为空？默认值？
3. 可能需要对外部的引用，这张表的字段被另一张表引用？
4. 自定义约束。

### 10.引用数据表的完整性问题，抛出外键的概念

外键用来解决当两张表有关联时（两张表中有公共的字段：主表与从表）修改数据（从主表中删除了一条数据（开除某个学生），从表应该怎么办？），删除数据（先删从表，再删主表），从表约束（从表中不能插入主表中关联字段没有的数据）等问题。

![Frank——主表与从表抛出的外键作用](F:\笔记\My笔记（看完Frank的课后）\Mysql\Frank——主表与从表抛出的外键作用.png)

### 11.外键

**创建外键**：

```mysql
# 主表
create stu(
stuId int(4) primary key,
name varchar(20)
);
# 从表
create table eatery(
id int primary key,
money decimal(10,4),
stuId int(4),
foreign key (stuId) references stu (stuId)
);
```

外键只用于学习，在实际项目当中（特别是并发），禁止使用外键。★

**添加外键**：

```mysql
alter table xxx add foreign key (字段名) references xxx (字段名);
```

### 12.什么时候设计

使用关系型数据库的时候在创建表时应该先把表的结构大致设计好，否则后期不好维护。★

### 13. 更正错误，删除外键

**删除外键**：首先使用`show create table xxx（从表）`然后删除 constraint 里面的内容。★

```mysql
alter table xxx drop foreign key xxx;
```

**查找外键**：外键只能通过`show create table xxx;`查看，`desc xxx;`则无法查看。★

MUL标记：multiple key，指的是这一列中的数据可以重复，当此表的外键引用主表的主键时会产生它。

### 14.外键三种操作：严格、置空和级联的使用情景介绍

**严格性操作**：上述的简单操作（添加，修改，删除）。

**置空操作**：从主表中与从表绑定的字段中删除一条数据，从表中的对应字段中的那几条数据将被置为null。

**级联操作**：从主表中与从表绑定的字段中删除一条数据，从表中对应的字段中的那几条数据将也一起被删除。

一般情况下删除不使用级联操作，使用置空。更新数据用级联。★

### 15.置空和级联演示

**创建有置空、级联操作的表**：

```mysql
# 主表
create table stu(
id int(4) primary key,
name varchar(20)
);

# 从表
create table eatery(
id int(20) primary key,
money decimal(10,4),
stuId int(4),
foreign key (stuId) references stu(id) on delete set null on update cascade
);
```

## 七、数据库设计思维

### 1.数据设计基本概念

**数据库的关系**： MySQL -> 关系型数据库 -> 通过两张表的共有字段去确定数据的完整性。

**行**：一条数据。一条数据记录。实体。

**列**：一个字段。属性。

**数据冗余**：

* 优点：提高查询效率。
* 缺点：数据太多。

冗余只能减少，不能杜绝。★

减少冗余：分表（专门为了减少冗余分表，没必要）。★

### 2.实体和实体之间的关系

就是一条记录与一条记录之间的关系。（一对多 -> 学生表的 id 与食堂表的 stuId，一对一 -> 学生表与家教表，多对一 -> 程序员表与项目表，多对多 -> 程序员做项目互相帮助。）

### 3.Codd 第一范式，确保每列原子性

共有6个范式，但一般只遵守三个，还需要考虑是否应该遵守这三个。

**确保原子性**：确保每一列不能再分了。

不需要统计的时候不用拆分，需要的时候拆开。

### 4.Codd 第二范式，非键字段必须依赖于键字段，说白了就是别他妈没事找事

一个表只能描述一件事，不能扯淡。

### 5.Codd 第三范式，消除传递依赖

多余的字段可能可以考虑干掉。

数据库的设计是根据项目的需求来的，没有标准。★

## 八、单表查询  ★

### 1.开端

### 2.select

select 后面可以加任意文字：

```mysql
select '去你妈的';

select 2*7;
```

起别名：（as 可省略）

```mysql
select 'Go fucking yourself' (as) qnmd;

select 2*7 as res;
```

### 3.from

```mysql
# 返回笛卡尔积
# 一般不使用 ★
select * from t1,t2;
```

### 4.dual

dual 是默认的伪表。

```mysql
# from dual 可省略

select 2*7 as res (from dual);
# 等价于
select 2*7 as res;
```

### 5.where

where 后面可以跟 =，!=，<，<=，>，>=，and，or，not。

### 6.in

in 前面可以加 not。

```mysql
select * from xxx where address (not) in('beijing','shanghai'); # (包括北京和上海的数据)
# 等价于
select * from xxx where address='beijing' or address='shanghai';
```

### 7.between...and

between..and 前面也可以加 not。

```mysql
select * from xxx where age (not) between 15 and 20; # ([15,20]之间的数据)
# 等价于
select * from xxx where age>=15 and age<=20;
```

### 8.is null

is null 前面也可以加 not。

```mysql
# 年龄为空的数据
select * from xxx where age is (not) null;
```

### 9.聚合函数

```mysql
# 求和
select sum(字段名) from xxx;
# 求平均
select avg(字段名) from xxx;
# 最大（小）值
select max(min)(字段名) from xxx;
# 次数
select count(字段名) from xxx;
```

最好别用 count(*)。★

### 10.客户端的使用

模糊查询：不确定的因素，大概。

**Navicat 的激活**：

1. 打开*激活工具*，点击 Patch （若没找到路径，找到 Navicat 的 exe 文件，将路径复制过来）。
2. 输入 Name 和 Organization（随便输）。
3. 点击 Generate，将 Key 拷贝。
4. 右键 Navicat ，点击属性 -> 兼容性 -> 以管理员身份运行此程序 -> 确定，打开 Navicat。
5. 点击注册，将激活码复制过来，提示有问题之后点击手动激活。
6. 拷贝请求码，粘贴到 *激活工具* 的 Request Code，点击 Activation Code 下方的 Generate。
7. 将生成的码拷贝到 *激活工具*。

**Navicat 连接 MySQL**：

- 连接名：xxx_localhost
- 密码：MySQL 的密码

### 11.like 模糊查询

**通配符**：% -> 匹配一个或多个字符，_ -> 匹配一个字符。

```mysql
select * from xxx where name like '张%'; # 查张三，张八，张跃进
select * from xxx where name like '张_'; # 查张三，张八
select * from xxx where name like '张__' # 查张跃进
```

### 12.order by 排序查询

```mysql
select * from xxx order by chinese asc(desc); # 按语文成绩升序（降序）
```

### 13.group by 分组查询

```mysql
select avg(age) as '年龄',gender as '性别' from xxx group by gender; # 按性别分组
select avg(age) as '年龄',address as '地区' from xxx group by address (desc); # 按地区分组
```

如果使用 group by ，查询的字段必须是分组字段，和聚合函数。★

### 14.group_concat

```mysql
select group_concat(name),gender from xxx group by gender; # 将同性别的学生的名字放在同一条数据中
```

### 15.having

`where` 从原表中筛选，`having` 从筛选原表后创建的虚表中筛选。★

```mysql
# 在已经查询过后的结果中再进行筛选（平均）年龄>24岁的地区
select avg(age) as '年龄',gender as '性别' from xxx having 年龄>24;
# 一般不把字段名起名为中文 ★
select avg(age) as 'age',gender as 'gender' from xxx having age>24;
```

### 16.limit

```mysql
# 从第6条数据开始，查2个数据
select * from xxx limit 5,2;

# limit 默认从0开始
# 查3个数据
select * from xxx limit (0,)3;
```

```mysql
# 查成绩前三
select * from xxx order by score desc limit 3;
```

### 17.distinct all

```mysql
# 去重（去除数据中重复的地址）
select distinct address from xxx;

select count(distinct address) from xxx;

# 默认情况下为 all （可省略）
select (all) address from xxx;
```

## 九、多表查询  ★

### 1.union 联合查询

联合查询字段的个数必须一致。★

```mysql
select age,gender from table_1 union (all) select `name`,phone from table_2;
```

### 2.inner join

```mysql
# 相当于外键，将 student 表里面的 id 与 score 表里面的 stuid 关联起来
# score 表里面的 stuid 来自于 student 表里面的 id
# 将两张表连接起来查询
select student.id,name,score from student inner join score on student.id=score.stuid;
```

inner join 叫做内连接，连接的两张表一定要有公共字段。

### 3.inner join 注意事项

```mysql
select student.id,name,score from student inner join score on student.id=(score.)stuid;
```

on 后面的需要关联的字段如果两张表中都有，则需要指明是哪张表中的，如果不重复，则不需要指定。

### 4.left join

```mysql
# 左连接以左表为基准
select student.id,name,score from student left join score on student.id=score.stuid;
```

### 5.right join

以右表为基准。

### 6.cross join（意义不大，不太实用）

```mysql
# 返回一个笛卡尔积
select * from table_1 cross join table_2;

# 相当于内连接
select * from table_1 cross join table_2 where table_1.id=table_2.id;
(select * from table_1 inner join table_2 on table_1.id=table_2.id;)
```

### 7.natural join（意义不大）

```mysql
# 通过同名字段关联表
select * from t_1 natural (left/right) join t_2;
```

### 8.无公共名字字段的自然连接返回笛卡尔积

### 9.using（不推荐）

如果两张表有两个同名字段，用 natural join 无法连接两表。★

```mysql
# 这两张表有两个同名字段
# 将 id 作为公共字段连接（将 id 作为连接字段）
select * from t_1 inner join t_2 using(id);
```

using 的处理方式和自然连接一样。

### 10.哪一个连接实用？

用 inner join ，然后将后面的公共字段写全。（可读性强）

最终还是得看自己的业务需求。

## 十、子查询  ★

### 1.子查询基本语法

```mysql
# 当括号中返回的 stuid 有多个值时用 in ，有一个值时可以用 = ,也可以用 in
select * from student where id in(=) (select stuid from score where score>=85);
```

### 2. in 和 not in 

一般情况下用 in 不用 = ，因为不知道子查询返回多少个数据，用 in 更通用。

not in 跟 in 的效果相反。

### 3. exists 和 not exists

```mysql
# 若 score 表中存在分数大于85的数据就把 student 表中的数据全部打印出来
select * from student where (not)exists (select stuid from score where score>=85);
```

### 4. 基础结束语

基础内容结束，已经达到实习走后端数据库这一块的要求。后面的内容作为了解，一般3-5年工作经验的人索引和事务锁对这块了解较深刻。

查询是难啃的骨头（重点）。 ★

在业务中常用的东西会记得特别牢。

## 十一、高级部分

### 1. 视图

#### 1. 开场

面试对这块内容主要是问问事务（transaction），看看你是否对此有点了解。对此不必深究，一般大厂在你在基础部分都回答过了之后会问深一点的内容来看看你的路能有多远。

#### 2. view 视图创建、使用、作用

跟数据库管理有关。

视图相当于一个虚拟的表。

**视图的作用**：

1. 用来筛选，防止程序员或者业务人员看到敏感数据。
2. 刻意隐藏表的结构。
3. 从某种意义上说，降低了SQL的复杂度。

**视图的好处**：便于查询。

**创建视图**：

视图跟函数有异曲同工之妙，创建了一个视图，就不用再写（`select name,phone,score from student inner join score on student.id=score.stuid;`）这么长一句SQL语句了，直接查询视图（`select * from vw_stu_all`）。

```mysql
create view vw_stu as select name,phone from student;

create view vw_stu_all as select name,phone,score from student inner join score on student.id=score.stuid;
```

**使用视图**：

```mysql
select * from vw_stu;
```

#### 3. 显示视图

视图是和表放在一起的。可以用 `show tables;`查看。所以要区分视图和表可以在视图前面加一个前缀`vw_` 。

**展示视图**：

```mysql
desc vw_stu;

show create view vw_stu;

# 装逼语句（只起装逼作用）
show table status where comment='view' \G
```

#### 4. 更新和删除视图

```mysql
alter view xxx as select xxx,xxx,... from xxx;

drop view xxx;
```

#### 5. 视图算法 temptable、merge

**创建视图的时候指定视图算法**：

```mysql
create algorithm=temptable view xxx as select xxx,xxx,... from xxx;
```

在视图中使用子查询的时候如果结果有问题记得将视图算法调为 ' temptable '。★

### 2.事务 ★

#### 6. 事务的提出

事务是 mysql 中最重要的一部分，跟金钱打交道，跟操作性的严谨打交道的东西都需要用到它。★

购物点了立即下单但没有付款，钱去哪了？转账没有点确定，钱去哪了？买了东西还没有收货，钱去哪了？

如果不用事务（transaction），下单后退款，会从自己这里更新两条数据，又在阿里那更新两条数据，不妥当。

#### 7. transaction

事务要么一起执行，要么全部回滚。

```mysql
# 开启事务
start transaction;

update wallet set balance=balance-50 where id=1;
update wallet set balance=balance+50 where id=2;

# 提交
commit;
```

```mysql
# 开启事务
start transaction;

update wallet set balance=balance-50;

# 回滚
rollback;
```

 一旦 commit 了，就不能再 rollback 了。★

#### 8. rollback to 回滚点

在公司里，遇到金额转账（跟钱有关的），一般都是用 transaction ，保证资金的准确性。

回滚点相当于虚拟机的快照，git 。

```mysql
start transaction;

insert into wallet values(4,1000);

# 保存一个回滚点
savepoint four;

insert into wallet values(5,199999);

# 再保存一个点
savepoint five;

# 回滚到 'four'
# 保留 'four' 之前的数据
rollback to four;

commit;
```

#### 9. ACID

atomicity 原子性 -> 不能再分了，事务是一个整体，要么一起执行，要么都不执行。

consistency 一致性 -> 一旦 commit ，数据也必须达到最后的状态（完整的状态）。

isolation 隔离性 -> 每个事务都是相互隔离的，A 和 B 的交易不能被 B 和 C 的交易打乱。

durability 持久性（相当于再数据库中永久的写存） -> 一旦 commit ，事务就不能再更改了。

#### 10. 注意事项

事务不是所有的情况都能用，只能在 MySQL 在创建数据库的时候引擎为 innodb 时才能用。★

一般情况下大家都使用 innodb 。

### 3. 索引

#### 11. 索引

**优点**：便于快速查询数据。

**缺点**：

1. 将某字段设为索引之后，该表的数据增、删、改的效率都将降低，还不是一般的低。
2. 索引还会占空间。

**索引的类型**：

* 主键索引
* 唯一键索引
* 普通的索引
* 全局索引（全文索引） -> 搜索引擎用的

旧版本的 MySQL 不支持中文的全局索引。*解决方案*：使用 sphinx 。

**创建（设置）索引**：

```mysql
# 创建普通索引
create index balance_index on wallet(balance);

# 创建唯一索引
create unique index xxx on a_table(a_filed_name);
```

**删除索引**：

```mysql
drop index the_name_of_the_index on a_table;
```

**创建索引的条件**：（为什么要创建索引？）

1. 这个数据需要频繁的查询。（高考总分 -> 可创建索引，也可不创）
2. 公共字段可能需要创建索引。

如果这个表里面的数据非常少，千万别创建索引。（愚蠢的行为） -> （在班级中创建索引、为性别创建索引）★

### 4. 存储过程

#### 12. delimiter

除了事务（transaction）非常重要，其他的都是扩展，可以了解，知道干什么用的就OK。

存储过程一般用不到，稍微玩儿一下就行了。

主要是DBA用的，用来模块化设计。支持事务，支持各种操作，增删改查，相当于一个函数。跟视图不同，视图只能用来查东西。

每用一个分号，相当于执行一条SQL语句，就发送服务器了。

**设置分隔符**：

```mysql
# 将一条语句以 ';' 结尾改为以 '//' 结尾
delimiter //
```

#### 13. procedure 存储过程的用途

**创建存储过程**：

```mysql
# 将分隔符改为 '//'
delimiter //

# 创建存储过程
create procedure proc()

begin
update wallet set balance=balance+50;
update t3 set name='Tom';
end //

# 将分隔符改回 ';'
delimiter ;

# 调用存储过程
call proc();
```

存储过程里面可以嵌套事务，在 `begin` 后面 `start transaction `，在 `end` 前面 `commit`。

**删除存储过程**：

```mysql
drop procedure proc;
```

**展示存储过程**：

```mysql
show create procedure proc;
```

**显示所有的存储过程**：

```mysql
show procedure status \G
```

### 5. 有趣的函数

#### 14. number

**生成一个随机数**：

```mysql
select rand();

# 抽奖
select * from student order by rand() limit 3;
```

一般情况下后端开发，能从数据库角度解决问题就不从 service 层解决问题。★

**取整**：

```mysql
# 向上取整
select ceil(3.1);

# 四舍五入
select round(3.4);

# 向下取整
select floor(3.9);
```

**截取数字**：

```mysql
# 第二个参数为截取的小数位数
select truncate(3.1415926535,2);
```

**随机排序**：

```mysql
select * from student order by rand();
```

#### 15. string

```mysql
# 转换为大写
select ucase('fuck!');

# 转换为小写
select lcase('FUCK!');
```

**截取字符串**：

```mysql
# 从左边截取2个
select left('FUCK!',2);

# 从右边截取2个
select right('FUCK!',2);

# 从第2个字符开始，截取3个
select substring('FUCK!',2,3);
```

**拼接字符串**：

```mysql
select concat('FUCK!','aaa');

# 将 student 中的 name 和 age 字段用 '|' 分割并查询
select concat(name,'|',age) from student;
```

#### 16. others

**时间**：

```mysql
# 当前的时间
select now();

# 获取当前的时间戳
select unix_timestamp();

# 年，月，日
select year(now()) year,month(now()) month,day(now()) day;
```

**加密**：

```mysql
# 加密函数
select sha('aaa');
```

## 十二、企业规范约束

### 1.★库表字段约束规范

**强制要求**：

1. 在字段中使用是和否，一定要给 is ，例如，is_vip ，数据类型为 unsigned tinyint ，长度为1。（不要为了奢侈，大度而浪费性能，浪费存储）
2. 如果该字段不能为负，类型必须添加 unsigned 。
3. 在 Java 中，POJO 类不能设置为布尔类型，在 request map 里面添加映射关系。
4. 表名和字段名必须使用小写字母，不能出现数字开头，不能有大写，下划线之间不能只出现数字（数据库的字段名，尤其是关系型数据库，一旦定义了就不能再改了。（很麻烦，代价太大，很多表都会被跟着动）），单词之间用下划线隔开。★
5. 字段名一定要谨慎考虑设计。★
6. MySQL 在 Windows 下不分大小写，但在 Linux 下默认分大小写。
7. 表名不能出现负数。
8. 不能用 MySQL 中的关键字当表名（select, table）。
9. 索引名
    * 主键索引名：pk_xxx
    * 唯一键：uk_xxx
    * 普通索引：idx_xxx

10. 凡是有小数的，禁止使用 float 和 double ，全部使用 decimal ，避免精度丢失，出现数据的差异，为项目带来不必要的负担成本。
11. 如果定义的字符串长度很小，别使用 varchar ，使用 char 。
12. varchar 长度一般不建议超过5000，超过5000用 text 。
13. 表里面必须要求要有的字段：
    * id
    * create_time
    * update_time

其中 id 必须为主键，类型为 bigint unsigned ，单表（该表的 id 不与其他表绑定）的时候必须自增，每次自增的步长为1，除非它是分布式 id 。★

create_time 和 update_time 必须为 datetime 类型。

---

**建议**：

14. 如果项目比较大的话，表名应当与业务名有些关系。
15. 仓库名一般与应用名保持一致。
16. 唯一索引一般不设置在冗余字段。
17. 单表行数超过500w行或者容量超过2个G，记得分库，分表。（工作3-5年）

### 2. 索引规范

1. 在业务和流程上具有唯一特性的字段，即时它是多个字段的组合，也应该设置一个唯一索引，唯一索引对插入数据速度的损耗可以忽略，但是提高查找速度是明显的。唯一索引便于数据的校验控制（完整性控制），如果没有唯一索引，肯定有脏数据、垃圾数据产生。★
2. 在开发过程中最多只能两个表关联查询，而且如果要 join ，数据类型两边必须绝对一致（虽然语法上不报错）。
3. 在多表关联查询的时候，要保证关联查询的字段也有索引。
4. 页面上的搜索，别使用左模糊或全模糊。
5. 如果在 varchar 上建立索引，必须指定索引的长度，没必要对全字段建立索引，根据实际的文本的区分度来决定索引的长度。
6. 建议新手不要搞索引。

### 3. ★SQL开发约束

1. 不要妄想用 count(xxx,xxx...)  替代 count(*) ，因为即便把列名写完，你会发现 NULL 的没统计。★
2. 千万不能用 '=' 号来判断 null 值，用 `is null` ，或者 ISNULL() 函数。
3. 不要使用外键和级联，尤其是在高并发、集群、分布式的项目当中，要更新的表、数据太多，会占用太多的CPU和服务器资源。一切外键的问题在 service 层或者应用层解决。用外键和级联，插入数据的时候也会影响到速度。★★
4. 实际开发过程中（开发人员）不允许使用存储过程，因为存储过程很难调试，如果其中有一句SQL出错，其他的语句都会执行，只有它不执行。存储过程还很难扩展。移植性也没有（不能移植到其他的数据库里面用）。
5. 在删除、更新数据的时候，先查出来（select），看看有没有，如果没有错误，再更新，删除。
6. in（子查询中的） 的操作，能避免就避免。
7. uft8作为国际的项目编码，数据库客户端，数据库server，数据库的接收端，发送端都要为 utf8 源码格式。

### 4. 其他约束

1. 在ORM映射当中（Spring data jpa, hibernate），在查询过程当中，不要使用 * 作为查询的字段列表，有哪些字段必须明确表明，因为使用 * 的时候，它对应的 map 的解析器会解析你的SQL，看看 * 里面到底有什么东西，需要耗费时间，而且增减字段的时候，万一返回的 result map 配置有问题，就完了。没必要的查询结果不需要使用 * （text）。（浪费性能）
2. POJO 类布尔类型不能加 is 。数据库类型必须加 is_ 。
3. 不要滥用 `@Transactional` ，可能会影响数据库的 QPS。而且使用事务的地方一定要考虑周全，考虑各方面的回滚，缓存的回滚，引擎的回滚，搜索引擎回滚，统计都要去考虑清楚。
4. 销毁表比 delete 表速度快。



