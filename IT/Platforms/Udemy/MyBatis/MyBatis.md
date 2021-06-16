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

### 2. MyBatis 入门案例：

1. 导入 jar 包（依赖）—— MySQL connector、MyBatis
2. 创建数据库和表
3. 编写实体类（Entity）—— 注：类成员要与创建的数据库表中的字段一致。★
4. 配置全局 mybatis-config.xml —— 配置连接池、连接参数、sql 映射文件信息等。
5. 配置 BlogMapper.xml （写 SQL 语句的文件）—— 注：与 BlogMapper.class 同名，MyBatis 会自动查找它。★★

mybatis-config.xml: 

```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=UTF-8&amp;serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="StudentMapper.xml"/>
    </mappers>
</configuration>
```

StudentMapper.xml: 

```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.google.StudentMapper">
    <select id="selectStudent" resultType="com.google.Student">
        select * from Student where id = #{id}
    </select>
</mapper>
```

StudentTest.java:

```java
public class StudentTest {
    @Test
    public void selectTest() throws IOException {
        // 1. 创建 SqlSessionFactoryBuilder
        // 2. 创建 SessionFactory
        // 3. 创建 SqlSession （用于执行 CRUD 操作）
        // 4. 执行操作
        // 5. 若是更新（增、删、改）操作，则需要提交事务 ★★★
        // 6. 关闭连接
    }
}
```

Student.java:

```java
package com.google;

public class Student {
    private int id;
    private String name;
    private int age;

    /**
     * ...
     * Constructor ...
     * ...
     * Getter and Setter ...
     * ...
     */
    
    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

StudentMapper.java:

```java
package com.google;

import org.apache.ibatis.annotations.Select;

public interface StudentMapper {
    // @Select("select * from student where id = #{id}")
    Student selectStudent(int id);
}
```

全都可以参照 MyBatis 官方文档解决，写得非常详细，还有中文翻译。★★★★★

### 3. MyBatis 日志输出以及核心架构：

通过 log4j.properties 文件增加日志输出。

目前是 log4j2 ，只能识别 xml 和 json 格式的配置文件。★★

默认情况下，系统选择配置文件的优先级：

1. log4j-test.json 或 log4j-test.jsn
2. log4j2-test.xml
3. log4j.json 或 log4j.jsn
4. log4j2.xml

log4j2.xml: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration status="OFF">
  <appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
  </appenders>
  <loggers>
    <logger name="com.relin.HelloLog4j" level="error" additivity="false">
      <appender-ref ref="Console"/>
    </logger>
    <root level="trace">
      <appender-ref ref="Console"/>
    </root>
  </loggers>
</configuration>
```

From: https://blog.csdn.net/lrenjun/article/details/8178875

### 4. 抽取 MyBatis 工具类：

将通过 MyBatis 获取 SqlSession 的一系列重复步骤提取为一个工具类：

SessionUtils.java:

```java
public class SessionUtils {
    static {
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSessionFactory getSqlSessionFactory() {
        return new SqlSessionFactoryBuilder().build(inputStream);
    }
}
```

### 5. CURD 操作 —— 添加：

StudentMapper.xml:

```xml
...
<mapper>
	<insert id="insertStudent" parameterType="com.google.Student">
        insert into student(name, age) values(#{name}, #{age})
    </insert>
</mapper>
```

StudentTest.java:

```java
...
Student student = new Student("Fcuk", 17);
session.insert("insertStudent", student);

// 注：需要提交事务，否则插入的数据不会显示在数据库中。★★
session.commit();
session.close();
```

### 6. 修改：

StudentMapper.xml:

```xml
<update id="updateStudent" parameterType="com.google.Student">
	
</update>
```

