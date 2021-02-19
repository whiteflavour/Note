# JDBCUtils 问题

## java.lang.NoClassDefFoundError: Could not initialize class com.google.util.JDBCUtils 问题解决：

```java
// 将下面这句话改为最下面那句话
InputStream inputStream = JDBCUtils.class.getClassLoader().getSystemResourceAsStream("db.properties");
InputStream inputStream = JDBCUtils.class.getClassLoader().getResourceAsStream("db.properties");
```

错误原因：（ from stackoverflow : https://stackoverflow.com/questions/7615040/difference-between-classloader-getsystemresourceasstream-and-getclass-getresou ）

因为在 webapp 中，是一个 目录层级 （classpath hierarchies），而不是简单的一个目录，这个 目录层级 会在各个 webapp 之间共享。`getSystemResourceAsStream()`只能访问 顶层 层级，所以 在运行 的时候会找不到 db.properties 文件，而在 编译 的时候却能找到。★

一般来说，使用`getResourceAsStream()`是更好的选择，因为它将使用与代码所属的Class相同的类加载器，即它 包含了 `getSystemResourceAsStream()`。★

## 驱动不能加载问题 (No suitable driver found for jdbc:mysql://localhost:3306/login?characterEncoding=utf8) 问题解决：

注意看 Server 给的提示。★

如果 驱动 不能加载，在`getConnection()`方法前面加上`forName()`语句。

From ： https://stackoverflow.com/questions/5556664/how-to-fix-no-suitable-driver-found-for-jdbcmysql-localhost-dbname-error-w 第二条回答。

## 时区问题 (The server time zone value '?  ???????' is unrecognized or represents more than one time zone.) ：

时区有问题，在 连接语句 后面加上`serverTimezone=UTC`，即：`jdbc:mysql://localhost:3306/login?useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC` 。

From ： https://www.cnblogs.com/EasonJim/p/6906713.html

