# MyBatis

## 一、入门：

### 1. MyBatis 与 JDBC 和 Hibernate 的区别：

#### 1. JDBC 的缺点：（及对应 MyBatis 的解决）

1. 数据库频繁连接与释放造成性能损失。**解决方法：**使用数据库连接池。（MyBatis 默认使用连接池）
2. SQL 语句在 Java 代码中，若改动，需要更改 Java 源码，不利于管理维护。（MyBatis 将 SQL 写在配置文件中）
3. PreparedStatement 的占位符也容易发生改变，造成改动源码。（MyBatis SQL 语句可以在配置文件中随意更改）
4. 返回的结果集不易维护，封装入 POJO 更佳。（MyBatis 提供对象封装机制）

#### 2. MyBatis 与 Hibernate：

MyBatis 不是一个完全的 ORM 框架，程序员手动编写 SQL 语句。

##### MyBatis 的优点：

1. 灵活。
2. 适合变化频繁，关系映射不太复杂的应用。（如：电商应用、商城 。。。）

##### MyBatis 的缺点：

1. 对关系性较复杂的应用处理较弱。
2. 需要维护大量的 SQL 映射文件。

---

##### Hibernate 的优点：

1. 对对象关系映射的处理较强。
2. 节省代码量。
3. 适合企业内部应用。（大型应用）

##### Hibernate 的缺点：

1. 门槛较高。
2. 性能不如 MyBatis，因为做了很多封装。