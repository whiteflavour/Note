# Note From Official Website

## 获取 Bean（使用 BeanFactory or ApplicationContext）：

### 1. BeanFactory: 

```java
DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(factory);
// 加载 beans.xml 配置文件
reader.loadBeanDefinitions(new FileSystemResource("src/main/resources/beans.xml"));

// 使用 BeanFactory 获取 Bean : 
factory.getBean("alien");
```

### 2. ApplicationContext: 

```java
GenericApplicationContext ctx = new GenericApplicationContext();
XmlBeanDefinitionReader xmlReader = new XmlBeanDefinitionReader(ctx);
xmlReader.loadBeanDefinitions(new ClassPathResource("applicationContext.xml"));
// 加载或者刷新配置文件的持久化数据：（该方法为启动方法，使用 ctx 前必须先调用此方法。★）
ctx.refresh();

// 使用：
ctx.getBean("alien");
```

