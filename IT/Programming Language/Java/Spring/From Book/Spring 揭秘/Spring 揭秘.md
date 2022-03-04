# Spring 揭秘 (2021.5.12 - 2022.3.4)

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

Advisor就是Spring中的 Aspect，但是有不同：Advisor 只有一个Pointcut 和一个 Advice；而理论上Aspect 可以有多个。所以，我们可以认为Advisor 是一种特殊的 Aspect。

**两个分支：**

1. PointcutAdvisor
2. IntroductionAdvisor

### 9.4.1 PointcutAdvisor:

**几个常用实现：**

1. DefaultPointcutAdvisor：最常用
2. NameMatchMethodPointcutAdvisor
3. RegexpMethodPointcutAdvisor：默认使用`JdkRegexpMethodPoinitcut`，可以通过设置`setPerl5(true)`强制使用`Perl5RegexpMethodPointcut`
4. DefaultBeanFactoryPointcutAdvisor：使用较少

### 9.4.2 IntroductionAdvisor：

**与PointcutAdvisor 最本质的区别：**

IntroductionAdvisor 只能应用于类级别的拦截，只能使用 Introduction 型的 Advice。

### 9.5 Spring AOP 的织入：

**最基本的织入器：**`org.springframework.aop.framework.ProxyFactory`。

**两种基本代理方式：**

1. 基于接口
2. 基于类

![AopProxy相关结构图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/AopProxy相关结构图.png)

**AdvisedSupport:**

![AdvisedSupport类层次图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/AdvisedSupport类层次图.png)

1. ProxyConfig：记载生成代理对象的控制信息
2. Advised：承载生成代理对象所需要的必要信息，如相关目标类、Advice、Advisor等

**Advised：**

可以通过 Advised 来设置和查阅一些信息。

直接操作Advised，更多时候用于测试场景。

![ProxyFactory继承层次类图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/ProxyFactory继承层次类图.png)

![ProxyFactory的“兄弟”](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter9/ProxyFactory的“兄弟”.png)

### 9.5.3 容器中的织入器 ── ProxyFactoryBean：

将 Spring AOP 与 Spring的 IoC 容器支持相结合，才是发挥Spring AOP更大作用的最佳途径。

在IoC 容器中，使用 ProxyFactoryBean作为织入器。

**ProxyFactoryBean的本质：**

应该这样断词：Proxy + FactoryBean，而非ProxyFactory + Bean。

ProxyFactoryBean 本质上是一个用来生产 Proxy 的 FactoryBean。跟 FactoryBean 类似，如果容器中某个对象持有某个 FactoryBean 的引用，它取的不是 FactoryBean 本身，而是 FactoryBean 的`getObject()`方法返回的对象。这也是 ProxyFactoryBean 能在容器中游刃有余的原因。

### 9.5.4 加快织入的自动化进程：

使用自动代理机制(Auto Proxy)。

**1. 原理：**

建立在 IoC 容器中的 BeanPostProcessor 概念之上。通过它，我们可以遍历 Bean，并对其进行操作。

**2. 可用的 AutoProxyCreator：**

1. BeanNameAutoProxyCreator：`beanNames`属性中可以使用`*`通配符简化配置；对于 String[] 类型的数组，可以不用`<list>`元素，而使用逗号分隔。
2. DefaultAdvisorAutoProxyCreator：只需在`ApplicationContext`的配置文件中注册下bean定义即可。只对Advisor有效，因为只有Advisor才既有Pointcut信息以捕捉符合条件的目标对象，又有相应的Advice。
   因为他的处理范围比较大，所以为了避免不必要的横切逻辑，应尽量细化各个Advisor的定义，或者转而使用`BeanNameAutoProxyCreator`。

**3. 扩展AutoProxyCreator：**

所有的AutoProxyCreator 都是 InstantiationAwareBeanPostProcessor，其与普通的 BeanPostProcessor 不同。当容器检测到这种类型的 BeanPostProcessor 的时候，会直接通过InstantiationAwareBeanPostProcessor 中的逻辑构造对象实例返回，即“短路”。这样，AutoProxyCreator 会返回代理对象，而非原目标对象。

所以扩展，就继承`AbstractAutoProxyCreator`或者`AbstractAdvisorAutoProxyCreator`。

### 9.6 TargetSource：

### 9.6.1 可用的 TargetSource 实现类：

1. SingletonTargetSource
2. PrototypeTargetSource: 由于每次返回新的对象实例，所以需注意两点：1. bean必须是prototype 2. 通过 targetBeanName 指定Bean定义名称，而非引用。
3. HotSwappableTargetSource：很有用，可用新的目标对象实例替换旧的目标对象实例(`swap()`)。
4. CommonsPoolTargetSource：返回有限数目的目标对象实例，而不是每次都返回新的。（也可以扩展 AbstractPoolingTargetSource）
5. ThreadLocalTargetSource：为不同线程提供不同的目标对象。（该类只是对 JDK的ThreadLocal进行了简单的封装。）

### 9.6.2 自定义 TargetSource：

直接实现TargetSource 接口。或者不在乎是否依赖于容器的话，可以直接扩展`org.springframework.aop.target`包中的几个抽象类。

### 9.7 小结：

重要的是掌握原理，后面的都是秉承着这些理念来进行进化的。

## 第十章、Spring AOP 二世：

### 10.1 @AspectJ 形式的 Spring AOP：

可以使用注解了。

其实本质就是多了一种表达方式，借了一下 AspectJ 的皮。就好像我们学习英语一样，它在世界上的影响范围广，我们学习它，为我所用，这也是一样的。

### 10.1.1 使用：

**1. 编程方式织入：**

使用 AspectJProxyFactory。

**2. 自动代理织入：**

使用 AnnotationAwareAspectJAutoProxyCreator。

使用基于 XSD 的配置方式将AnnotationAwareAspectJAutoProxyCreator 注册进容器：`<aop:aspectj-autoproxy proxy-target="ture"> </aop:aspectj-autoproxy>`。这背后的工作实际上是由`AnnotationAwareAspectJAutoProxyCreator`来做的。

**注意：**

使用@AspectJ形式的AOP的时，尽量使用自动代理法织入（测试除外），因为他们的一些行为并不统一，是有差异的。

### 10.1.2 @AspectJ形式的 Pointcut：

**1. @AspectJ形式Pointcut的声明方式：**

通过使用Pointcut 注解实现。

**2. @AspectJ形式Pointcut表达式的标志符：**

只能使用 AspectJ中的少数。

通常，this 和 target 与其他标志符结合使用，以进一步加强匹配的限定规则。

@within只接受注解类型。

**@within与@target的区别：**

@within静态匹配，@target在运行时点动态匹配。

@args 可以同时指定两个注解参数，但是 Spring 并不理睬。（需要使用逻辑运算符）

@annotation 所接受的注解类型只应用于方法级别，即标注了@Target(ElementType.METHOD) 的注解声明。

> 其实 Spring AOP 和 AspectJ 他们的语义还是有一定区别，虽然 Spring 借用了表达方式，但实现还是使用的 Spring 的底层。★

**有关 Pointcut 表达式以及相关标志符的详细信息：**

参考 AspectJ Programming Guide：http://www.eclipse.org/aspectj/doc/released/progguide/index.html。

**3. @AspectJ形式的Pointcut在 Spring AOP 中的真面目：**

实际上，@AspectJ 形式声明的所有 Pointcut 表达式，在 Spring AOP 内部都会通过解析，转化为具体的 Pointcut 对象。AspectJExpressiontPointcut 就代表 Spring AOP 中面向 AspectJ 的实现。

对 bean 标志的生动介绍 ── 参考 Spring 团队的博文：http://blog.springsource.com/main/2007/09/24/the-new-bean-pointcut/。

### 10.1.3 @AspectJ形式的 Advice：

1. @Before
2. @AfterReturning
3. @AfterThrowing
4. @After
5. @Around
6. @DeclareParents：用于标注 Introduction 类型的 Advice，但它标注对象的域 (Filed)，而非方法 (Method)。

使用起来其实跟前面的差不多。

### 10.1.4 @AspectJ 中的 Aspect 更多话题：

**1. Advice 的执行顺序：**

最先声明的 Advice 有最高优先级。Before Advice 先执行高优先级；AfterReturningAdvice 后执行高优先级。（类比函数嵌套）

注意：如果使用编程的方式来使用Aspect，那么顺序完全由添加到 AspectJProxyFactory 的顺序决定。★

### 10.2.1 基于 Schema 的 AOP 配置概览：

`<aop:config>`和`AutoProxyCreator`两种方式不要一起使用，可能会造成一些问题。★

注意：对于基于 Schema 的 AOP 来说，他的 Aspect 只支持 singleton 实例化模式。

## 第十一章、AOP 应用案例：

### 11.1 异常处理：

使用 AOP 的方式进行异常处理，叫做 Fault Barrier，来自 dev2dev 上的一篇文章："Effective Java Exception"。

文章中，作者把unchecked exception 称为 Fault，而将 checked exception 称为 Contingency。Fault Barrier 要处理的就是 Fault。

### 11.1.2 Fault Barrier：

unchecked exception 实际上可做的事情很少，通常就是记录日志、通知相应人员。所以，这些相同的逻辑可以归并于一处进行处理。

### 11.2 安全检查：

Filter 的资源访问控制，仅仅针对特定领域的安全检查需求，而 AOP 能对任何类型添加安全支持。

现在也有专门的框架，Spring Security。

### 11.3 缓存：

AOP 可以为系统添加缓存，不是业务需求，而是系统需求。

现在也有专门的产品实现，Spring 也有了Spring Cache。

dev2dev 上有一篇文章："Declarative Caching Services for Spring" ── http://dev2dev.bea.com/pub/a/2006/05/declarative-caching.html/，专门介绍如何通过 Spring Cache 为应用程序添加声明性 Caching 支持。

## 第十三章、统一的数据访问异常层次体系：

![异常层次体系简图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter13/异常层次体系简图.png)

## 第十四章、JDBC API 的最佳实践：

Spring 提供了两种使用 JDBC API 的最佳实践：

1. 以 JdbcTemplate 为核心的基于 Template 的 JDBC 使用方式：即直接导入 JDBC 包。
2. 在 JdbcTemplate 基础之上构建的基于操作对象的 JDBC 使用方式：相当于使用框架。

Spring 默认提供面向 Common DBCP、C3P0、Weblogic、WebSphere等数据源的NativeJdbcExtractor 实现类。

可以在`org.springframework.jdbc.support.nativejdbc`包中获取所有这些实现类的更多信息。

## 第十五章、Spring 对各种 ORM 的集成：

### 15.1 Spring 对 Hibernate 的集成：

Hibernate 的详细信息，参考官方文档和相关书籍：《Hibernate基础教程》（人邮出版社，2008.2）、《Hibernate 实战》（人邮出版社，2008.4），这两本书是优秀的 Hibernate 著作。★

## 第十六章、Spring 数据访问之扩展篇：

### 16.1 活用模板方法模式及 Callback：

**各种框架在资源管理上的共性：**

使用后安全地释放这些资源。

与 Bitter Java 所提出的理念相同，为了确保尽可能地将资源的获取和资源的释放操作放在一起，Spring 在数据访问层处理资源的问题上，采用了模板方法模式。

## 第二十二章、迈向 Spring MVC 的旅程：

单独使用 JSP 阶段的 Web 开发，存在许多弊端，可以通过从 Rod Johnson 的 Expert One-on-One J2EE Design and Development 一书中了解更多详情。JSP Model1 也有其先进性，但是切记，不要以这种架构用于实际的生产环境。

## 第二十三章、Spring MVC 初体验：

### 23.1 鸟瞰 Spring MVC：

Spring MVC 中的 Front Controller：DispatcherController，它接收所有请求，并委派给下一级控制器 (Controller) 去实现。

**1. HandlerMapping：**

专门管理 Web 请求到具体处理类的映射关系。

### 23.2 实践出真知：

**1. ContextLoaderListener 与 /WEB-INF/applicationContext.xml ：**

在`web.xml`中首先通过`<listner>`元素添加一个ServletContextListener 的定义，即`ContextLoaderListener`。它为整个 Web 程序加载顶层的 WebApplicationContext (ROOT WebApplicationContext) ，主要用于提供应用所使用的中间层服务。数据源(DataSource)、数据访问对象(DAO)、服务对象(Services)等的定义都在其中注册。

完全可以将其比作独立运行的应用程序中使用的 ClassPathXmlApplicationContext 或者 FileSystemXmlApplicationContext。不过，WebApplicationContext 专门用于 Web 环境下，在其中，我们可以自定义 scope 来注册相应的 bean了，包括 request、session等。

默认路径：`/WEB-INF/applicationContext.xml`。★ 可以使用在`web.xml`中指定名称为`contextConfigLocation`的配置参数来更改它。详情查看`org.springframework.web.context.ContextLoader`，最终是委派给它来进行 WebApplicationContext 的加载。

**ContextLoaderListener之外的选择：**

若不支持，可以使用ContextLoaderServlet 来加载顶层的 WebApplicationContext，但是得通过调整 load-on-startup 的值，使其在其他 Servlet 之前启动。

ContextLoaderListener 和 ContextLoaderServlet 加载相应路径下的容器配置文件，构建完相应的顶层WebApplicationContext 后，将其绑定到 ServletContext。要获取绑定到 ServletContext 的 WebApplicationContext，可以使用`WebApplicationContextUtils`类。

任何类型的 Web 应用程序（基于 Java 的），只要能获取 ServletContext 的引用，就能获取并使用该 WebApplicationContext。即即使当前应用程序没有使用 Spring 提供的基于 IoC 容器的中国年层业务对象管理支持，也可以这样做。

**2. DispatcherServlet 与 XXX-servlet.xml：**

DispatcherServlet 基于 Front Controller。它启动之后加载`<servlet-name>-servlet.xml`配置文件，并构建相应的 WebApplicationContext。将之前通过 ContextLoaderListener 加载的顶层 WebApplicationContext 作为父容器，这样该配置文件中也能注入来自父容器的依赖了。

### 23.2.2 按部就班地开始工作：

**2. 开发独立的业务逻辑：**

虽然 Web 层依赖于业务层对象，但业务层却不应该对 Web 层有任何依赖。Web 层只应该看作是公开业务逻辑的一种视角或者交互方式。

好处：业务层可以独立设计并实现，而不需要关心最终通过什么手段将服务公开给用户（Spring Remoting）。

**4. 添加 HandlerMapping：**

默认使用 BeanNameUrlHandlerMapping。

**5. 实现对应的 Controller 并添加到配置文件：**

扩展AbstractController。

**6. 添加 ViewResolver：**

因为使用 JST/JSTL 作为视图技术，所以使用 InternalResourceViewResolver。

**7. 实现相应的视图：**

对于表格数据的实现，可以使用 DisplayTag 或者 eXtrmeTable 等开源的 Taglib，提高效率。

## 第二十四章、近距离接触 Spring MVC主要角色：

### 24.1 忙碌的协调人 HandlerMapping：

### 24.1.1 可用的 HandlerMapping ：

1. SimpleUrlHandlerMapping
2. ControllerClassNameHandlerMapping
3. DefaultAnnotationHandlerMapping

**补充：Spring 的 PropertiesEditor 的作用：**

将 bean 外部属性转换为内部属性（类型转换）。

### 24.2.2 MultiActionController：

在 4.3 被遗弃，被 Annotated Controllers 替代。

### 24.2.3 SimpleFormController：

专门处理单一表单；AbstractWizardFormController 提供多页面向导的交互能力。

**1. 了解数据绑定：**

为数据绑定一个目标对象，这个对象在 Spring中称为 Command 对象。

> 可以在 org.springframework.beans.PropertyEditorRegistrySupport 的代码中发现所有默认注册的 PropertyEditor类型。

有关绑定的参数表达式与 Command 对象属性之间的设置，可以进一步参考 Spring 文档的 "Bean manipulation and the BeanWrapper"。

从参数获取到参数转型并绑定到 Command 对象，这个过程最终以 ServletRequestDataBinder 的形式进行封装。

**2. Spring 框架数据验证简介：**

核心类：Validator 和 org.springframework.validation.Errors。

除了编程式，还可以借助 Commons Validator (http://commons.apache.org/validator) 或者 Valang (http://opensource.atlassian.com/confluence/spring/display/MODULES/Using+Valang+validator) 实现声明式的数据验证，详情参考 Spring MVC and Web Flow 一书。

**3. 深入表单 (form) 处理流程：**

SimpleFormController 及其父类 AbstractFormController 最主要的特点就是对表单的处理流程进行了统一。可以毫不夸张的说，只要掌握了 AbstractFormController 以及其子类的表单处理流程，就基本掌握了整个本派武功之精髓。

![SimpleFormController处理流程图](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter24/SimpleFormController处理流程图.png)

Backing Object 就是 Command 对象。

### 24.2.4 AbstractWizardFormController：

使用 IDE 创建一个项目，他们会引导我们进行一步步操作。对于这种向导式的简单的多页面流程的实现，就可以使用 AbstractWizardFormController，能简化工作。

注意：它只能处理简单的多页面流程，他所管理的多个页面的数据，最终只绑定到一个 Command 对象上，只不过是每个页面绑定一部分而已。所以如果流程很复杂，建议集成 Spring Web Flow。Expert Spring MVC and Web Flow 一书对其进行了详尽的介绍。

### 24.2.5 其他可用的 Controller 实行：

1. AbstractCommandController：加强型的AbstractController
2. ParameterizableViewController
3. UrlFilenameViewController：处理不用任何处理直接返回的一组视图文件
4. ServletForwardingController和 ServletWrappingController

### 24.3 ModelAndView：

我们倾向于使用逻辑是图名来标志视图，这样灵活性更高。除非必要，尽量不要直接返回具体的View实例。

### 24.3.2 ModelAndView中的模型数据：

模型中的数据对应的键需要与视图模板中的标志相对应。

### 24.4 视图定位器 ViewResolver：

大部分 ViewResolver 实现类，除了BeanNameViewResolver直接实现了 ViewResolver接口，都直接或间接继承自AbstractCachingViewResolver。因为性能原因，Spring 加入了缓存，默认打开。若在测试或者开发环境下，想即刻反映相应的修改结果，可以通过`setCache(false)`暂时关闭 AbstractCachingViewResolver 的缓存功能。

### 24.4.1 可用的 ViewResolver 实现类：

**1. 面向单一视图类型的 ViewResolver：**

1. InternalResourceViewResolver
2. FreeMarkerViewResolver/VelocityViewResolver
3. JasperReportViewResolver
4. XsltViewResolver

更多内容可以参考 Javadoc 或者 Professional Java Development with the Spring Framework 一书。★

**2. 面向多视图类型的 ViewResolver：**

1. ResourceBundleViewResolver：继承了ResourceBundle 的国际化能力。

注意：对于 Velocity （或者 Freemarker）的模板文件，最好将他们放入应用程序的 classpath 中进行加载，而不是依赖于默认的文件系统加载行为。

2. XmlViewResolver：配置文件不同，使用`xml`文件进行配置。
3. BeanNameViewResolver：可以认为是 XmlViewResolver 的原型版或者简化版。多用于快速搭建应用框架原型，或者构建小型的 Web 应用程序。对于正常的 Spring MVC 应用程序，应尽量避免将可以分离出来的视图配置信息一并加入到 DispatcherServlet 的 WebApplicationContext 中。★

### 24.4.2 ViewResolver 查找序列（Chain Of ViewResolver）：

如果为 DispatcherServlet 指定多个 ViewResolver 的话，不要给予 InternalResourceViewResolver 以及其他 UrlBaseViewResolver 子类过高的优先级，因为即使找不到相应的视图，他们也不会返回 null 以给我们轮询下一个 ViewResolver 的机会，这样，我们所指定的其他 ViewResolver 就形同虚设。

### 24.5 各司其职的 View：

### 24.5.2 可用的 View 实现类：

顶层类：AbstractView。他的主要扩展类：AbstractUrlBasedView

**1. 使用 JSP 技术的 View 实现：**

1. InternalResourceView
2. JstlView
3. TilesView: 使用了 Struts 的 Tiles 视图技术。使用时必须提供 DefinitionFactory。
4. TilesJstlView

**2. 使用通用模板技术的 View 实现：**

1. FreeMarkerView
2. VelocityView

**3. 面向二进制文档格式的 View 实现：**

1. AbstractExcelView
2. AbstractJExcelView

**4. 面向 JasperReport 的 View 实现：**

1. AbstractJasperReportsSingleFormatView
2. JasperReportsMultiFormatView

**5. 使用 XSLT 技术的 View 实现：**

1. AbstractXsltView
2. XsltView

**6.RedirectView 和逻辑视图前缀名：**

```java
ModelAndView mav = new ModelAndView("redirect:addUser.do")；
  ...
return mav;
```

### 24.5.3 自定义 View 实现：

继承 AbstractView。或者根据 URL 获取文件的话，直接继承 AbstractUrlBasedView 更好。

## 第二十五章、认识更多 Spring MVC 家族成员：

![三万英尺鸟瞰Spring MVC 的处理流程的逻辑结构](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter24/Chapter25/三万英尺鸟瞰Spring MVC 的处理流程的逻辑结构.png)

![几千米高空再次鸟瞰](/Users/fuck/Documents/Note/IT/Programming Language/Java/Spring/From Book/Spring 揭秘/Pictures/Chapter24/Chapter25/几千米高空再次鸟瞰.png)

### 25.1 文件上传与 MultipartResolver：

使用最多的类库：Commons FileUpload。

**两个可用的 MultipartResolver 实现类：**

1. CommonsMultipartResolver
2. CosMultipartResolver

**两个 PropertyEditor 实现类进行类型转换：**

1. ByteArrayMultipartFileEditor：将 MultipartFile 类型转换为 byte[] 类型
2. StringMultipartFileEditor：将 MultipartFile 转化为 String

### 25.2 Handler 与 HandlerAdaptor：

HandlerAdaptor用于调用不同的 Handler，相当于指挥中心。

**1. 可用的 Handler 类型：**

Spring MVC 提供了一种与 WebWork的 Action 功能类似的 Handler 实现，即 ThrowawayController。它相对于 Handler 的最大优势是，不需要依赖任何 Servlet API，并能够为他们定义状态，这使得它有良好的可测试性。

Spring 2.5 中已被遗弃，预计将在 Spring 3.0 中删除，而被基于注解的 Handler 类型取代。

**2. 自定义 Handler：**

只需想办法标识一下，使其能够被知道是 Handler 类即可，如使用注解。

**对应 HandlerAdaptor 的实现：**

1. SimpleControllerHandlerAdaptor - Controller 的HandlerAdaptor
2. ThrowawayControllerHandlerAdaptor - ThrowawayController
3. AnnotationMethodHandlerAdaptor - 基于注解的 Handler

只要能给出对应的 HandlerAdaptor 的实现，任何类型的 Handler 都能纳入 Spring MVC 使用。

### 25.3 框架内处理流程拦截与 HandlerInterceptor：

HandlerExecutionChain 就是一个数据载体，它包含两方面的数据：

1. 用于处理 Web 请求的 Handler
2. 随同 Handler 遗弃返回的 HandlerInterceptor

### 25.3.1 可用的 HandlerInterceptor 实现：

1. UserRoleAuthorizationInterceptor：对用户角色 (UserRoles) 使用
2. WebContentInterceptor

### 25.3.2 自定义实现 HandlerInterceptor:

继承 HandlerInterceptor。

**Java API 设计的“光荣传统”：**

对于那些需要经常被扩展，又包含多个方法需要实现的接口声明，通常使用者并非都想实现。为了避免每次都要全部实现的繁琐，API 设计者通常都会提供一个 XXXAdapter 类专门用于子类化的需要。注意：不要与 Adaptor 设计模式中的 Adaptor 混淆。

### 25.3.3 HandlerInterceptor寻根：

HandlerMapping是其顶层。所以，要使我们的 HandlerInterceptor 发挥作用，只需将它添加进相应的 HandlerMapping 即可。

### 25.3.4 HandlerInterceptor 之外的选择：

Filter。

**区别：**

1. HandlerInterceptor 拥有更细粒度的拦截点。
2. Filter 有更高的执行优先级

**如何选择？**

对程序中一些普遍关注点进行统一处理，使用 Filter；需要细化处理流程的拦截逻辑，使用 HandlerInterceptor。

**让Filter 更加自由：**

Filter 是 servlet的标准组件，需要在 `web.xml `中配置，这意味着其生命周期管理更多由容器进行。如果我们在实现 Filter 期间需要某些服务的支持，就必须采用某种过度耦合的绑定机制或者查找方式来获取这些服务的支持。

为了让 Filter 的实现更加无拘无束，尽情享受依赖注入，Spring MVC 引入了 DelegatingFilterProxy，使其生命周期由 WebApplicationContext 管理。可以通过`targetFilterLifeCycle`将其值设置为true 来使其还原为原始的 Web 容器管理。

Spring MVC 还在`org.springframework.web.filter`包中提供了多个 Filter 的实现类。

### 25.4 框架内的异常处理与 HandlerExceptionResolver：

只提供了一个实现类：SimpleMappingExceptionResolver。

### 25.5 国际化视图与 LocaleResovler：

### 25.5.1 可用的 LocaleResolver：

1. FixedLocaleResolver：一直保持一个 Locale 值不变，所以不能通过`setLocale`更改。
2. AcceptHeaderLocaleResolver：根据 Accept-Language 协议头解析并返回 Locale 值，因为不能更改 Accept-Language 协议头，故也无法更改其 Locale 值
3. SessionLocaleResolver：可以更改 Locale 值。若无法从 Session 获取，也没有默认 Locale 值，将从 Accept-Language 头获取。
4. CookieLocaleResolver：与Session 类似。只要用户不禁止 Cookie，就能更改 Locale 值。

### 25.5.3 Locale 的变更与 LocaleChangeHandler：

使用LocaleChangeHandler。

### 25.6 主题（Theme）与 ThemeResolver：

由 ThemeSource 负责。

### 25.6.2 管理主题的 ThemeResolver：

解析当前请求的主题是什么。

**三种管理策略：**

除了Accept-Language，其他三种都可以。

### 25.6.3 切换主题的 ThemeChangeInterceptor

## 第二十六章、Spring MVC 中基于注解的 Controller：

实际上就是一个普通的 POJO，使用注解附加了一些相关元数据信息而已。
