# Spring Framework （小马哥）

## 第一章：Spring Framework总览 (12讲)

### 01 | 课程介绍

生态：
1.SpringBoot
2.SpringCloud
3.SpringSecurity



细节：
1.Java语言特性

反射、动态代理、枚举、泛型、注解、ARM和Lambda语法

2.设计思想和模式的实现

OP、lOC、DDD、TDD、GoF23等

3.Java API的封装与简化

JDBC事务Transaction Servlet

JPA JMX Bean Validation

4.JSR规范的适配与实现

5.第三方框架的整合



优势

API抽象

模块化设计

功能稳定性

功能可扩展性、可测试性



### 02 | 内容综述



1.特性

按需分配

胶水：API和或者规范整合在一起

2.使用API

Spring 3 对Java 5 的支持（注解）

Spring 5 对Java 8 的支持

Java: XML、反射、动态代理

JavaEE: Servlet、Jsp、Jpa、Jms

3.自己的实现

* 面向对象（OOP）：多态，接口对应语义


* 切面编程：jdk动态代理、ASM、CGLIB、AspectJ 类的提升

* 面向元编程

配置元信息包含三种

配置类：配置属性在XML或者.properties文件，会影响运行时的一些状态，比如影响依赖注入的方式

注解

属性配置：占位符、外部化配置



不是面向程序来编程，在程序的基础上在进行元数据的一些处理

* 面向模块编程 

* 面向函数编程 



### 03 | 课前准备：学习三件套（工具、代码与大脑）

方法

基础:夯实基础,了解动态
思考:保持怀疑，验证一切
分析:不拘小节,观其大意
实践:思辨结合，学以致用

工具
JDK: Oracle JDK 8
Spring Framework: 5.2.2.REL EASE
IDE: IDEA 2019 (Community)
Maven: 3.2 +


### 04 | 特性总览：核心特性、数据存储、Web技术、框架整合与测试

1. 核心特性(Core)

* IoC(IoC Container)
* Spring事件(Events)
* 资源管理(Resources)
* 国际化(i18n)
* 校验(Validation )
* 数据绑定(Data Binding)
* 类型转换(Type Conversion)
* Spring表达式(Spring Express Language )
* 面向切面编程(AOP)



2.数据存储(Data Access)

* JDBC
* 事务抽象(Transactions)
* DAO支持(DAO Support)
* O/R映射(O/R Mapping)
* XML编列(XML Marshalling)



3.Web技术(Web)

* Web Servlet技术栈
  * Spring MVC
  * WebSocket
  * SockJS
* Web Reactive技术栈
  * Spring WebFlux
  * WebClient
  * WebSocket

当然Reactive它也是可以运用Spring MVC的，也可以运用到Servlet引擎来进行实现。

在Spring框架5.0之前，有另外一个东西叫做RestTemplate，或者是有个叫做HttpClient，是这个同步的。那么WebClient引用之后，它把过去的同步执行变成异步回调的方式。



4.技术整合(Integration)

* 远程调用(Remoting)
* Java 消息服务 (JMS)
* Java连接架构( JCA)
* Java 管理扩展(JMX)
* Java 邮件客户端 (Email)
* 本地任务(Tasks)
* 本地调度(Scheduling)
* 缓存抽象(Caching)
* Spring测试(Testing)

通常来说远程调用是采用的同步的模式。

JMX 运维侧，查看CUP、磁盘利用率等。



5.测试(Testing)

* 模拟对象(Mock Objects)
* TestContext 框架(TestContext Framework)
* Spring MVC测试(Spring MVC Test)
* Web 测试客户端(WebTestClient)



Mock对象我们可以去动态的去生成它，比如说在Spring Framework里面，它生成的这么一个MockHttp这么一个接口。



### 05 | Spring版本特性：Spring各个版本引入了哪些新特性？

####                                                            **Java版本依赖与支持**

|Spring Framework版本|Java标准版|Java企业版|
|:-:|:-:|:-:|
|1.x|1.3+|J2EE 1.3 +|
|2.x|1.4.2+|J2EE 1.3 +|
|3.x|5+|J2EE 1.4和Java EE 5|
|4.x|6+|JavaEE6和7|
|5.x|8+|Java EE 7|


### 06 | Spring模块化设计：Spring功能特性如何在不同模块中组织？

1. Spring模块化设计(Modular)

* spring-aop 
* spring-aspects
* spring-jms
* spring-context-indexer
* spring-messaging
* spring-context-support
* spring-orm
* spring-context
* spring-oxm
* spring-core
* spring-test
* spring-expression
* spring-tx
* spring-instrument
* spring-web
* spring-jcl
* spring-webflux
* spring-jdbc
* spring-webmvc
* spring-websocket

模块化：按需分配



### 07 | Java语言特性运用：各种Java语法特性是怎样被Spring各种版本巧妙运用的？

![java语法变化](/img/java语法变化.png)



* Java 5语法特性

|语法特性|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|注解(Annotation)|1.2 +|@Transactional|
|枚举(Enumeration)|1.2 +|Propagation|
|for- each语法|3.0 +|AbstractApplicationContext|
|自动装箱(AutoBoxing)|3.0 +||
|泛型(Generic)|3.0 +|ApplicationListener|

* Java 6语法特性
|语法特性|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|接口@Override|4.0 +|

* Java 7语法特性
|语法特性|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|Diamond语法|5.0 +|DefaultListableBeanFactory|
|try-with-resources语法|5.0 +|ResourceBundleMessageSource|

* Java 8语法特性
|语法特性|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|Lambda语法|5.0 +|PropertyEditorRegistrySupport|


### 08 | JDK API实践：Spring怎样取舍Java I/O、集合、反射、动态代理等API的使用？

* < Java5 API
|API类型|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|反射(Reflection)|1.0 +|MethodMatcher|
|Java Beans|1.0 +|CachedIntrospectionResults|
|动态代理(Dynamic Proxy)|1.0 +|JdkDynamicAopProxy|

Java反射是从ava 1.2

还会借助于像AspectJ来进行实现


* Java 5 API
|API类型|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|XML处理(DOM,SAX..)|1.0 +|XmlBeanDefinitionReader|
|Java管理扩展(JMX)|1.2 +|@ManagedResource |
|Instrumentation|2.0 +|InstrumentationSavingAgent|
|并发框架(J.U.C)|3.0 +|ThreadPoolT askScheduler|
|格式化(Formatter)|3.0 +|DateFormatter|

XmlBeanDefinitionReader：把XML内容就XML配置文件，读取为BeanDefinition 。

InstrumentationSavingAgent：API可以帮助我们去做字节码的一个重写。做字节码的一个提升。大多数Agent的实现都是基于这个API来进行实现的。


* Java 6 API
|API类型|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|JDBC 4.0 (JSR 221)|1.0 +|JdbcTemplate|
|Common Annotations (JSR 250)| 2.5 +|CommonAnnotationBeanPostProcessor|
|JAXB 2.0 (JSR 222)|3.0 +|Jaxb2Marshaller|
|Scripting in JVM (JSR 223)|4.2 +|StandardScriptFactory|
|可插拔注解处理API (JSR 269)|5.0 +|@Indexed|
|Java Compiler API (JSR 199)|5.0 +|TestCompiler (单元测试)|

JSR 250：@Resource这一个注解就在里面，比如说PostConstruct或者PreDestroy都是这个API里面实现的。

JAXB 2.0：ava API for XML Binding,Java API去绑定XML的实现,里面就会有个marshal、unmarshal的操作。

SpringBoot 注解的使用需求出现了急剧性的膨胀，注解的实现就来自于两个方面：ASM、标准的Java反射，都是运行时实现。

通过编译时来进行实现@Indexed：Component的基础上面，编译时把API去做一个相当于说建立索引，能够帮助我快速的定位到
到底哪个类建了Component索引，那么这时候我就可以定位到类而不需要逐一扫描。

* Java 7 API
|API类型|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|Fork/Join框架(JSR 166)|3.1 +|ForkJoinPoolFactoryBean|
|NIO 2 (JSR 203)|4.0 +|PathResource|

* Java 8 API
|API类型|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|Date and Time API (JSR 310)|4.0 +|Date TimeContext|
|可重复Annotations (JSR 337)|4.0 +|@PropertySources|
|Stream API (JSR 335)|4.2 +|StreamConverter|
|CompletableFuture (J.U.C)|4.2 +|CompletableToListenableFutureAdapter|


解决过去时间可变的情况

### 09 | Java EE API整合：为什么Spring要与“笨重”的Java EE共舞？

* Java EE Web技术相关
|JSR规范|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|Servlet + JSP(JSR 035)|1.0 +|DispatcherServlet|
|JSTL(JSR 052)|1.0 +|JstlView|
|JavaServer Faces(JSR 127)|1.1 +|FacesContextUtils|
|Portlet(JSR 168)|2.0 - 4.2|DispatcherPortlet|
|SOAP(JSR 067)|2.5 +|SoapFaultException|
|WebServices(JSR 109)|2.5 +|CommonAnnotationBeanPostProcessor|
|WebSocket(JSR 356)|4.0 +|WebSocketHandler|

* Java EE数据存储相关
|JSR规范|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|JDO(JSR 12)|1.0 - 4.2|JdoTemplate|
|JTA(JSR 907)|1.0 +|JtaTransactionManager|
|JPA(EJB 3.0 JSR 220的成员)|2.0 +|JpaTransactionManager|
|Java Caching API(JSR 107)|3.2 +|JCacheCache|

* Java EE Bean技术相关
|JSR规范|Spring支持版本|代表实现|
|:-:|:-:|:-:|
|JMS(JSR 914)|1.1 +|JmsTemplate|
|EJB 2.0 (JSR 19)|1.0 +|AbstractStatefulSessionBean|
|Dependency Injection for Java(JSR 330)|2.5 +|AutowiredAnnotationBeanPostProcessor|
|Bean Validation(JSR 303)|3.0 +|LocalValidatorFactoryBean|




### 10 | Spring编程模型：Spring实现了哪些编程模型？

### 11 | Spring核心价值：我们能从Spring Framework中学到哪些经验和教训呢？

1. 编程模型
* 面向对象主要是以接口为主，面向对象主要是以LP拦截为主；
* 面向元数据主要是一些元信息的一个封装，注解、配置、元数据的调整；



### 12 | 面试题精选

* 沙雕面试题 - 什么是 Spring Framework？
答:
Spring使得创建Java企业应用变得很容易。它提供了拥抱企业环境中所需的一切在Java语言上面，支持Groovy和
Kotlin作为JVM上的可选语言，并与创建多种架构的灵活性取决于应用程序的需求。

* 996面试题- Spring Framework有哪些核心模块?
答:
spring-core: Spring 基础API模块，如资源管理，泛型处理
spring-beans: Spring Bean相关,如依赖查找（BeanFactory）,依赖注入（@Autowired）
spring-aop : Spring AOP处理，如动态代理，AOP字节码提升
spring-context :事件驱动（ApplicationEvent）、注解驱动（@ComponentScan 扫描）、模块驱动（Enable*）等
spring-expression: Spring 表达式语言模块

* 劝退面试题 - Spring Framework 的优势和不足是什么?

## 第二章：重新认识IoC (9讲)

### 13 | IoC发展简介：你可能对IoC有些误会？

在软件工程中，控制反转(IoC)是一种编程原理。IoC反转控制与传统控制流相比（串行）。在IoC中，计算机程序的自定义编写部分
从通用框架接收控制流。采用这种设计的软件体系结构颠倒了控制。与传统程序设计的比较：在传统程序设计中，习惯
表达程序目的的代码调用可重用库来处理泛型任务，但在控制反转中，是框架调用定制的或特定于任务的代码。

### 14 | IoC主要实现策略：面试官总问IoC和DI的区别，他真的理解吗？

在面向对象编程中，有几种基本的技术来实现控制反转。这些是:

* 使用服务定位器模式
* 使用依赖注入，例如
   * 构造函数注入
   * 参数注入
   * Setter注入
   * 接口注入
它通常是由容器帮我们自动去注入一些事情。
* 使用上下文查找
* 使用模板法设计模式
  比如说是Spring JDBC里面会用到,JDBC Template这样的实现,会给我们一种类似于比如说Statement,这样的Callback这种Callback能够帮助我们实现地更为抽象,当我们去实现这样的接口的时候,我们不需要关心Callback从哪来,那么也实现了一种反转控制的方式
* 使用策略设计模式

### 15 | IoC容器的职责：IoC除了依赖注入，还涵盖哪些职责呢？

1. IoC以下设计目的:

* 将任务的执行与实现解耦。

* 关注于这个模块，在其任务上模块它所赋予的一个设计目的，关注最终目标，而不是具体实现。

* 释放模块，其他系统知道它怎么运作，都是不依赖某个契约。（依赖注入替换依赖查找）

* 防止更换模块时产生副作用。

* “控制反转”有时被戏谑地称为“好莱坞原则:不要打电话给我们，我们会呼叫你“。


2. IoC 容器的职责

* 通用职责
* 依赖处理
  * 依赖查找（主动，但是大多数事情被容器做了）
  * 依赖注入
* 生命周期管理
  * 容器
  * 托管的资源（Java Beans 或其他资源）
* 配置
  * 容器
  * 外部化配置
  * 托管的资源（Java Beans 或其他资源）

当然Spring的Bean可以作为事件监听的一个来源，但不是唯一来源。可能是外部进行添加进去的。

Servlet容器：Model2的设计模式，通过JavaEE或者是通过我们的Servlet去获取比如说像数据库源或者是比如说像线程池或者是消息服务，那么也是通过JNDI的方式在我的server容器或者EJB容器或者Java EE容器里面来进行获取。

### 16 | 除了Spring，还有其它的IOC容器实现吗？

### 17 | 传统IoC容器实现：JavaBeans也是IoC容器吗？

1.特性
* 一个可以管理应用程序代码的容器。
* 一个快速启动的容器。
* 不需要任何特殊部署步骤就可以在其中部署对象的容器。
* 一个具有轻量级内存占用和最小API依赖的容器，它可以在各种环境中运行
* 一个在部署工作量和性能方面设置非常低的添加托管对象的门槛的容器
* 部署和管理细粒度对象以及粗粒度组件的开销。

2.优点

* 释放掉一些聚式的容器
* 最大化代码可重用性
* 更大的对象定向
* 更大的生产力
* 更好的测试能力

### 18 | 轻量级IoC容器：如何界定IoC容器的“轻重”？

1.优劣对比
|类型|依赖处理|实现便利性|代码侵入性|API依赖性|可读性|
|:-:|:-:|:-:|:-:|:-:|:-:|
|依赖查找|主动获取|相对繁琐|侵入业务逻辑|依赖容器API|良好|
|依赖注入|被动提供|相对便利|低侵入性|不依赖容器API|一般|

依赖查找需要主动查找：所以它对业务逻辑会带来一定的伤害，必然会耦合一些API（eg：BeanFactory查找）

依赖注入浸入性相对来说比较低(eg：@Autowired)

不依赖API不依赖容器API，不代表没有侵入性


### 19 | 依赖查找 VS. 依赖注入：为什么Spring总会强调后者，而选择性忽视前者？

Spring团队通常提倡构造函数注入，因为它允许您将应用程序组件实现为不变的对象，并确保所需的依赖项不为空。
此外,constructor-injected组件始终以完全初始化状态返回给客户机(调用)代码。大量的构造函数
参数是一种糟糕的体验，意味着类可能有太多的责任，应该重构
更好地解决问题的适当分离。

Setter注入应该主要用于可选的依赖项，这些依赖项可以被分配合理的默认值在类。否则，必须在代码使用依赖项的任何地方执行非空检查。

有个类叫ObjectProvider这个类，它是种类型安全的方式，如果你的依赖注入的方式或者依赖查找的方式，是一个单一类型的话，它会调用getIfAvailable的方法来进行示范性地去返回
那么等于空的时候它就会返回空,这种方式在Spring Boot的场景经常用到。

当我们的Bean初始化之后是不变的对象，对我们的程序和维护性都会带来更多的便利。


### 20 | 构造器注入 VS. Setter 注入：为什么Spring官方文档的解读会与作者的初心出现偏差？

### 21 | 面试题精选

* 沙雕面试题 - 什么是 IoC ？
答：简单地说，IoC 是反转控制，类似于好莱坞原则，主要有依赖查找和依赖注入实现

包括我们说消息其实也算，因为消息其实是被动的，我们如果说我们传统的调用链路是一个主动拉的模式，那么IoC其实是一种推的模式
那么推的模式在消息事件以及各种这样类似于这种反向的观察者模式的扩展都属于IoC。

* 996 面试题 - 依赖查找和依赖注入的区别？
答：依赖查找是主动或手动的依赖查找方式，通常需要依赖容器或标准 API实现。而依赖注入则是手动或自动依赖绑定的方式，无需依赖特定的容器和API

* 劝退面试题 - Spring 作为 IoC 容器有什么优势？
答：
典型的 IoC 管理，依赖查找和依赖注入
AOP 抽象
事务抽象
事件机制
SPI 扩展(包括BeanPostProcessor、BeanFactoryPostProcessor、Spring Factories)
强大的第三方整合
易测试性
更好的面向对象

## 第三章：Spring IoC容器概述 (9讲)

### 22 | Spring IoC依赖查找：依赖注入还不够吗？依赖查找存在的价值几何？

### 23 | Spring IoC依赖注入：Spring提供了哪些依赖注入模式和类型呢？

依赖注入和依赖查找来源并不是同一个

## 24 | Spring IoC依赖来源：依赖注入和查找的对象来自于哪里？

1.Spring IoC 依赖来源
* 自定义 Bean
* 容器內建 Bean 对象
* 容器內建依赖

BeanFactory对象不是內建 Bean 对象，而是容器內建依赖，非SpringBean。

### 25 | Spring IoC配置元信息：Spring IoC有哪些配置元信息？它们的进化过程是怎样的？

* Bean 定义配置
  * 基于 XML 文件
  * 基于 Properties 文件
  * 基于 Java 注解
  * 基于 Java API（专题讨论）
* IoC 容器配置
  * 基于 XML 文件
  * 基于 Java 注解
  * 基于 Java API （专题讨论）
* 外部化属性配置
  * 基于 Java 注解

### 26 | Spring IoC容器：BeanFactory和ApplicationContext谁才是Spring IoC容器？

BeanFactory接口提供了一种高级配置机制，能够管理任何类型的对象。ApplicationContext是BeanFactory的一个子接口。
更容易与Spring的AOP特性集成
* 消息资源处理(用于国际化)
* 事件发表
* 应用程序层特定的上下文，如用于web应用程序的WebApplicationContext。

简而言之，BeanFactory提供了配置框架和基本功能，以及应用程序ionContext添加更多特定于企业的功能。ApplicationContext是BeanFactory的一个完整超集。


### 27 | Spring应用上下文：ApplicationContext除了IoC容器角色，还提供哪些特性？

* ApplicationContext 除了 IoC 容器角色，还有提供：
  * 面向切面（AOP） 
  * 配置元信息（Configuration Metadata） 
  * 资源管理（Resources） 
  * 事件（Events） 
  * 国际化（i18n） 
  * 注解（Annotations） 
  * Environment 抽象（Environment Abstraction）

### 28 | 使用Spring IoC容器：选BeanFactory还是ApplicationContext？

### 29 | Spring IoC容器生命周期：IoC容器启停过程中发生了什么？

启动：
第一个操作是创建我们的BeanFactory，并且进行初步的初始化，加入些我们的内建的一些Bean对象或者Bean依赖，以及加上一些内建的非Bean的依赖。
第二部分就是关于BeanFactory的扩展点，通过执行BeanFactoryPostProcessor。
第三个是对Bean的一些修改或者扩展，通过执行这个BeanPostProcessor来进行操作，这个操作这里只是注册，具体的调用是在BeanFactory里面进行操作的。
再接下来就会定义我们说的国际化事件等


### 30 | 面试题精选

* 沙雕面试题 - 什么是 Spring IoC 容器？
Spring框架实现的控制反转(IoC)原则。IoC也称为依赖注入(DI)。DI是IOC的一种实现方式，还有依赖查找，
看通过构造函数参数，属性的setter方式来注入一些其他的对象，来完成依赖注入。

* 996 面试题 - BeanFactory 与 FactoryBean？

BeanFactory 是 IoC 底层容器
FactoryBean 是 创建 Bean 的一种方式，帮助实现复杂的初始化逻辑

* 劝退面试题 - Spring IoC 容器启动时做了哪些准备？
答：IoC 配置元信息读取和解析、IoC 容器生命周期、Spring 事件发布、国际化等，更多答案将在后续专题章节逐一讨论

## 第四章：Spring Bean基础 (11讲)

### 31. 如何注册一个Spring Bean?
什么是 BeanDefinition？ 
* BeanDefinition 是 Spring Framework 中定义 Bean 的配置元信息接口，包含：
  * Bean 的类名
  * Bean 行为配置元素，如作用域、自动绑定的模式，生命周期回调等
  * 其他 Bean 引用，又可称作合作者（collaborators）或者依赖（dependencies） 
  * 配置设置，比如 Bean 属性（Properties） 

### 31 | 定义Bean：什么是BeanDefinition？

* BeanDefinition 构建
  * 通过 BeanDefinitionBuilder
  * 通过 AbstractBeanDefinition 以及派生类

### 32 | BeanDefinition元信息：除了Bean名称和类名，还有哪些Bean元信息值得关注？



### 33 | 命名Spring Bean：id和name属性命名Bean，哪个更好？

* 自动生成
* 自己定义

### 34 | Spring Bean的别名：为什么命名Bean还需要别名？

到了第三方的一个jar包或者是相关的依赖资源，可以通过新的名称来进行更场景化的一个依赖。

### 35 | 注册Spring Bean：如何将BeanDefinition注册到IoC容器？

BeanDefinition 注册
* XML 配置元信息
  * <bean name=”...” ... />
* Java 注解配置元信息
  * @Bean
  * @Component
  * @Import
* Java API 配置元信息
  * 命名方式：BeanDefinitionRegistry#registerBeanDefinition(String,BeanDefinition)
  * 非命名方式：BeanDefinitionReaderUtils#registerWithGeneratedName(AbstractBeanDefinition,BeanDefinitionRegistry)
  * 配置类方式：AnnotatedBeanDefinitionReader#register(Class...)注

### 36 | 实例化Spring Bean：Bean实例化的姿势有多少种？
Bean 实例化（Instantiation）
*  常规方式
  * 通过构造器（配置元信息：XML、Java 注解和 Java API ）
  * 通过静态工厂方法（配置元信息：XML 和 Java API ）
  * 通过 Bean 工厂方法（配置元信息：XML和 Java API ）
  * 通过 FactoryBean（配置元信息：XML、Java 注解和 Java API ）
* 特殊方式
  * 通过 ServiceLoaderFactoryBean（配置元信息：XML、Java 注解和 Java API ）
  * 通过 AutowireCapableBeanFactory#createBean(java.lang.Class, int, boolean)
  * 通过 BeanDefinitionRegistry#registerBeanDefinition(String,BeanDefinition)
  
### 37 | 初始化Spring Bean：Bean初始化有哪些方式？

Bean 初始化（Initialization）
* @PostConstruct 标注方法
* 实现 InitializingBean 接口的 afterPropertiesSet() 方法
* 自定义初始化方法
  * XML 配置：<bean init-method=”init” ... />
  * Java 注解：@Bean(initMethod=”init”)
  * Java API：AbstractBeanDefinition#setInitMethodName(String)

### 38 | 延迟初始化Spring Bean：延迟初始化的Bean会影响依赖注入吗？

* Bean 延迟初始化（Lazy Initialization）
  * XML 配置：<bean lazy-init=”true” ... />
  * Java 注解：@Lazy(true)
### 39 | 销毁Spring Bean： 销毁Bean的基本操作有哪些？

### 40 | 回收Spring Bean：Spring IoC容器管理的Bean能够被垃圾回收吗？
* Bean 垃圾回收（GC）
  * 1. 关闭 Spring 容器（应用上下文）
  * 2. 执行 GC
  * 3. Spring Bean 覆盖的 finalize() 方法被回调
### 41 | 面试题精选

* 沙雕面试题 - 如何注册一个 Spring Bean？

答：通过 BeanDefinition 和外部单体对象来注册

* 996 面试题 - 什么是 Spring BeanDefinition？
答：回顾“定义 Spring Bean” 和 “BeanDefinition 元信息”

* 劝退面试题 - Spring 容器是怎样管理注册 Bean
答：答案将在后续专题章节详细讨论，如：IoC 配置元信息读取和解析、依赖查找和注入以及 Bean 生命周期等。

## 第五章：Spring IoC依赖查找（Dependency Lookup） (9讲)

42 | 依赖查找的今世前生：Spring IoC容器从Java标准中学到了什么？


### 43 | 单一类型依赖查找：如何查找已知名称或类型的Bean对象？
单一类型依赖查找接口 - BeanFactory
* 根据 Bean 名称查找
  * getBean(String)
  * Spring 2.5 覆盖默认参数：getBean(String,Object...)
* 根据 Bean 类型查找
  * Bean 实时查找
     * Spring 3.0 getBean(Class)
     * Spring 4.1 覆盖默认参数：getBean(Class,Object...)
  * Spring 5.1 Bean 延迟查找
    * getBeanProvider(Class)
    * getBeanProvider(ResolvableType)
* 根据 Bean 名称 + 类型查找：getBean(String,Class)

### 44 | 集合类型依赖查找：如何查找已知类型多个Bean集合？
集合类型依赖查找接口 - ListableBeanFactory
* 根据 Bean 类型查找
  * 获取同类型 Bean 名称列表
    * getBeanNamesForType(Class)
    * Spring 4.2 getBeanNamesForType(ResolvableType)
  * 获取同类型 Bean 实例列表
    * getBeansOfType(Class) 以及重载方法
* 通过注解类型查找
  * Spring 3.0 获取标注类型 Bean 名称列表
    * getBeanNamesForAnnotation(Class<? extends Annotation>)
  * Spring 3.0 获取标注类型 Bean 实例列表
    * getBeansWithAnnotation(Class<? extends Annotation>)
  * Spring 3.0 获取指定名称 + 标注类型 Bean 实例
    * findAnnotationOnBean(String,Class<? extends Annotation>)
  
@Configuration 是非必须注解
    
就是Bean的定义默认情况是可以覆盖的，之前定义的bean，后面用相同名称可以同时覆盖掉。

我们通过命名接口可以学习到一些什么事情：就当你去表达单和复杂的时候，我们通常来说可以通过继承，那么你去得到我的复杂或者
复合类型的时候，首先继承我们单一的接口，同时做一些扩展。

BeanDefinition其实是在Bean定义的注册阶段。

ListableBeanFactory,它是针对于某一个类型去查找一个集合列表,那么集合列表可能有两种情况,一种情况是查询Bean的名称，
一种情况是查询Bean的实例。我们推荐你使用Bean的名称去判断这个Bean是否存在，当然重要的方式是判断BeanDefinition是否存在，这种方式会避免提早初始化你的Bean，
产生一些不确定的因素。Why？


### 45 | 层次性依赖查找：依赖查找也有双亲委派？
层次性依赖查找接口 - HierarchicalBeanFactory
* 双亲 BeanFactory：getParentBeanFactory()
* 层次性查找
  * 根据 Bean 名称查找
    * 基于 containsLocalBean 方法实现
  * 根据 Bean 类型查找实例列表
    * 单一类型：BeanFactoryUtils#beanOfType
    * 集合类型：BeanFactoryUtils#beansOfTypeIncludingAncestors
  * 根据 Java 注解查找名称列表
    * BeanFactoryUtils#beanNamesForTypeIncludingAncestors



ClassLoader里面的双亲委派非常相似：推到直接能够找到我的根的一个对象为止


### 46 | 延迟依赖查找：非延迟初始化Bean也能实现延迟查找？

Bean 延迟依赖查找接口
* org.springframework.beans.factory.ObjectFactory
* org.springframework.beans.factory.ObjectProvider
  * Spring 5 对 Java 8 特性扩展
    * 函数式接口
      * getIfAvailable(Supplier)
      * ifAvailable(Consumer)
    * Stream 扩展 - stream()

### 47 | 安全依赖查找

* 依赖查找安全性对比
|依赖查找类型| 代表实现 |是否安全|
|:-:|:-:|:-:|
|单一类型查找 |BeanFactory#getBean|否|
||ObjectFactory#getObject|否|
||ObjectProvider#getIfAvailable|是|
|集合类型查找 |ListableBeanFactory#getBeansOfType|是|
||ObjectProvider#stream |是|

注意：层次性依赖查找的安全性取决于其扩展的单一或集合类型的 BeanFactory 接口（继承了多个接口）

如果你想用延迟加载的话，我建议大家用ObjectProvider，Spring Cloud源码大量使用，既可以表示单一类型，有可以表示复合类型或者集合类型。

DefaultListableBeanFactory implements ConfigurableListableBeanFactory ：既是单一类型又是集合类型和层次类型，兜底实现。

### 48 | 内建可查找的依赖：哪些Spring IoC容器内建依赖可供查找？
* AbstractApplicationContext 内建可查找的依赖（基类）
|Bean 名称| Bean 实例 |使用场景|
|:-:|:-:|:-:|
|environment| Environment 对象| 外部化配置以及 Profiles|
|systemProperties |java.util.Properties 对象 |Java 系统属性|
|systemEnvironment |java.util.Map 对象| 操作系统环境变量|
|messageSource |MessageSource 对象| 国际化文案|
|lifecycleProcessor |LifecycleProcessor 对象| Lifecycle Bean 处理器|
|applicationEventMulticaster |ApplicationEventMulticaster 对象|Spring 事件广播器|

environment：外部化配置属性主要是指的我们比如说像-D参数

systemProperties：当我们去获取比如说系统的一些路径的时候

* 注解驱动 Spring 应用上下文内建可查找的依赖（部分）
|Bean 名称| Bean 实例 |使用场景|
|:-:|:-:|:-:|
|org.springframework.context.annotation.internalConfigurationAnnotationProcessor|ConfigurationClassPostProcessor 对象|处理 Spring 配置类|
|org.springframework.context.annotation.internalAutowiredAnnotationProcessor|AutowiredAnnotationBeanPostProcessor 对象 |处理 @Autowired 以及 @Value注解|
|org.springframework.context.annotation.internalCommonAnnotationProcessor|CommonAnnotationBeanPostProcessor 对象|条件激活）处理 JSR-250 注解，如 @PostConstruct 等|
|org.springframework.context.event.internalEventListenerProcessor|EventListenerMethodProcessor对象|处理标注 @EventListener 的Spring 事件监听方法|
|org.springframework.context.event.internalEventListenerFactory|DefaultEventListenerFactory 对象|@EventListener 事件监听方法适配为 ApplicationListener|
|org.springframework.context.annotation.internalPersistenceAnnotationProcessor|PersistenceAnnotationBeanPostProcessor 对象|（条件激活）处理 JPA 注解场景|

ConfigurationClassPostProcessor：Bean的后置处理，是在BeanFactory在生命周期里面去做的，它是处理Spring配置类的一个很核心的要素。
ConfigurationClassPostProcessor implements BeanDefinitionRegistryPostProcessor

依赖注入其实包含两个层次意思：它注人的对象也许是一个Spring Bean，还有的有可能是一个可依赖的对象，再者它可能是一个外部化配置。
像@value就是外部化配置属性的一个注入

AnnotationConfigUtils


### 49 | 依赖查找中的经典异常：Bean找不到？Bean不是唯一的？Bean创建失败？

* BeansException 子类型
|异常类型 |触发条件（举例） |场景举例|
|:-:|:-:|:-:|
|NoSuchBeanDefinitionException |当查找 Bean 不存在于 IoC 容器时 |BeanFactory#getBean ObjectFactory#getObject|
|NoUniqueBeanDefinitionException|类型依赖查找时，IoC 容器存在多个 Bean 实例|BeanFactory#getBean(Class)|
|BeanInstantiationException| 当 Bean 所对应的类型非具体类时|  BeanFactory#getBean|
|BeanCreationException | 当 Bean 初始化过程中 | Bean 初始化方法执行异常时|
|BeanDefinitionStoreException|  当 BeanDefinition 配置元信息非法时| XML 配置资源无法打开时|


### 50 | 面试题精选

* 沙雕面试题 - ObjectFactory 与 BeanFactory 的区别？

答：ObjectFactory 与 BeanFactory 均提供依赖查找的能力。不过 ObjectFactory 仅关注一个或一种类型的 Bean 依赖查找，并且自身不具备依赖查找的能力，能力则由 BeanFactory 输出。BeanFactory 则提供了单一类型、集合类型以及层次性等多种依赖找方式。

* 996 面试题 - BeanFactory.getBean 操作是否线程安全？

答：BeanFactory.getBean 方法的执行是线程安全的，超过过程中会增加互斥锁

* 劝退面试题 - Spring 依赖查找与注入在来源上的区别?

答：答案将《Spring IoC依赖注入》以及《Spring IoC依赖来源》章节中继续讨论。

## 第六章：Spring IoC依赖注入（Dependency Injection） (20讲)


### 51 | 依赖注入的模式和类型：Spring提供了哪些依赖注入的模式和类型？

依赖注入的模式
* 手动模式 - 配置或者编程的方式，提前安排注入规则
  * XML 资源配置元信息
  * Java 注解配置元信息
  * API 配置元信息
* 自动模式 - 实现方提供依赖自动关联的方式，按照內建的注入规则
  * Autowiring（自动绑定）

*依赖注入类型
|依赖注入类型| 配置元数据举例|
|:-:|:-:|
|Setter 方法| <proeprty name="user" ref="userBean"/>|
|构造器| <constructor-arg name="user" ref="userBean" />|
|字段| @Autowired User user;|
|方法| @Autowired public void user(User user) { ... }|
|接口回调| class MyBean implements BeanFactoryAware { ... }|

### 52 | 自动绑定（Autowiring）：为什么Spring会引入Autowiring？

The Spring container can autowire relationships between collaborating beans. You can let Spring
resolve collaborators (other beans) automatically for your bean by inspecting the contents of the
ApplicationContext.

优点：
* 自动装配可以显著减少指定属性或构造函数参数的需要。
* 传值引用


### 53 | 自动绑定（Autowiring）模式：各种自动绑定模式的使用场景是什么？

* Autowiring modes

|模式 |说明|
|:-:|:-:|
|no |默认值，未激活 Autowiring，需要手动指定依赖注入对象。|
|byName| 根据被注入属性的名称作为 Bean 名称进行依赖查找，并将对象设置到该属性。|
|byType| 根据被注入属性的类型作为依赖类型进行查找，并将对象设置到该属性。|
|constructor| 特殊 byType 类型，用于构造器参数。|

byType：如果出现多个类型相同的Bean，一种解法就把其他的不需要的Bean给干掉；第二种方式把某个Bean设置为primary这种方式。

### 54 | 自动绑定（Autowiring）限制和不足：如何理解和挖掘官方文档中深层次的含义？

* 精确依赖项property和constructor-arg设置始终会覆盖Autowiring
* 不能绑定简单类型和原生类型（绑定bean和对象，可以通过@Value方式绑定）
* 容器内的多个bean定义，绑定不够精确
55 | Setter方法依赖注入：Setter注入的原理是什么？

56 | 构造器依赖注入：官方为什么推荐使用构造器注入？

57 | 字段注入：为什么Spring官方文档没有单独列举这种注入方式？

58 | 方法注入：方法注入是@Autowired专利吗？

59 | 接口回调注入：回调注入的使用场景和限制有哪些？

60 | 依赖注入类型选择：各种依赖注入有什么样的使用场景？

61 | 基础类型注入：String和Java原生类型也能注入Bean的属性，它们算依赖注入吗？

62 | 集合类型注入：注入Collection和Map类型的依赖区别？还支持哪些集合类型？

63 | 限定注入：如何限定Bean名称注入？如何实现Bean逻辑分组注入？

64 | 延迟依赖注入：如何实现延迟执行依赖注入？与延迟依赖查找是类似的吗？

65 | 依赖处理过程：依赖处理时会发生什么？其中与依赖查找的差异在哪？

66 | @Autowired注入：@Autowired注入的规则和原理有哪些？

67 | JSR-330 @Inject注入：@Inject与@Autowired的注入原理有怎样的联系？

68 | Java通用注解注入原理：Spring是如何实现@Resource和@EJB等注解注入的？

69 | 自定义依赖注入注解：如何最简化实现自定义依赖注入注解？

70 | 面试题精选

## 第七章：Spring IoC依赖来源（Dependency Sources） (8讲)

71 | 依赖查找的来源：除容器内建和自定义Spring Bean之外，还有其他来源提供依赖查找吗？

72 | 依赖注入的来源：难道依赖注入的来源与依赖查找的不同吗？

73 | Spring容器管理和游离对象：为什么会有管理对象和游离对象？

74 | Spring Bean Definition作为依赖来源：Spring Bean的来源

75 | 单例对象作为依赖来源：单体对象与普通Spring Bean存在哪些差异？

76 | 非Spring容器管理对象作为依赖来源：如何理解ResolvableDependency？

77 | 外部化配置作为依赖来源：@Value是如何将外部化配置注入Spring Bean的？

78 | 面试题精选

## 第八章：Spring Bean作用域（Scopes） (9讲)

79 | Spring Bean作用域：为什么Spring Bean需要多种作用域？

80 | "singleton" Bean作用域：单例Bean在当前Spring应用真是唯一的吗？

不是

81 | "prototype" Bean作用域：原型Bean在哪些场景下会创建新的实例？

82 | "request" Bean作用域：request Bean会在每次HTTP请求创建新的实例吗？

83 | "session" Bean作用域：session Bean在Spring MVC场景下存在哪些局限性？

84 | "application" Bean作用域：application Bean是否真的有必要？

没太大必要

85 | 自定义Bean作用域：设计Bean作用域应该注意哪些原则？

86 | 课外资料：Spring Cloud RefreshScope是如何控制Bean的动态刷新？

87 | 面试题精选

## 第九章：Spring Bean生命周期（Bean Lifecycle） (18讲)

88 | Spring Bean 元信息配置阶段：BeanDefinition配置与扩展

89 | Spring Bean 元信息解析阶段：BeanDefinition的解析

90 | Spring Bean 注册阶段：BeanDefinition与单体Bean注册

91 | Spring BeanDefinition合并阶段：BeanDefinition合并过程是怎样出现的？

92 | Spring Bean Class加载阶段：Bean ClassLoader能够被替换吗?

93 | Spring Bean实例化前阶段：Bean的实例化能否被绕开？

94 | Spring Bean实例化阶段：Bean实例是通过Java反射创建吗？

95 | Spring Bean实例化后阶段：Bean实例化后是否一定被是使用吗？

96 | Spring Bean属性赋值前阶段：配置后的PropertyValues还有机会修改吗？

有

```java
public abstract class InstantiationAwareBeanPostProcessorAdapter implements SmartInstantiationAwareBeanPostProcessor {
    public PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName) throws BeansException {
        return null;
    }
}
```

97 | Aware接口回调阶段：众多Aware接口回调的顺序是安排的？

98 | Spring Bean初始化前阶段：BeanPostProcessor

99 | Spring Bean初始化阶段：@PostConstruct、InitializingBean以及自定义方法

100 | Spring Bean初始化后阶段：BeanPostProcessor

101 | Spring Bean初始化完成阶段：SmartInitializingSingleton

102 | Spring Bean销毁前阶段：DestructionAwareBeanPostProcessor用在怎样的场景?

103 | Spring Bean销毁阶段：@PreDestroy、DisposableBean以及自定义方法

104 | Spring Bean垃圾收集（GC）：何时需要GC Spring Bean？

105 | 面试题精选

## 第十章：Spring配置元信息（Configuration Metadata） (17讲)

106 | Spring配置元信息：Spring存在哪些配置元信息？它们分别用在什么场景？

107 | Spring Bean配置元信息：BeanDefinition

108 | Spring Bean属性元信息：PropertyValues

109 | Spring容器配置元信息

110 | 基于XML资源装载Spring Bean配置元信息

111 | 基于Properties资源装载Spring Bean配置元信息：为什么Spring官方不推荐？

112 | 基于Java注解装载Spring Bean配置元信息

113 | Spring Bean配置元信息底层实现之XML资源

114 | Spring Bean配置元信息底层实现之Properties资源

115 | Spring Bean配置元信息底层实现之Java注解

116 | 基于XML资源装载Spring IoC容器配置元信息

117 | 基于Java注解装载Spring IoC容器配置元信息

118 | 基于Extensible XML authoring 扩展Spring XML元素

119 | Extensible XML authoring扩展原理

120 | 基于Properties资源装载外部化配置

121 | 基于Yaml资源装载外部化配置

122 | 面试题

第十一章：Spring资源管理（Resources） (11讲)

123 | 引入动机：为什么Spring不使用Java标准资源管理，而选择重新发明轮子？

124 | Java标准资源管理：Java URL资源管理存在哪些潜规则？

125 | Spring资源接口：Resource接口有哪些语义？它是否“借鉴”了SUN的实现呢？

126 | Spring内建Resource实现：Spring框架提供了多少种内建的Resource实现呢？

127 | Spring Resource接口扩展：Resource能否支持写入以及字符集编码？

128 | Spring资源加载器：为什么说Spring应用上下文也是一种Spring资源加载器？

129 | Spring通配路径资源加载器：如何理解路径通配Ant模式？

130 | Spring通配路径模式扩展：如何扩展路径匹配的规则？

131 | 依赖注入Spring Resource：如何在XML和Java注解场景注入Resource对象？

132 | 依赖注入ResourceLoader：除了ResourceLoaderAware回调注入，还有哪些注入方法？

133 | 面试题精选

## 第十二章：Spring国际化（i18n） (5讲)

134 | Spring国际化使用场景

135 | Spring国际化接口：MessageSource不是技术的创造者，只是技术的搬运工？

136 | 层次性MessageSource：双亲委派不是ClassLoader的专利吗？

137 | Java国际化标准实现：ResourceBundle潜规则多？

138 | Java文本格式化：MessageFormat脱离Spring场景，能力更强大？