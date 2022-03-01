# Spring 揭秘 (2021.5.12 - )

## 序：

**心法：**须知万物溯其源，学东西不是为了学而学，最初是有个场景、问题，然后就是解决方案的提出、选择、权衡、实施、反思和改进。

**对于 Java 学习和应用：**如能掌握精髓，自可海阔鱼跃天高鸟飞，只因心中已修得真经。若方法不当，无人指导作战思路和心得，纵使看了规范、API 和手册，也不解其意，只能硬头先抄，盼经年累月恍然自知，但效率太低。

## 第一章、Spring 框架的由来：

EJB 太笨重，所以就有了灵活的 Spring 。但具体使用什么还是需要根据需求来决定。

> 没有任何一种解决方案是普遍适用的，只有适合用于特定场景的解决方案，脱离具体场景来讨论任何解决方案都是脱体实际的表现。★

![Spring总体结构](F:\Note\IT\Programming Language\Java\Spring\From Book\Spring 揭秘\Pictures\Chapter1\Spring总体结构.png)

(https://blog.csdn.net/wangmaohong0717/article/details/53325104)

抓住了这副骨架，也就抓住了 Spring 框架的学习主线。

只要掌握了 Spring 的理念和方法，就能自己“造轮子“，在相应的应用场景中创造新的”Spring“。★

> Before the dream lifts you into the clouds, make sure look hard at the facts on the ground. ——(Donald J. Trump, How to Get Rich)

## 第二章、IoC 基本概念：

**IoC 理念：**与好莱坞原则：Don't call us, we will call you. 一致。

### 三种注入方式：——(Martin Fowler, Inversion of Control Containers and the Dependency Injection pattern)

1. 构造方法注入：对象被构造完成之后，马上就可以使用。
   （缺点：对象多的时候构造方法的参数列表唱，此时对相同类型的参数处理困难，不好维护和使用；并且 Java 中构造方法无法被继承，无法设置默认值；对非必须的依赖处理，要引入多个构造方法，参数数量上的变动也会不好维护。
2. setter 方法注入：可以在对象构造完成之后注入，使用于不着急使用的场景。
   （优点：除构造方法的缺点对应的部分外，还有良好的 IDE 支持。缺点：对象无法在构造完成之后立马进入就绪状态。）
3. 接口注入：必须实现某个接口，比较死板和烦琐。
   （不提倡使用，因为它强制对象实现不必要的接口，带有侵入性）

## 第四章、BeanFactory

BeanFactory 是最基本的容器，而 ApplicationContext 有更多的功能。

xml 文件的 XSD 格式是较于 DTD 之后出新的，推荐使用。★

### BeanFactory 的使用：

```java
DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(factory);
reader.loadBeanDefinitions(new FileSystemResource("beans.xml"));

factory.getBean("...");
```

### 对一个字符串注入 null：

使用`<null/>`。

### `<bean/>`配置的自动绑定：

**注：**★

1. 手工明确指定的绑定关系总会覆盖自动绑定的行为。
2. 自动绑定只适用于“原生类型、String 以及Classes类型以外“的对象类型，对这些类型及其它们的数组无法自动绑定。

建议手动绑定，因为有良好的 IDE 支持，通常不介意多敲那几个字符，并且有助于自己把握系统的行为。当然，任何事都不是绝对的，找到对于该场景合适的即可。

**技巧：**

可以在`<beans/>`标签中指定一些属性，它们会直接运用于所有的`<bean/>`。★

### 继承：

可以在`<bean/>`中指定 parent 属性，甚至还可以指定 abstract ，避免容器对其实例化，特别是 ApplicationContext 。

### scope 属性中的 singleton and prototype：

singleton 与单例设计模式不同：singleton 保证这种类型的 bean 在同一个容器中只存在一个共享实例；而 Singleton 设计模式则是保证在同一个 ClassLoader 中只存在一个这种类型的实例。

prototype 的 bean，容器每次返回给请求方一个新的对象实例后，就任由它自生自灭了。

**自定义 scpoe ：**

实现 Scope 接口，get() 和 remove() 必须实现。

通常情况下，使用 ConfigurableBeanFactory 的 registerScope() 方法注册自定义 scope 。

### FactoryBean：

容器返回的是 FactoryBean 所生产的类型，而不是 FactoryBean 本身，若要取得其本身，在 bean 定义的 id 之前加 & 。

### Spring 容器较为独特的功能特性：

1. 方法注入。
2. 方法替换。

## 第五章、Spring IoC 容器 ApplicationContext

**几种常用实现：**

1. FileSystemXmlApplicationContext
2. ClassPathXmlApplicationContext
3. XmlWebApplicationContext

### 5.1 统一资源加载策略：

为了各司其职，Spring 提出了一套基于`org.springframework.core.io.Resource`和`ResourceLoader`接口的资源抽象和加载策略。

ClassPathResource就是Resource的一个实现。

要自己实现，实现`Resource`接口就是了。

**ResourcePatternResolver - 批量查找的 ResourceLoader：**

返回多个`Resource`实例，最常用的实现为`PathMatchingResourcePatternResolver`，该实现类支持`ResourceLoader`级别的资源加载，支持基于Ant风格的路径匹配模式（`**/*.suffix`），支持`ResourcePatternResolver`新增加的`classpath*:`前缀等，集所有技能于一身。可以指定一个`ResourceLoader`，否则使用`DefaultResourceLoader`。

![Resource和ResourceLoader类层次图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter5/Resource和ResourceLoader类层次图.png)

**ApplicationContext与ResourceLoader：**

因为`ApplicationContext`继承了`ResourcePatternResolver`，所以任何的`ApplicationContext`的实现都可以看作是一个`ResourceLoader`甚至`ResourcePatternLoader`，这就是`ApplicationContext`支持Spring内统一资源加载策略的真相。

![AbstractApplicationContext作为ResourceLoader和ResourcePatternLoader](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter5/AbstractApplicationContext作为ResourceLoader和ResourcePatternLoader.png)

**ResourceLoader类型的注入：**

实现`ResourceLoaderAware`或`ApplicationContextAware`接口。`ApplicationContextAware`更宽泛。

**Resource类型的注入：**

对于那些Spring容器提供的默认的`PropertyEditors`无法识别的对象类型，我们可以提供自定义的`PropertyEditors`实现并注册进容器中。

默认情况下，`BeanFactory`容器不为`Resource`提供相应的`PropertyEditors`，但是`ApplicationContext`可以正确识别。它使用`ResourceEditorRegistrar`来注册针对`Resource`类型的PropertyEditor，即`ResourceEditor`。

若需依赖一组Resource，可以使用`ResourceArrayPropertyEditor`，然后通过`CustomEditorConfigurar`告知容器。

**特定情况下，ApplicationContext的Resource加载行为：**

ResourceLoader 中增加了新的资源路径协议──`classpath:`，ResourcePatternResolver又增加了`classpath*:`。

ClassPathXmlApplicationContext 默认从 classpath 中加载bean定义配置文件；而 FileSystemXmlApplicationContext从文件系统中加载。

### 5.2 国际化信息支持（I18n MessageSource)：Internationalization，中间有18个字母，通常简写为I18n

要全面了解Java中的I18n，建议参考O'Reilly出版的 Java Internationalization。

Java 国际化信息处理主要涉及两个类：java.util.Local 和 java.util.ResourceBundle。通常，ResourceBundle 管理一组信息序列，所有的信息序列有统一的一个basename，然后特定的Local信息，可以根据basename后追加的语言或者地区代码来区分，如：

```properties
messages.properties
messages_zh.properties
messages_zh_CN.properties
messages_en.properties
messages_en_US.properties
```

注意：properties文件中的编码应该是ISO-8859-1，所以messages_zh_CN.properties中的各个键对应的内容不应该是中文，应该使用 native2ascii或者是类似的工具进行转码。

**MessageSource 与 ApplicationContext：**

Spring 提供了`MessageSource`。

如果ApplicationContext找不到MessageSource的实现，那么其内部会默认实例化一个不含任何内容的StaticMessageSource实例，以保证相应的方法调用。若要添加`MessageSource`的实现，自己在配置文件中添加即可。

**可用的MessageSource实现：**

1. StaticMessageSource：多用于测试，不应该用于生产环境。
2. ResourceBundleMessageSource：有缓存，最常用。
3. ReloadableResourceBundleMessageSource：可定期检查并刷新properties文件的变更，所以应该避免将信息资源文件放到classpath中，这会影响其检查。

上述三种都能独立于ApplicationContext运行。

![MessageResource类层次结构](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter5/MessageResource类层次结构.png)

**MessageSourceAware和MessageSource的注入：**

ApplicationContext自动识别MessageSourceAware，最简单的方法是让需要国际化的类实现`MessageSourceAware`接口，然后注册到ApplicationContext容器，但是这样对容器的依赖性太强，显得容器具有较强的侵略性。

应该直接通过构造方法或者setter方法注入的方式声明依赖，配置bean时，将ApplicationContext容器内部的那个messageSource注入该业务对象即可。

**既然MessageSource可以独立使用，为什么还让ApplicationContext实现它？**

在Web应用程序中通常会公开ApplicationContext给视图层(View)，这样，通过标签(tag)就可以直接访问国际化信息了。

### 5.3 容器内部事件发布：

Java SE: java.util.EventObject和EventListener。

涉及三个角色：自定义事件类型、事件监听器和事件发布者。

Spring：ApplicationEvent（三个实现：ContextClosedEvent, ContextRefreshedEvent, RequestHandleEvent）、ApplicationListener。可以自动识别。

ApplicationContext还继承了ApplicationEventPublisher接口，并充当事件发布者。它将活转包给ApplicationEventMulticaster及其子类SimpleApplicationEventMulticaster。但是，默认使用`SyncTaskExecutor`进行发布。可以提供其它类型的`TaskExecutor`。

ApplicationContext的事件发布机制只适用于单一容器内的简单消息通知和处理，并不适合分布式、多进程、多容器之间的事件通知，虽然可以曲折地通过使用Spring的Remoting，但弊大于利、失大于得。

可以脱离容器直接使用`ApplicationEventMulticaster`进行事件发布。

### 5.4 多配置模块加载的简化：

通过ApplicationContext，可以以String[] 形式传入这些配置文件所在的路径，支持通配符。

## 第六章、IoC容器扩展篇：

### 6.1.1 注解版的自动绑定(@Autowired)：

`AutowiredAnnotationBeanPostProcessor`是BeanPostProcessor的实现，可以自动检测`@Autowired`，只需要在配置文件中添加一个该类的`bean`定义即可。（必须使用`ApplicationContext`容器）

**`@Qualifier`的陪伴：**

@Autowired 是按类型匹配的；@Qualifier 按名字匹配。在@Autowired 后面增加@Qualifier语句，可以作进一步限定。

@Qualifier 还可以用于标注注解类型，这主要用于自定义@Qualifier 的场合。

### 6.1.2 @Autowired 之外的选择──使用JSR250 标注依赖注入关系：

三个可用：@Resource, @PostConstruct和@PreDestroy。

@Resource 与 @Autowired不同，它是 byName 来进行自动绑定的。

@PostConstruct 和 @PreDestroy 不是服务于依赖注入的，而是用于标注对象生命周期管理相关方法的，相当于Spring中的`init-method`和`destroy-method`。

同时JSR250的注解也需要一个BeanProcessor，即`CommonAnnotationBeanPostProcessor`。

可以使用`<context:annnotation-config>`一键搞定上述所有配置。

可以把两个派系的代码混合使用，只要别造成使用上的混乱即可。

### 6.1.3 classpath-scanning 功能介绍：

`<context:component-scan base-package="org.spring21"/>`

从顶层 (org.spring21) 开始扫描，当扫到某个类进行了相应的注解标注后，就会提取该类的相关信息，构建对应的 BeanDefinition，然后将其注册进容器。

可以对`base-package`进行过滤：

```properties
<context:component-scan base-package="org.spring21">
	<context:include-filter type="annotation" expression="cn.spring21.annotation.FXService"/>
	<context:exclude-filter type="aspectj" expression=".."/>
</context:component-scan>
```

## 第七章、一起来看AOP：

存在一个横切关注点，即很多地方都需要插入的一段代码、文件。。，如：日志，此时我们使用 AOP 将其织入即可，减少实现代码分布散乱的麻烦。

### 7.4 AOP国家的公民：

### 7.4.1 Joinpoint：

织入点。

### 7.4.2 Pointcut：

织入点的表达方式。（横切逻辑）

### 7.4.3 Advice：

单一横切关注点逻辑的载体。

主要有以下几种：

1. Before Advice
2. After Advice

   1. After returning Advice

   2. After throwing Advice

   3. After Advice：或许叫 After (Finally) Advice 更确切
3. Around Advice: J2EE 中的 `Filter`实际上就是`Around Advice`的一种体现。
4. Introduction: 不根据横切逻辑的时机，而根据它可以完成的功能来区别。Introduction 可以为原有的对象添加新的特性或行为，就像你是一个普通公民，给你穿军装、戴军帽，添加了军人类型的Introduction之后，你就拥有军人的特征或者行为。
   Introduction类型的Advice因实现技术不同，在具体软件环境中可能存在性能差异。

### 7.4.4 Aspect

是对系统中横切关注点逻辑进行封装的 AOP 概念实体。可以包含多个 Pointcut 和 Advice 相关定义。

## 第八章、Spring AOP 概述及其实现机制：

Spring AOP 简单而强大，如果它无法满足你，求助 AspectJ 好了。

### 8.2 Spring AOP 的实现机制：

属于二代 AOP，采用动态代理和字节码生成技术实现，在运行期间为目标对象生成一个代理对象，最终将代理对象织入，而非目标对象。

实际上起源于代理设计模式。

### 8.2.2 动态代理：

主要有`java.lang.reflect.Proxy`和`java.lang.reflect.InvocationHandler`组成。

**动态代理的缺点：**

只能对实现了相应的 Interface 接口的类使用。

如果Spring AOP 发现目标对象没有实现任何 Interface，则会尝试使用一个称为 CGLIB (Code Generation Library) 的开源动态字节码生成类库，为目标对象生成动态的代理对象实例。

> Java Reflection In Action (Manning, 2005) 对Java的 Reflection 机制进行了详尽的阐述，其中有一章专门讲解了动态代理机制，不妨一读。

### 8.2.3 动态字节码生成：

**原理：**

对目标对象进行继承扩展，为其生成相应的子类，而子类通过覆写来扩展父类的行为，只要将横切逻辑的实现放到子类中，然后让系统使用它，就可以达到与代理模式相同的效果了。

对类进行扩展，首先需要实现一个`net.sf.cglib.proxy.Callback`，但更多时候我们直接使用`net.sf.cglib.proxy.MethodInterceptor`接口。

**CGLIB唯一的限制：**

无法对 final 方法进行覆写。

**CGLIB官网：**

http://cglib.sourceforge.net/。不过，文档并不多，读代码或许更加实际。

## 第九章、Spring AOP 一世：

虽然Spring AOP有两代，但是实现机制没变。

### 9.1 Joinpoint：

Spring AOP 仅支持方法级别的Joinpoint。

### 9.2 Pointcut：

`org.springframework.aop.Pointcut`接口是Pointcut中最顶层的抽象。

![Pointcut局部“族谱”](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/Pointcut局部“族谱”.png)

### 9.2.1 常见的Pointcut：

1. NameMatchMethodPointcut
2. JdkRegexpMethodPointcut
3. Perl5RegexpMethodPointcut
4. AnnotationMatchingPointcut
5. ComposablePointcut：提供逻辑运算
6. ControlFlowPointcut：可以指定只有当某个特定的类调用某方法时才对该方法进行拦截，而不管其他类。

> ControlFlowPointcut 每次方法调用时都需要在运行期间检查程序的调用栈，所以性能较差。

### 9.2.2 扩展 Pointcut（Customize Pointcut）：

可以通过实现`StaticMethodMatcherPointcut`和`DynamicMethodMatcherPointcut`来自定义Pointcut。

### 9.3 Advice：

Spring AOP 加入了开源组织 AOP Alliance (http://aopalliance.sourceforge.net/)，目的在于标准化 AOP 的使用，促进各个AOP实现产品之间的可交互性。

![Spring中Advice略图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/Spring中Advice略图.png)

Advice按照其自身实例(instance) 能否在目标对象类的所有实例中共享这一标准，分为两大类：

1. per-class类型
2. per-instance

### 9.3.1 per-class 类型的 Advice：

该类型的Advice实例可以在目标对象类的所有实例之间共享。通常只提供方法拦截的功能，不会为目标对象类保存任何状态或者添加新的特性。

除了Introduction类型的Advice外，其他都属于该类型。

**1. Before Advice：**

实现`org.springframework.aop.MethodBeforeAdvice`即可。是标志接口，该接口中没有任何方法。

**2. ThrowsAdvice：**

同理，实现`ThrowsAdvice`即可。

**3. AfterReturningAdvice：**

虽然可以访问到方法的返回值，但是不能更改，要更改需要用到 Around Advice。

**4. Around Advice：**

Spring AOP 没有提供After (Finally) Advice；AfterReturningAdvice 不能更改返回值。所以，是 Around Advice 的时候了。

Spring没有直接提供定义对应 Around Advice的实现接口，而是直接采用了 AOP Alliance 的标准接口：`org.aopalliance.intercept.MethodInterceptor`，该接口**神通广大**：系统安全验证及检查、系统各处的性能检测、简单的日志记录以及系统附加行为的添加等，样样精通。

记得调用MethodInterceptor的`proceed()`方法，除非你知道你在做什么，否则程序的执行会在当前MethodInterceptor处”短路“，Jointpoint 上的调用链将被中断，同一Joinpoint上的其他 MethodInterceptor 的逻辑以及 Jointpoint 处的方法逻辑不会执行。

### 9.3.2 per-instance：

**Introduction：**

实现`IntroductionInterceptor`即可。

不用执行`proceed()`方法，因为当前被拦截方法就是整个调用链中要最终执行的唯一方法。

![Introduction相关类结构图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/Introduction相关类结构图.png)

**两条分支：**

1. 以DynamicIntroductionAdvice为首的动态分支：可以到运行时再去判定当前Introduction可应用到的目标接口类型，而不用预先就设定
2. IntroductionInfo 的静态分支：与上述相反。

要添加 Introduction 逻辑，使用 Spring 的两个实现类即可：（或者干脆直接自己实现IntroductionInterceptor接口）

1. DelegatingIntroductionInterceptor：不自己实现行为，而是委派(delegate) 给其他实现类。它会使用它所持有的同一个”delegate“接口实例，供同一个目标类的所有实例共享使用。
2. DelegatePerTargetObjectIntroductionInterceptor：如果根据当前目标对象实例没有找到对应的Introduction 实现类实例，该类就将会为其创建一个新的，然后添加到映射关系中。

**这两个类的唯一区别：**

在于构造方式上：我们不是自己构造delegate接口实例，而是告知DelegatePerTargetObjectIntroductionInterceptor相应的delegate 接口类型和对应实现类的类型就可以了。

**扩展上述两个类或者IntroductionInterceptor接口的情况：**

通常是因为目标对象的行为，与新附加到目标对象的状态和行为相关联。

**Introduction的性能问题：**

Spring AOP采用的动态代理机制，性能比AspectJ 的直接通过编译器将Introduction 织入目标对象逊色不少。若有必要，可以考虑采用 AspectJ 的Introduction 实现。

### 9.4 Spring AOP 中的 Aspect：

