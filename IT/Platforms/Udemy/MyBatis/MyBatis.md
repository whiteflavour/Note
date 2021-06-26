# MyBatis

## 一、入门：

### 一、基本操作：

#### 1. MyBatis 与 JDBC 和 Hibernate 的区别：

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

#### 2. MyBatis 入门案例：

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

#### 3. MyBatis 日志输出以及核心架构：

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

#### 4. 抽取 MyBatis 工具类：

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

#### 5. CURD 操作 —— 添加：

#### 根据官方文档，有三种方法：

##### 一、直接使用 SqlSession 中的方法：

StudentTest.java:

```java
...
Student student = new Student("Fcuk", 17);
session.insert("insertStudent", student);

// 注：需要提交事务，否则插入的数据不会显示在数据库中。★★
session.commit();
session.close();
```

StudentMapper.xml:

> 注：若需传入多个参数，那么需要将它们封装起来，传入 Student 。★★★

```xml
...
<mapper>
    <!-- 这里需要 name and age 两个参数，所以需要将它们封装入 Student -->
	<insert id="insertStudent" parameterType="com.google.Student">
        insert into student(name, age) values(#{name}, #{age})
    </insert>
</mapper>
```

##### 二、使用 StudentMapper.java 中自定义的方法：

StudentTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    StudentMapper mapper = session.getMapper(StudentMapper.class);
    mapper.insertStudent(new Student("hello", 16));
    session.commit();
}
```

StudentMapper.java:

```java
int insertStudent(Student student);
```

##### 三、不通过 StudentMapper.xml ，而在 StudentMapper.java 中使用方法级别的注解：

StudentMapper.java:

```java
@Insert("insert into student(name, age) values(#{name}, #{age})")
int insertStudent(Student student);
```

#### 6. 修改：

StudentMapper.xml:

```xml
<update id="updateNameOfStudent" parameterType="com.google.Student">
    update student set name = #{name} where id = #{id}
</update>
```

#### 7. 查询所有数据：

StudentTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    List<Student> results = session.selectList("selectAllStudents");
    // System.out.println(results);
    for (Student student : results) {
        System.out.println(student);
    }
}
```

#### 8. 根据 id 查询：

```xml
<select id="select" resultType="com.google.Student" parameterType="int">
    select * from student where id = #{value}
</select>
```

#### 9. 根据字段模糊查询：

#### 方法一：

StudentMapper.xml:

```xml
<select id="selectByName" resultType="com.google.Student" parameterType="String">
    select * from student where name like #{value}
</select>
```

StudentTest.java:

```java
...
List<Student> results = session.selectList("selectByName", "%张%");
...
```

#### 方法二：

StudentMapper.xml:

```xml
<select id="selectByName" resultType="com.google.Student" parameterType="String">
    select * from student where name like '%${value}%'
</select>
```

StudentTest.java:

```java
...
List<Student> results = session.selectList("selectByName", "张");
...
```

#### 10. 删除：

```xml
<select id="selectByName" resultType="com.google.Student" parameterType="String">
    delete from student where id = #{value}
</select>
```

#### 11. MyBatis 核心 API 介绍：

SqlSessionBuilder：工具类，只用一次。

SqlSessionFactory：作用范围：整个应用程序运行期间；创建后可以重复使用，一般设置为单例模式来管理 SqlSessionFactory 。★

SqlSession：线程不安全，每个线程必须拥有自己的 SqlSession；最佳使用范围：请求或者方法中；注：绝对不能将 SqlSession 实例的引用放在一个类的静态字段或实例字段中；使用完之后需要关闭。（放在 finally 中或者带资源的 try 语句中）★★★

### 二、XML 配置：

#### 12. properties 属性的使用：

mybatis-config.xml 中，`<dataSource type="POOLED">`中的 POOLED 表示使用 MyBatis 内置的连接池，若使用 UNPOOLED ，则表示不使用连接池，一般使用 POOLED 。★

#### properties：

内部配置：

mybatis-config.xml:

```xml
<!-- 定义全局属性，方便在后续中使用 -->
<properties>
    <property name="driver" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=UTF 8&amp;serverTimezone=UTC"/>
</properties>
...
<dataSource type="POOLED">
    <!-- 使用 -->
    <property name="driver" value="${driver}"/>
    <property name="url" value="${url}"/>
    <property name="username" value="root"/>
    <property name="password" value="123456"/>
</dataSource>
...
```

外部配置：推荐使用。★

mybatis-config.xml:

```xml
...
<!-- 定义 -->
<properties resource="jdbc.properties"/>
<!-- 使用 -->
<dataSource type="POOLED">
    <property name="driver" value="${driver}"/>
    <property name="url" value="${url}"/>
</dataSource>
...
```

jdbc.properties:

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?characterEncoding=UTF 8&amp;serverTimezone=UTC
```

#### 13. 别名的使用：

MyBatis 中有一些内置的别名，也可以自定义别名：（——官方文档）

方法一：

mybatis-config.xml:

```xml
<typeAliases>
  <typeAlias alias="Author" type="domain.blog.Author"/>
  <typeAlias alias="Blog" type="domain.blog.Blog"/>
  <typeAlias alias="Comment" type="domain.blog.Comment"/>
  <typeAlias alias="Post" type="domain.blog.Post"/>
  <typeAlias alias="Section" type="domain.blog.Section"/>
  <typeAlias alias="Tag" type="domain.blog.Tag"/>
</typeAliases>
```

方法二：

mybatis-config.xml:

```xml
<typeAliases>
  <package name="domain.blog"/>
</typeAliases>
```

若没有注解，自动使用对应类名的首字母小写的值：

Author.java:

```java
@Alias("author")
public class Author {
    ...
}
```

注：别名不区分大小写。★★★

#### 14. mapper 映射器的基本使用：

告诉 MyBatis 查找映射文件的方法：

1. 相对于类路径
2. URL
3. 类接口
4. 包

## 二、进阶：

### 15. MyBatis 原始方式的 DAO 层开发：

StudentDao.java:

```java
public interface StudentDao {
    void selectStudent(int id);
}
```

StudentDaoImpl.java:

```java
public class StudentDaoImpl implements StudentDao {
    @Override
    public void selectStudent(int id) {
        SqlSessionFactory sqlSessionFactory;
        SqlSession session = null;
        try {
            InputStream inputStream = Resources.getResourceAsStream("mybatis-config.xml");
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
            session = sqlSessionFactory.openSession();
            Student student = session.selectOne("selectStudent", 1);
            System.out.println(student);
        } catch (IOException e) {
            session.rollback();
            e.printStackTrace();
        } finally {
            session.close();
        }
    }
}
```

StudentDaoImplTest:

```java
public class StudentDaoImplTest {
    @Test
    public void testDao() {
        StudentDaoImpl studentDao = new StudentDaoImpl();
        studentDao.selectStudent(1);
    }
}
```

缺点：DAO 接口的实现类的代码冗余，非常繁杂。★

解决方法：使用动态代理接口开发 DAO 层，不需要写实现类。★

### 16. 动态代理接口开发 DAO 层：（推荐使用）★

**规则：**

1. StudentMapper.xml 的 namespace 必须与对应的 StudentMapper.java 接口一致，即官网所说的绑定。
2. xml 中的 id 与接口中的方法名称一致。
3. 参数与返回值类型一致。

### 17. 输入映射- 不同类型的使用：

**输入映射支持的类型：**

1. 基本类型：int, String, double 。。。（常见）
2. JavaBean （常见）
3. 包装 JavaBean （一个类的类成员含有另一个类，即一个类依赖于另一个类）

**包装 JavaBean 类型输入映射的使用：**

StudentMapper.xml:

```xml
<insert id="insertStudentByWrapper" parameterType="studentWrapper">
    insert into student(name, age) values(#{student.name}, #{student.age})
</insert>
```

StudentWrapper.java:

```java
public class StudentWrapper {
    private Student student;

    public StudentWrapper(Student student) {
        this.student = student;
    }
}
```

StudentMapper.java:

```java
void insertStudentByWrapper(StudentWrapper studentWrapper);
```

StudentMapperTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    StudentMapper mapper = session.getMapper(StudentMapper.class);
    Student student = new Student("RNM", 20);
    StudentWrapper studentWrapper = new StudentWrapper(student);
    mapper.insertStudentByWrapper(studentWrapper);
    session.commit();
}
```

### 18. 输出映射 - 基本类型和 JavaBean：

**支持的类型：**

1. 基本类型 （常用）
2. JavaBean （常用）
3. ResultMap

### 19. 输出映射-ResultMap的使用：

**适用场景：**当数据库中的字段名和对应POJO类的成员名不一样的时候，就不能封装为 JavaBean 类型，这是使用 ResultMap 。★

StudentMapper.xml:

```xml
<select id="selectAnotherStudent" parameterType="int" resultMap="anotherStudent">
    select * from student where id = #{id}
</select>

<!-- id 必须与上面 resultMap 特性一样 -->
<resultMap id="anotherStudent" type="anotherStudent">
    <!--
         column 为原来本身的类型，即 Student 的类成员；
         property 为现在需要映射到的类型，即 AnotherStudent
         的类成员
    -->
    <id column="id" property="aId"/>
    <id column="name" property="aName"/>
    <id column="age" property="aAge"/>
</resultMap>
```

StudentMapper.java:

```java
AnotherStudent selectAnotherStudent(int id);
```

StudentMapperTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    StudentMapper mapper = session.getMapper(StudentMapper.class);
    AnotherStudent student = mapper.selectAnotherStudent(1);
    System.out.println(student);
}
```

### 20. 动态SQL-if 标签：

StudentMapper.xml:

```xml
<select id="selectByNameOrAge" resultType="student" parameterType="student">
    select * from student
    <where>
        <if test="name != null">
            and name like #{name}
        </if>
        <if test="age != 0">
            and age >= #{age}
        </if>
    </where>
</select>
```

StudentMapper.java:

```java
List<Student> selectByNameOrAge(Student student);
```

DynamicSqlTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    StudentMapper mapper = session.getMapper(StudentMapper.class);
    Student student = new Student();
    // student.setName("f%");
    student.setAge(20);
    List<Student> results = mapper.selectByNameOrAge(student);
    System.out.println(results);
}
```

### 21. where Tag

可以自动去掉第一个 and 。

官方文档写的非常详细，还能自定义 where 的作用。★★★

### 22. sql Tag

**作用：**将相同的 SQL 片段抽取出来。

StudentMapper.xml:

```xml
<mapper namespace="com.google.mapper.StudentMapper">
    <sql id="studentField">
        ${stu}.name, ${stu}.age
    </sql>
    <select id="selectByNameOrAge" resultType="student" parameterType="student">
        select
        <include refid="studentField">
            <property name="stu" value="student"/>
        </include>
        from student
        <where>
            <if test="name != null">
                and name like #{name}
            </if>
            <if test="age != 0">
                and age >= #{age}
            </if>
        </where>
    </select>
</mapper>
```

### 23. foreach Tag

**最常见：**在构建 IN 条件语句的时候。★★

StudentMapper.xml:

```xml
<select id="selectIn" parameterType="student" resultType="student">
    select * from student where age in
    <foreach collection="ages" item="age" open="(" close=")" separator=",">
        #{age}
    </foreach>
</select>
```

DynamicSqlTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    StudentMapper mapper = session.getMapper(StudentMapper.class);
    Student student = new Student();
    student.setAges(new int[]{15, 19});
    System.out.println(mapper.selectIn(student));
}
```

### 24. 关系查询-一对一查询（JavaBean）

StudentMapper.xml:

```xml
<select id="selectStuAndOrder" resultType="result">
    select stuId, name, age, price, datetime
    from student
    	left join fruit_shop_order on student.id = fruit_shop_order.stuId;
</select>
```

DynamicSqlTest.java:

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    StudentMapper mapper = session.getMapper(StudentMapper.class);
    List<Result> results = mapper.selectStuAndOrder();
    for (Result result : results) {
        System.out.println(result.getStuId() + ", " + result.getName() + ", "
                   + result.getPrice() + ", " + result.getDatetime());
    }
}
```

FruitShopOrder.java:

```java
public class FruitShopOrder {
    private int id;
    private int stuId;
    private double price;
    private Timestamp datetime;
    
    // getter and setter...
}
```

Result.java:

```java
public class Result extends FruitShopOrder {
    private String name;
    
    // getter and setter...
}
```

### 25. 一对一查询（ResultMap）：

