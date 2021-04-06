# web.xml 问题（2021.4.2 —— ）

IDEA 提示一些标签不允许出现在此位置，但这个标签却是在正确的位置（报 Element is not allow here 错误 )：

如：`<filter-mapping>`的`<dispatcher>`标签：

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>My Web Application</display-name>

  <filter>
    <filter-name>normalFilter</filter-name>
    <filter-class>com.google.filter.AnyRequestFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>normalFilter</filter-name>
    <url-pattern>/*</url-pattern>
      
    <!--此处报错-->
    <!--Element dispatcher is not allow here. -->
    <dispatcher>REQUEST</dispatcher>

  </filter-mapping>
</web-app>
```

**解决办法**：

将 web.xml 文件头的：

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
```

替换为：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
```

**参考**：https://blog.csdn.net/wang415834554/article/details/52997514 