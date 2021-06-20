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

#### 1.特性

按需分配

胶水：API和或者规范整合在一起

#### 2.使用API

Spring 3 对Java 5 的支持（注解）

Spring 5 对Java 8 的支持

Java: XML、反射、动态代理

JavaEE: Servlet、Jsp、Jpa、Jms

#### 3.自己的实现

* 面向对象（OOP）：多态，接口对应语义
* 切面编程：jdk动态代理（局限性）、ASM、CGLIB、AspectJ 类的提升
* 面向元编程
 * 配置元信息包含三种
 * 配置类：配置属性在XML或者.properties文件，会影响运行时的一些状态，比如影响依赖注入的方式
 * 注解
 * 属性配置：占位符、外部化配置
   * 不是面向程序来编程，在程序的基础上在进行元数据的一些处理
* 面向模块编程 
* 面向函数编程 



### 03 | 课前准备：学习三件套（工具、代码与大脑）

方法

基础:夯实基础,了解动态
思考:保持怀疑,验证一切
分析:不拘小节,观其大意
实践:思辨结合,学以致用

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
  * 类似序列号和反序列化

# 必考 事务抽象


3.Web技术(Web)

* Web Servlet技术栈
  * Spring MVC
  * WebSocket
  * SockJS
* Web Reactive技术栈（Spring 5 ）注解一样，底层实现不一样
  * Spring WebFlux
  * WebClient
  * WebSocket

当然Reactive它也是可以运用Spring MVC的，也可以运用到Servlet引擎来进行实现。

在Spring框架5.0之前，有另外一个东西叫做RestTemplate，或者是有个叫做HttpClient，是这个同步的Http执行的客户端。那么WebClient引用之后，它把过去的同步执行变成异步回调的方式。



4.技术整合(Integration)

* 远程调用(Remoting)
  * 一般是同步
* Java 消息服务 (JMS)
  * 异步
* Java连接架构( JCA)
* Java 管理扩展(JMX)
  * CPU磁盘利用率（运维）
* Java 邮件客户端 (Email)
* 本地任务(Tasks)
  * 单机版
* 本地调度(Scheduling)
* 缓存抽象(Caching)
  * 注解
* Spring测试(Testing)

通常来说远程调用是采用的同步的模式。

JMX 运维侧，查看CUP、磁盘利用率等。



5.测试(Testing)

* 模拟对象(Mock Objects)
  * 单元测试
* TestContext 框架(TestContext Framework)
  * 集成测试
* Spring MVC测试(Spring MVC Test)
  * 服务端
* Web 测试客户端(WebTestClient)



Mock对象我们可以去动态的去生成它，比如说在Spring Framework里面，它生成的这么一个MockHttp这么一个接口。



### 05 | Spring版本特性：Spring各个版本引入了哪些新特性？

####Java版本依赖与支持

|Spring Framework版本|Java标准版|Java企业版|
|:-:|:-:|:-:|
|1.x|1.3+（动态代理）|J2EE 1.3 +|
|2.x|1.4.2+（NIO）|J2EE 1.3 +|
|3.x （注解 事件）|5+(注解)|J2EE 1.4和Java EE 5|
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
  * 重点
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

JAXB 2.0：Java API for XML Binding,Java API去绑定XML的实现,里面就会有个marshal、unmarshal的操作。

SpringBoot 注解的使用需求出现了急剧性的膨胀，注解的实现就来自于两个方面：ASM、标准的Java反射，都是运行时实现。

通过编译时来进行实现@Indexed：Component的基础上面，编译时把API去做一个相当于说建立索引，能够帮助我快速的定位到底哪个类建了Component索引，那么这时候我就可以定位到类而不需要逐一扫描。

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

* 面向对象编程
  * 契约接口：Aware、BeanPostProcessor ...
  * 设计模式：观察者模式、组合模式、模板模式 ...
  * 对象继承：Abstract* 类

* 面向切面编程
  * 动态代理：JdkDynamicAopProxy
  * 字节码提升：ASM、CGLib、AspectJ...

* 面向元编程
  * 注解：模式注解（@Component、@Service、@Respository ...）
  * 配置：Environment 抽象、PropertySources、BeanDefinition ...
  * 泛型：GenericTypeResolver、ResolvableType ...

* 函数驱动
  * 函数接口：ApplicationEventPublisher
  * Reactive：Spring WebFlux

* 模块驱动
  * Maven Artifacts
  * OSGI Bundles
  * Java 9 Automatic Modules
  * Spring @Enable*

### 11 | Spring核心价值：我们能从Spring Framework中学到哪些经验和教训呢？

1. 编程模型
* 面向对象主要是以接口为主，面向对象主要是以LP拦截为主；
* 面向元数据主要是一些元信息的一个封装，注解、配置、元数据的调整；



### 12 | 面试题精选

* 沙雕面试题 - 什么是 Spring Framework？

答:
Spring使得创建Java企业应用变得很容易。它在Java语言上面上，提供了拥抱企业环境中所需的一切，支持Groovy和Kotlin作为JVM上的可选语言，并与创建多种架构的灵活性取决于应用程序的需求。

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

在软件工程中，控制反转(IoC)是一种编程原理。IoC反转控制与传统控制流相比（串行）。在IoC中，计算机程序的自定义编写部分从通用框架接收控制流。采用这种设计的软件体系结构颠倒了控制。与传统程序设计的比较：在传统程序设计中，习惯表达程序目的的代码调用可重用库来处理泛型任务，但在控制反转中，是框架调用定制的或特定于任务的代码。

### 14 | IoC主要实现策略：面试官总问IoC和DI的区别，他真的理解吗？

在面向对象编程中，有几种基本的技术来实现控制反转。这些是:

* 使用服务定位器模式
* 使用依赖注入，例如
   * 构造函数注入
   * 参数注入
   * Setter注入
   * 接口注入
     * 它通常是由容器帮我们自动去注入一些事情。
* 使用上下文查找
* 使用模板法设计模式
   * 比如说是Spring JDBC里面会用到,JDBC Template这样的实现,会给我们一种类似于比如说Statement,这样的Callback这种Callback能够帮助我们实现地更为抽象,当我们去实现这样的接口的时候,我们不需要关心Callback从哪来,那么也实现了一种反转控制的方式
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



### 16 | 除了Spring，还有其它的IOC容器实现吗？

#### 主要实现

* Java SE
  * Java Beans
  * Java ServiceLoader SPI
  * JNDI（Java Naming and Directory Interface） 
* Java EE
  * EJB（Enterprise Java Beans）
  * Servlet 
* 开源
  * Apache Avalon（http://avalon.apache.org/closed.html） 
  * PicoContainer（http://picocontainer.com/） 
  * Google Guice（https://github.com/google/guice） 
  * Spring Framework（https://spring.io/projects/spring-framework）


Servlet容器：Model2的设计模式，通过JavaEE或者是通过我们的Servlet去获取比如说像数据库源或者是比如说像线程池或者是消息服务，那么也是通过JNDI的方式在我的Servlet容器或者EJB容器或者Java EE容器里面来进行获取。

### 17 | 传统IoC容器实现：JavaBeans也是IoC容器吗？

#### Java Beans 作为 IoC 容器

* 特性
  * 依赖查找
  * 生命周期管理
  * 配置元信息
  * 事件
  * 自定义
  * 资源管理
  * 持久化
* 规范
  * JavaBeans
  * BeanContext

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

此外,constructor-injected组件始终以完全初始化状态返回给客户机(调用)代码。大量的构造函数参数是一种糟糕的体验，意味着类可能有太多的责任，应该重构更好地解决问题的适当分离。

Setter注入应该主要用于可选的依赖项，这些依赖项可以被分配合理的默认值在类。否则，必须在代码使用依赖项的任何地方执行非空检查。顺序无法确定。

有个类叫ObjectProvider这个类，它是种类型安全的方式，如果你的依赖注入的方式或者依赖查找的方式，是一个单一类型的话，它会调用getIfAvailable的方法来进行示范性地去返回那么等于空的时候它就会返回空,这种方式在Spring Boot的场景经常用到。




### 20 | 构造器注入 VS. Setter 注入：为什么Spring官方文档的解读会与作者的初心出现偏差？

### 21 | 面试题精选

* 沙雕面试题 - 什么是 IoC ？

答：简单地说，IoC 是反转控制，类似于好莱坞原则，主要有依赖查找和依赖注入实现。

按照IoC的定义，很多方面都是IoC，比如说JavaBeans是IoC的一个容器实现，Servlet的容器也是IoC的实现，因为Servlet可以去依赖或者反向地通过JNDI的方式进行得到一些外部的一些资源，包括DataSource或者相关的EJB的组件。像是Spring Framework依赖注入的框架，也能够帮助我们去实现我们的IoC。

如果是反转控制，那就包括我们说消息，因为消息其实是被动的，我们如果说我们传统的调用链路是一个主动拉的模式，那么IoC其实是一种推的模式那么推的模式在消息事件以及各种这样类似于这种反向的观察者模式的扩展都属于IoC。

* 996 面试题 - 依赖查找和依赖注入的区别？

答：依赖查找是主动或手动的依赖查找方式，通常需要依赖容器或标准 API实现。而依赖注入则是手动或自动依赖绑定的方式，无需依赖特定的容器和API。

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

#### 官网解释

BeanFactory接口提供了一种高级配置机制，能够管理任何类型的对象。ApplicationContext是BeanFactory的一个子接口。
* 更容易与Spring的AOP特性集成
* 消息资源处理(用于国际化)
* 事件发布
* 应用程序层特定的上下文，如用于web应用程序的WebApplicationContext。

简而言之，BeanFactory提供了配置框架和基本功能，ApplicationContext提供更多企业级功能。ApplicationContext是BeanFactory的一个完整超集。也就是说BeanFactory含有的能力，ApplicationContext全都有，并且提供以上4点更多的特性。

BeanFactory是一个底层的IoC容器,ApplicationContext组合了BeanFactory的实现，在这基础上面增加了一些它的特性。


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

#### 启动

第一个操作是创建我们的BeanFactory，并且进行初步的初始化，加入些我们的内建的一些Bean对象或者Bean依赖，以及加上一些内建的非Bean的依赖。
第二部分就是关于BeanFactory的扩展点，通过执行BeanFactoryPostProcessor。
第三个是对Bean的一些修改或者扩展，通过执行这个BeanPostProcessor来进行操作，这个操作这里只是注册，具体的调用是在BeanFactory里面进行操作的。
再接下来就会定义我们说的国际化事件等

#### 运行

#### 停止


### 30 | 面试题精选

* 沙雕面试题 - 什么是 Spring IoC 容器？

Spring框架实现的控制反转(IoC)原则。IoC也称为依赖注入(DI)。DI是IOC的一种实现方式，还有依赖查找，看通过构造函数参数，属性的setter方式来注入一些其他的对象，来完成依赖注入。

* 996 面试题 - BeanFactory 与 FactoryBean？

BeanFactory 是 IoC 底层容器。

FactoryBean 是 创建 Bean 的一种方式，帮助实现复杂的初始化逻辑。


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

#### BeanDefinition 元信息
|属性（Property） |说明|
|:-:|:-:|
|Class |Bean 全类名，必须是具体类，不能用抽象类或接口|
|Name |Bean 的名称或者 ID|
|Scope |Bean 的作用域（如：singleton、prototype 等）|
|Constructor arguments|Bean 构造器参数（用于依赖注入）|
|Properties |Bean 属性设置（用于依赖注入）|
|Autowiring mode |Bean 自动绑定模式（如：通过名称 byName）|
|Lazy initialization mode| Bean 延迟初始化模式（延迟和非延迟）|
|Initialization method |Bean 初始化回调方法名称|
|Destruction method |Bean 销毁回调方法名称|

* BeanDefinition 构建
  * 通过 BeanDefinitionBuilder
  * 通过 AbstractBeanDefinition 以及派生类

### 33 | 命名Spring Bean：id和name属性命名Bean，哪个更好？

* 自动生成
* 自己定义

#### 命名 Spring Bean

* Bean 名称生成器（BeanNameGenerator） 
* 由 Spring Framework 2.0.3 引入，框架內建两种实现：
  * DefaultBeanNameGenerator：默认通用 BeanNameGenerator 实现
* AnnotationBeanNameGenerator：基于注解扫描的 BeanNameGenerator 实现，起始于Spring Framework 2.5

### 34 | Spring Bean的别名：为什么命名Bean还需要别名？

到了第三方的一个jar包或者是相关的依赖资源，可以通过新的名称来进行更场景化的一个依赖。

### 35 | 注册Spring Bean：如何将BeanDefinition注册到IoC容器？

BeanDefinition 注册
* XML 配置元信息
  * <bean name=”...” ... />
* Java 注解配置元信息（不会重复注册）
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

### 42 | 依赖查找的今世前生：Spring IoC容器从Java标准中学到了什么？


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

我们通过命名接口可以学习到一些什么事情：就当你去表达单和复杂的时候，我们通常来说可以通过继承，那么你去得到我的复杂或者复合类型的时候，首先继承我们单一的接口，同时做一些扩展。

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

* 依赖查找安全性对比（找不到bean会不会报错）

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

答：ObjectFactory 与 BeanFactory 均提供依赖查找的能力。不过 ObjectFactory 仅关注一个或一种类型的 Bean 依赖查找，并且自身不具备依赖查找的能力，能力则由 BeanFactory 输出。BeanFactory 则提供了单一类型、集合类型以及层次性等多种依赖查找方式。

* 996 面试题 - BeanFactory.getBean 操作是否线程安全？

答：BeanFactory.getBean 方法的执行是线程安全的，操作过程中会增加互斥锁

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

#### 依赖注入类型
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

### 55 | Setter方法依赖注入：Setter注入的原理是什么？
实现方法
* 手动模式
  * XML 资源配置元信息
  * Java 注解配置元信息
  * API 配置元信息
* 自动模式
  * byName
  * byType

缺点：顺序不确定

### 56 | 构造器依赖注入：官方为什么推荐使用构造器注入？
实现方法
* 手动模式
  * XML 资源配置元信息
  * Java 注解配置元信息
  * API 配置元信息
* 自动模式
  * constructor

### 57 | 字段注入：为什么Spring官方文档没有单独列举这种注入方式？

实现方法
* 手动模式
  * Java 注解配置元信息
  * @Autowired
  * @Resource
  * @Inject（可选）
  
@Autowired 会忽略掉静态字段

### 58 | 方法注入：方法注入是@Autowired专利吗？
* 实现方法
  * 手动模式
  * Java 注解配置元信息
  * @Autowired
  * @Resource
  * @Inject（可选）
  * @Bean


### 59 | 接口回调注入：回调注入的使用场景和限制有哪些？

### 60 | 依赖注入类型选择：各种依赖注入有什么样的使用场景？
注入选型
* 低依赖：构造器注入
* 多依赖：Setter 方法注入
  * 先后顺序无法确定
* 便利性：字段注入 （无论在Spring或者Spring Boot里面，它慢慢处于淘汰状态）
* 声明类：方法注入

### 61 | 基础类型注入：String和Java原生类型也能注入Bean的属性，它们算依赖注入吗？
基础类型
* 原生类型（Primitive）：boolean、byte、char、short、int、float、long、double
* 标量类型（Scalar）：Number、Character、Boolean、Enum、Locale、Charset、Currency、Properties、UUID
* 常规类型（General）：Object、String、TimeZone、Calendar、Optional 等
* Spring 类型：Resource、InputSource、Formatter 等

### 62 | 集合类型注入：注入Collection和Map类型的依赖区别？还支持哪些集合类型？
集合类型
* 数组类型（Array）：原生类型、标量类型、常规类型、Spring 类型
* 集合类型（Collection）
* Collection：List、Set（SortedSet、NavigableSet、EnumSet）
* Map：Properties

### 63 | 限定注入：如何限定Bean名称注入？如何实现Bean逻辑分组注入？

* 使用注解 @Qualifier 限定
  * 通过 Bean 名称限定
  * 通过分组限定
* 基于注解 @Qualifier 扩展限定
  * 自定义注解 - 如 Spring Cloud @LoadBalanced （分组）

### 64 | 延迟依赖注入：如何实现延迟执行依赖注入？与延迟依赖查找是类似的吗？

* 使用 API ObjectFactory 延迟注入
  * 单一类型
  * 集合类型
* 使用 API ObjectProvider 延迟注入（推荐）
  * 单一类型
  * 集合类型
  
来进行注入一些非必要性的依赖，这种方式可以避免些关于NoSuchBeanException相关的一个错误。

### 65 | 依赖处理过程：依赖处理时会发生什么？其中与依赖查找的差异在哪？

基础知识
* 入口 - DefaultListableBeanFactory#resolveDependency
* 依赖描述符 - DependencyDescriptor
  * required 是否必须的
  * eager 实时注入，和 lazy 相反 
  * fieldName 字段名称
  * containingClass 包含类型
* 自定绑定候选对象处理器 - AutowireCandidateResolver

先定义然后先注册然后先初始化;

在注入过程中我们把这个对象的依赖来进行解析,然后再把它插入或者说通过反射的方式来调入;

### 66 | @Autowired注入：@Autowired注入的规则和原理有哪些？

@Autowired 注入规则
* 非静态字段
* 非静态方法
* 构造器

//前个阶段叫构建元数据
AutowiredAnnotationBeanPostProcessor#postProcessMergedBeanDefinition
//后个阶段来进行注入(这个注入过程又出现了依赖处理的过程)
AutowiredAnnotationBeanPostProcessor#postProcessProperties

注入在postProcessProperties方法执行，早于setter注入， 也早于@PostConstruct


### 67 | JSR-330 @Inject注入：@Inject与@Autowired的注入原理有怎样的联系？

@Inject 注入过程
* 如果 JSR-330 存在于 ClassPath 中，复用 AutowiredAnnotationBeanPostProcessor 实现

### 68 | Java通用注解注入原理：Spring是如何实现@Resource和@EJB等注解注入的？
CommonAnnotationBeanPostProcessor
* 注入注解
  * javax.xml.ws.WebServiceRef
  * javax.ejb.EJB
  * javax.annotation.Resource
* 生命周期注解
  * javax.annotation.PostConstruct
  * javax.annotation.PreDestroy

### 69 | 自定义依赖注入注解：如何最简化实现自定义依赖注入注解？

基于 AutowiredAnnotationBeanPostProcessor 实现
* 自定义实现
  * 生命周期处理
  * InstantiationAwareBeanPostProcessor
  * MergedBeanDefinitionPostProcessor
* 元数据
  * InjectedElement
  * InjectionMetadata

如果你非常需要你的Bean提前初始化或提前注册的时候，这时候你可以选择性地把它标成static（脱离的限制）。

### 70 | 面试题精选

* 沙雕面试题 - 有多少种依赖注入的方式？
答：构造器注入(少依赖，强制性依赖)
Setter 注入（多依赖，非强制性依赖）
字段注入（使用便利）
方法注入
接口回调注入

* 996 面试题 - 你偏好构造器注入还是 Setter 注入？
答：两种依赖注入的方式均可使用，如果是必须依赖的话，那么推荐使用构造器注入（参数比较少），Setter 注入用于可选依赖。

原始构造器参数构造来进行操作：那么不但可以帮助我们解决我们的必须依赖问题，那么不但可以帮助我们解决我们的必须依赖问题。

* 劝退面试题 - Spring 依赖注入的来源有哪些？
答：答案将《Spring IoC依赖来源》章节中继续讨论。

## 第七章：Spring IoC依赖来源（Dependency Sources） (8讲)

### 71 | 依赖查找的来源：除容器内建和自定义Spring Bean之外，还有其他来源提供依赖查找吗？

底层全部都是BeanDefinition，BeanDefinition是最终Bean用于解析的。


查找来源
|来源| 配置元数据|
|:-:|:-:|
|Spring BeanDefinition| <bean id="user" class="org.geekbang...User">|
||@Bean public User user(){...}|
||BeanDefinitionBuilder|
|单例对象| API 实现|

### 72 | 依赖注入的来源：难道依赖注入的来源与依赖查找的不同吗？

注入来源
|来源| 配置元数据|
|:-:|:-:|
|Spring BeanDefinition| <bean id="user" class="org.geekbang...User">|
||@Bean public User user(){...}|
||BeanDefinitionBuilder|
|单例对象| API 实现|
|非 Spring 容器管理对象||

```java
    // ResolvableDependency这个依赖，不能用于getBean，非Spring管理对象，只能用于依赖注入
    beanFactory.registerResolvableDependency(BeanFactory.class, beanFactory);
    beanFactory.registerResolvableDependency(ResourceLoader.class, this);
    beanFactory.registerResolvableDependency(ApplicationEventPublisher.class, this);
    beanFactory.registerResolvableDependency(ApplicationContext.class, this);
```


### 73 | Spring容器管理和游离对象：为什么会有管理对象和游离对象？

依赖对象
|来源 |Spring Bean 对象| 生命周期管理 |配置元信息 |使用场景|
|:-:|:-:|:-:|:-:|:-:|
|Spring BeanDefinition |是 |是| 有 |依赖查找、依赖注入|
|单体对象 |是 |否 |无| 依赖查找、依赖注入|
|Resolvable Dependency |否| 否| 无 |依赖注入|

### 74 | Spring Bean Definition作为依赖来源：Spring Bean的来源
要素
* 元数据：BeanDefinition
* 注册：BeanDefinitionRegistry#registerBeanDefinition
* 类型：延迟和非延迟
* 顺序：Bean 生命周期顺序按照注册顺序

### 75 | 单例对象作为依赖来源：单体对象与普通Spring Bean存在哪些差异？

* 要素
  * 来源：外部普通 Java 对象（不一定是 POJO）
  * 注册：SingletonBeanRegistry#registerSingleton
* 限制
  * 无生命周期管理
  * 无法实现延迟初始化 Bean

它的生命周期不由Spring,上下文来进行托管,他没有办法实现所谓的延迟初始化,之后会有一个生命周期的管理。

### 76 | 非Spring容器管理对象作为依赖来源：如何理解ResolvableDependency？
* 要素
  * 注册：ConfigurableListableBeanFactory#registerResolvableDependency
* 限制
  * 无生命周期管理
  * 无法实现延迟初始化 Bean
  * 无法通过依赖查找
  
### 77 | 外部化配置作为依赖来源：@Value是如何将外部化配置注入Spring Bean的？
* 要素
  * 类型：非常规 Spring 对象依赖来源
* 限制
  * 无生命周期管理
  * 无法实现延迟初始化 Bean
  * 无法通过依赖查找
### 78 | 面试题精选
* 沙雕面试题 - 注入和查找的依赖来源是否相同？
答：否，依赖查找的来源仅限于 Spring BeanDefinition 以及单例对
象，而依赖注入的来源还包括 Resolvable Dependency 以及
@Value 所标注的外部化配置

* 996 面试题 - 单例对象能在 IoC 容器启动后注册吗？
答：可以的，单例对象的注册与 BeanDefinition 不同，BeanDefinition 会
被 ConfigurableListableBeanFactory#freezeConfiguration() 方法影响，
从而冻结注册，单例对象则没有这个限制。

* 劝退面试题 - Spring 依赖注入的来源有哪些？
答：
Spring BeanDefinition
单例对象
Resolvable Dependency
@Value 外部化配置

## 第八章：Spring Bean作用域（Scopes） (9讲)

### 79 | Spring Bean作用域：为什么Spring Bean需要多种作用域？

|来源| 说明|
|:-:|:-:|
|singleton |默认 Spring Bean 作用域，一个 BeanFactory 有且仅有一个实例|
|prototype |原型作用域，每次依赖查找和依赖注入生成新 Bean 对象|
|request |将 Spring Bean 存储在 ServletRequest 上下文中|
|session |将 Spring Bean 存储在 HttpSession 中|
|application |将 Spring Bean 存储在 ServletContext 中|

层次性的应用，上下文的时候或者层次性的BeanFactory时候，id或名称并不是唯一的。（多个BeanFactory）


### 80 | "singleton" Bean作用域：单例Bean在当前Spring应用真是唯一的吗？

Bean作用域其实严格意义上面来讲不是所有的Spring的Bean，而是指的我们的BeanDefinition。

单例和原型可能同时存在，使用的时候会产生一些问题。

无论是 Singleton 还是 Prototype Bean 均会执行初始化方法回调；

不过仅 Singleton Bean 会执行销毁方法回调。

### 81 | "prototype" Bean作用域：原型Bean在哪些场景下会创建新的实例？

注意事项
* Spring 容器没有办法管理 prototype Bean 的完整生命周期，也没有办法记录示例的存在。销毁回调方法将不会执行，可以利用 BeanPostProcessor 进行清扫工作。

### 82 | "request" Bean作用域：request Bean会在每次HTTP请求创建新的实例吗？

当对象一旦生成request的时候，每次请求的时候会形成不同对象，它所引用的配置对象是不同的；

主要是基于AbstractRequest来实现，返回前端的对象实际上是一个不变代理对象，最后页面渲染的时候每次新生成一个对象。


### 83 | "session" Bean作用域：session Bean在Spring MVC场景下存在哪些局限性？

### 84 | "application" Bean作用域：application Bean是否真的有必要？

### 85 | 自定义Bean作用域：设计Bean作用域应该注意哪些原则？

### 86 | 课外资料：Spring Cloud RefreshScope是如何控制Bean的动态刷新？

上在SC里面有一种自定义的作用域RefreshScope，

### 87 | 面试题精选

* 沙雕面试题 - Spring 內建的 Bean 作用域有几种？
答：singleton、prototype、request、session、application 以及websocket

* 996 面试题 - singleton Bean 是否在一个应用是唯一的？

答：否，singleton bean 仅在当前 Spring IoC 容器（BeanFactory）中是单例对象。因为整个应用可能包含多个应用上下文，也所谓的层次性的上下文。


一个静态字段在JVM里面是否唯一？

否，通常来说是给它ClassLoader是唯一的，但是一个应用可以有多个ClassLoader。ClassLoader之间是可以相互隔离的，可以维持不同的一个静态字段。


* 劝退面试题 - “application”Bean 是否被其他方案替代？

答：可以的，实际上，“application” Bean 与“singleton” Bean 没有本质区别。(层次性上下文)，它无非就是在某个地方存储了一下。


## 第九章：Spring Bean生命周期（Bean Lifecycle） (18讲)

### 88 | Spring Bean 元信息配置阶段：BeanDefinition配置与扩展

### 89 | Spring Bean 元信息解析阶段：BeanDefinition的解析

* 面向资源 BeanDefinition 解析
  * BeanDefinitionReader
  * XML 解析器 - BeanDefinitionParser
* 面向注解 BeanDefinition 解析
  * AnnotatedBeanDefinitionReader

### 90 | Spring Bean 注册阶段：BeanDefinition与单体Bean注册

* BeanDefinition 注册接口
  * BeanDefinitionRegistry

### 91 | Spring BeanDefinition合并阶段：BeanDefinition合并过程是怎样出现的？

* BeanDefinition 合并
  * 父子 BeanDefinition 合并
    * 当前 BeanFactory 查找
    * 层次性 BeanFactory 查找
    
在合并过程中，通常会把一个GenericBeanDefinition变成一个RootBeanDefinition分类型。子类合并的时候，通常会把子的Definition
来覆盖父的Definition里的实例，在最终得到BeanDefinition的时候合并后的结果就是说基本上是通过一个GenericBeanDefinition变成一个RootBeanDefinition。


### 92 | Spring Bean Class加载阶段：Bean ClassLoader能够被替换吗?

 * ClassLoader 类加载
 * Java Security 安全控制
 * ConfigurableBeanFactory 临时 ClassLoader

 其实我们的BeanDefinition变成一个Class的过程，还是利用我们传统的Java的ClassLoader

### 93 | Spring Bean实例化前阶段：Bean的实例化能否被绕开？

 * 非主流生命周期 - Bean 实例化前阶段
   * InstantiationAwareBeanPostProcessor#postProcessBeforeInstantiation
   
它是一个在初始在实例化之前的一个前置操作


### 94 | Spring Bean实例化阶段：Bean实例是通过Java反射创建吗？

实例化方式
 * 传统实例化方式
   * 实例化策略 - InstantiationStrategy
 * 构造器依赖注入

构造器注入按照类型注入，resolveDependency

### 95 | Spring Bean实例化后阶段：Bean实例化后是否一定被是使用吗？

* Bean 属性赋值（Populate）判断
  * InstantiationAwareBeanPostProcessor#postProcessAfterInstantiation

可以理解为它是个Bean的赋值的一个判断

### 96 | Spring Bean属性赋值前阶段：配置后的PropertyValues还有机会修改吗？

* Bean 属性值元信息
  * PropertyValues
* Bean 属性赋值前回调
  * Spring 1.2 - 5.0：InstantiationAwareBeanPostProcessor#postProcessPropertyValues
  * Spring 5.1：InstantiationAwareBeanPostProcessor#postProcessProperties
  
元信息就是称为一个类叫PropertyValues，BeanDefinition里面有个属性的一个值称为PropertyValues，

### 97 | Aware接口回调阶段：众多Aware接口回调的顺序是安排的？

* Spring Aware 接口
  * BeanNameAware
  * BeanClassLoaderAware
  * BeanFactoryAware
  * EnvironmentAware
  * EmbeddedValueResolverAware
  * ResourceLoaderAware
  * ApplicationEventPublisherAware
  * MessageSourceAware
  * ApplicationContextAware
  
如果你是个简单的一个BeanFactory实现，比如像DefaultListableBeanFactory，这个时候你是没办法进行所谓的和应用上下文相关的Aware

### 98 | Spring Bean初始化前阶段：BeanPostProcessor

* 已完成
  * Bean 实例化
  * Bean 属性赋值
  * Bean Aware 接口回调
  * 方法回调
  * BeanPostProcessor#postProcessBeforeInitialization

### 99 | Spring Bean初始化阶段：@PostConstruct、InitializingBean以及自定义方法
* Bean 初始化（Initialization）
  * @PostConstruct 标注方法
  * 实现 InitializingBean 接口的 afterPropertiesSet() 方法
  * 自定义初始化方法
  
一个BeanFactory可以对应多个BeanPostProcessor实现

BeforeInitialization 初始化前阶段就已经完成了PostConstruct 

### 100 | Spring Bean初始化后阶段：BeanPostProcessor

* 方法回调
  * BeanPostProcessor#postProcessAfterInitialization


initializeBean() 逐一回调
Aware回调:invokeAwareMethods
BeforeInitialization:applyBeanPostProcessorsBeforeInitialization
Initialize:invokeInitMethods
AfterInitialization:applyBeanPostProcessorsAfterInitialization





### 101 | Spring Bean初始化完成阶段：SmartInitializingSingleton

* 方法回调
  * Spring 4.1 +：SmartInitializingSingleton#afterSingletonsInstantiated

在我们的所有的单例对象实例化之后，BeanDefinition已经变成Bean之后，逐一地进行我们的Singleton回调。



### 102 | Spring Bean销毁前阶段：DestructionAwareBeanPostProcessor用在怎样的场景?

* 方法回调
  * DestructionAwareBeanPostProcessor#postProcessBeforeDestruction
  
容器里面被销毁

### 103 | Spring Bean销毁阶段：@PreDestroy、DisposableBean以及自定义方法

* Bean 销毁（Destroy）
  * @PreDestroy 标注方法
  * 实现 DisposableBean 接口的 destroy() 方法
  * 自定义销毁方法

### 104 | Spring Bean垃圾收集（GC）：何时需要GC Spring Bean？

* Bean 垃圾回收（GC）
  * 关闭 Spring 容器（应用上下文）
  * 执行 GC
  * Spring Bean 覆盖的 finalize() 方法被回调

### 105 | 面试题精选

* 沙雕面试题 - BeanPostProcessor 的使用场景有哪些？

答：BeanPostProcessor 提供 Spring Bean 初始化前和初始化后的生
命周期回调，分别对应 postProcessBeforeInitialization 以及
postProcessAfterInitialization 方法，允许对关心的 Bean 进行扩展
，甚至是替换。（返回null是没有调整）
（这个对象也许是本身参数传过来的Bean对象，也可能不是传输Bean对象，但是如果是返回null的话，相对说是没有调整）

加分项：其中，ApplicationContext 相关的 Aware 回调也是基于BeanPostProcessor 实现，即 ApplicationContextAwareProcessor（内部类，只有在ApplicationContext中调用）。

* 996 面试题 - BeanFactoryPostProcessor 与BeanPostProcessor 的区别

答：BeanFactoryPostProcessor 是 Spring BeanFactory（实际为
ConfigurableListableBeanFactory） 的后置处理器，用于扩展
BeanFactory，或通过 BeanFactory 进行依赖查找和依赖注入

加分项：BeanFactoryPostProcessor 必须有 Spring ApplicationContext
执行，BeanFactory 无法与其直接交互。（就是它的一个BeanFactory的后置操作）

而 BeanPostProcessor 则直接与BeanFactory 关联，属于 N 对 1 的关系。

* 劝退面试题 - BeanFactory 是怎样处理 Bean 生命周期？

答：
BeanFactory 的默认实现为 DefaultListableBeanFactory，其中 Bean生命周期与方法映射如下：
BeanDefinition 注册阶段 - registerBeanDefinition
BeanDefinition 合并阶段 - getMergedBeanDefinition
Bean 实例化前阶段 - resolveBeforeInstantiation
Bean 实例化阶段 - createBeanInstance
Bean 初始化后阶段 - populateBean
Bean 属性赋值前阶段 - populateBean
Bean 属性赋值阶段 - populateBean
Bean Aware 接口回调阶段 - initializeBean
Bean 初始化前阶段 - initializeBean
Bean 初始化阶段 - initializeBean
Bean 初始化后阶段 - initializeBean
Bean 初始化完成阶段 - preInstantiateSingletons
Bean 销毁前阶段 - destroyBean
Bean 销毁阶段 - destroyBean

## 第十章：Spring配置元信息（Configuration Metadata） (17讲)

### 106 | Spring配置元信息：Spring存在哪些配置元信息？它们分别用在什么场景？

* 配置元信息
  * Spring Bean 配置元信息 - BeanDefinition
  * Spring Bean 属性元信息 - PropertyValues
  * Spring 容器配置元信息
  * Spring 外部化配置元信息 - PropertySource
  * Spring Profile 元信息 - @Profile

### 107 | Spring Bean配置元信息：BeanDefinition

* Bean 配置元信息 - BeanDefinition
  * GenericBeanDefinition：通用型 BeanDefinition
  * RootBeanDefinition：无 Parent 的 BeanDefinition 或者合并后 BeanDefinition
  * AnnotatedBeanDefinition：注解标注的 BeanDefinition

### 108 | Spring Bean属性元信息：PropertyValues

* Bean 属性元信息 - PropertyValues
  * 可修改实现 - MutablePropertyValues
  * 元素成员 - PropertyValue
  * Bean 属性上下文存储 - AttributeAccessor
  * Bean 元信息元素 - BeanMetadataElement

辅助定义BeanDefinition，同时也可以在一些生命周期阶段辅助我们进行相关的自定义。


### 109 | Spring容器配置元信息

* Spring XML 配置元信息 - beans 元素相关
|beans元素属性 |默认值 |使用场景|
|:-:|:-:|:-:|
|profile| null（留空）| Spring Profiles 配置值|
|default-lazy-init| default |当 outter beans “default-lazy-init” 属性存在时，继承该值，否则为“false”|
|default-merge |default |当 outter beans “default-merge” 属性存在时，继承该值，否则为“false”|
|default-autowire| default |当 outter beans “default-autowire” 属性存在时，继承该值，否则为“no”|
|default-autowire-candidates |null（留空） |默认 Spring Beans 名称 pattern|
|default-init-method |null（留空）| 默认 Spring Beans 自定义初始化方法|
|default-destroy-method| null（留空）| 默认 Spring Beans 自定义销毁方法|

* Spring XML 配置元信息 - 应用上下文相关

|XML 元素| 使用场景|
|:-:|:-:|
|<context:annotation-config /> |激活 Spring 注解驱动|
|<context:component-scan /> |Spring @Component 以及自定义注解扫描|
|<context:load-time-weaver /> |激活 Spring LoadTimeWeaver|
|<context:mbean-export />| 暴露 Spring Beans 作为 JMX Beans|
|<context:mbean-server /> |将当前平台作为 MBeanServer|
|<context:property-placeholder /> |加载外部化配置资源作为 Spring 属性配置|
|<context:property-override /> |利用外部化配置资源覆盖 Spring 属性值|

BeanDefinitionParserDelegate处理相关的上下文容器，相关的属性和一些默认值的呈现


### 110 | 基于XML资源装载Spring Bean配置元信息

* Spring Bean 配置元信息
|XML 元素| 使用场景|
|:-:|:-:|
|<beans:beans /> |单 XML 资源下的多个 Spring Beans 配置|
|<beans:bean />| 单个 Spring Bean 定义（BeanDefinition）配置|
|<beans:alias />| 为 Spring Bean 定义（BeanDefinition）映射别名|
|<beans:import />| 加载外部 Spring XML 配置资源|

底层实现 - XmlBeanDefinitionReader

推荐用schema(XSD)的方式校验。因为DTD的结构性比较松散，理解方面相对来说会更加的没那么紧凑。


这个Bean的加载是有序的，也就是说它是通过first-in-first-out方式；

BeanDefinition只能确保Bean的定义的一个顺序；

Bean是不是要加载，取决于依赖查找的时机或依赖注入的时机。这两个时机是不确定的，那是由用户的代码行为来进行控制的。

如果你用ApplicationContext，AbstractApplicationContext加载的时候，它在最后面refresh的时候，这个过程中它会通过BeanDefinition的顺序来进行初始化。

                         
### 111 | 基于Properties资源装载Spring Bean配置元信息：为什么Spring官方不推荐？

* Spring Bean 配置元信息
|Properties 属性名| 使用场景|
|:-:|:-:|
|(class) Bean| 类全称限定名|
|(abstract)| 是否为抽象的 BeanDefinition|
|(parent) |指定 parent BeanDefinition 名称|
|(lazy-init)| 是否为延迟初始化|

底层实现 - PropertiesBeanDefinitionReader


* Spring Bean 配置元信息


|Properties 属性名 |使用场景|
|:-:|:-:|
|(ref) |引用其他 Bean 的名称|
|(scope) |设置 Bean 的 scope 属性|
|${n} |n 表示第 n+1 个构造器参数|


底层实现 - PropertiesBeanDefinitionReader


### 112 | 基于Java注解装载Spring Bean配置元信息

* Spring 模式注解
|Spring 注解 |场景说明| 起始版本|
|:-:|:-:|:-:|
|@Repository |数据仓储模式注解 |2.0|
|@Component| 通用组件模式注解| 2.5|
|@Service| 服务模式注解| 2.5|
|@Controller Web| 控制器模式注解 |2.5|
|@Configuration |配置类模式注解 |3.0|

* Spring Bean 定义注解
|Spring 注解 |场景说明| 起始版本|
|:-:|:-:|:-:|
|@Bean| 替换 XML 元素 <bean> |3.0|
|@DependsOn |替代 XML 属性 <bean depends-on="..."/> |3.0|
|@Lazy| 替代 XML 属性 <bean lazy-init="true|falses" /> |3.0|
|@Primary| 替换 XML 元素 <bean primary="true|false" /> |3.0|
|@Role| 替换 XML 元素 <bean role="..." /> |3.1|
|@Lookup |替代 XML 属性 <bean lookup-method="..."> |4.1|

* Spring Bean 依赖注入注解
|Spring 注解 |场景说明| 起始版本|
|:-:|:-:|:-:|
|@Autowired |Bean 依赖注入，支持多种依赖查找方式 |2.5|
|@Qualifier |细粒度的 @Autowired 依赖查找 |2.5|
|@Resource| 类似于 @Autowired |2.5|
|@Inject |类似于 @Autowired |2.5|

* Spring Bean 条件装配注解
|Spring 注解 |场景说明| 起始版本|
|:-:|:-:|:-:|
|@Profile |配置化条件装配 |3.1|
|@Conditional |编程条件装配| 4.0|

* Spring Bean 生命周期回调注解
|Spring 注解| 场景说明| 起始版本|
|:-:|:-:|:-:|
|@PostConstruct |替换 XML 元素 <bean init-method="..." /> 或 InitializingBea |2.5|
|@PreDestroy |替换 XML 元素 <bean destroy-method="..." /> 或 DisposableBean| 2.5|

### 113 | Spring Bean配置元信息底层实现之XML资源

* Spring BeanDefinition 解析与注册
|实现场景| 实现类 |起始版本|
|:-:|:-:|:-:|
|XML |资源 XmlBeanDefinitionReader |1.0|
|Properties| 资源 PropertiesBeanDefinitionReader |1.0|
|Java 注解| AnnotatedBeanDefinitionReader |3.0|



Spring XML 资源 BeanDefinition 解析与注册

* 核心 API - XmlBeanDefinitionReader
    * 资源 - Resource
    * 底层 - BeanDefinitionDocumentReader
      * XML 解析 - Java DOM Level 3 API
      * BeanDefinition 解析 - BeanDefinitionParserDelegate
      * BeanDefinition 注册 - BeanDefinitionRegistry

### 114 | Spring Bean配置元信息底层实现之Properties资源

Spring Properties 资源 BeanDefinition 解析与注册

* 核心 API - PropertiesBeanDefinitionReader
  * 资源
     * 字节流 - Resource
     * 字符流 - EncodedResource
  * 底层
     * 存储 - java.util.Properties
     * BeanDefinition 解析 - API 内部实现
     * BeanDefinition 注册 - BeanDefinitionRegistry
     
### 115 | Spring Bean配置元信息底层实现之Java注解

Spring Java 注册 BeanDefinition 解析与注册
* 核心 API - AnnotatedBeanDefinitionReader
  * 资源
     * 类对象 - java.lang.Class
  * 底层
     * 条件评估 - ConditionEvaluator
     * Bean 范围解析 - ScopeMetadataResolver
     * BeanDefinition 解析 - 内部 API 实现
     * BeanDefinition 处理 - AnnotationConfigUtils.processCommonDefinitionAnnotations
     * BeanDefinition 注册 - BeanDefinitionRegistry

### 116 | 基于XML资源装载Spring IoC容器配置元信息

* Spring IoC 容器相关 XML 配置
|命名空间| 所属模块  |Schema资源 URL|
|:-:|:-:|:-:|
|beans|spring-beans| https://www.springframework.org/schema/beans/spring-beans.xsd|
|context| spring-context |https://www.springframework.org/schema/context/spring-context.xsd|
|aop |spring-aop |https://www.springframework.org/schema/aop/spring-aop.xsd|
|tx |spring-tx |https://www.springframework.org/schema/tx/spring-tx.xsd|
|util |spring-beans| https://www.springframework.org/schema/util/spring-util.xsd|
|tool| spring-beans |https://www.springframework.org/schema/tool/spring-tool.xsd|

### 117 | 基于Java注解装载Spring IoC容器配置元信息

* Spring IoC 容器装配注解
|Spring 注解 |场景说明 |起始版本|
|:-:|:-:|:-:|
|@ImportResource |替换 XML 元素 <import> |3.0|
|@Import |导入 Configuration Class |3.0|
|@ComponentScan |扫描指定 package 下标注 Spring 模式注解的类 |3.1|

首先它自身就是说它是标注在某个类上面的，这个类必须是Configuration Class，把Import或ImportResource解析完之后，来再次地把里面的内容再进行重新地进行解析（递归操作）。最终达到它的完整的一个解析的过程。

* Spring IoC 配属属性注解
|Spring 注解| 场景说明 |起始版本|
|:-:|:-:|:-:|
|@PropertySource |配置属性抽象| PropertySource 注解|3.1|
|@PropertySources |@PropertySource 集合注解|4.0|

### 118 | 基于Extensible XML authoring 扩展Spring XML元素

* Spring XML 扩展
  * 编写 XML Schema 文件：定义 XML 结构
  * 自定义 NamespaceHandler 实现：命名空间绑定
  * 自定义 BeanDefinitionParser 实现：XML 元素与 BeanDefinition 解析
  * 注册 XML 扩展：命名空间与 XML Schema 映射
  
  

### 119 | Extensible XML authoring扩展原理

### 120 | 基于Properties资源装载外部化配置

* 注解驱动
  * @org.springframework.context.annotation.PropertySource
  * @org.springframework.context.annotation.PropertySources
* API 编程
  * org.springframework.core.env.PropertySource
  * org.springframework.core.env.PropertySources
  
### 121 | 基于Yaml资源装载外部化配置

API 编程
* org.springframework.beans.factory.config.YamlProcessor
  *  org.springframework.beans.factory.config.YamlMapFactoryBean
  *  org.springframework.beans.factory.config.YamlPropertiesFactoryBean

### 122 | 面试题

沙雕面试题 - Spring 內建 XML Schema 常见有哪些？

答：

|命名空间| 所属模块| Schema 资源 URL|
|---|---|---|
|beans |spring-beans |https://www.springframework.org/schema/beans/spring-beans.xsd|
|context |spring-context |https://www.springframework.org/schema/context/springcontext.xsd|
|aop| spring-aop |https://www.springframework.org/schema/aop/spring-aop.xsd|
|tx |spring-tx| https://www.springframework.org/schema/tx/spring-tx.xsd|
|util |spring-beans |https://www.springframework.org/schema/util/spring-util.xsd|
|tool |spring-beans| https://www.springframework.org/schema/tool/spring-tool.xsd|

996 面试题 - Spring配置元信息具体有哪些？

答：

* Bean 配置元信息：通过媒介（如 XML、Proeprties 等），解析 BeanDefinition
* IoC 容器配置元信息：通过媒介（如 XML、Proeprties 等），控制 IoC 容器行为，比如注解驱动、AOP 等
* 外部化配置：通过资源抽象（如 Proeprties、YAML 等），控制 PropertySource
* Spring Profile：通过外部化配置，提供条件分支流程


劝退面试题 - Extensible XML authoring 的缺点？

答：

* 高复杂度：开发人员需要熟悉 XML Schema，spring.handlers，spring.schemas以及 Spring API 。
* 嵌套元素支持较弱：通常需要使用方法递归或者其嵌套解析的方式处理嵌套（子）元素。
* XML 处理性能较差：Spring XML 基于 DOM Level 3 API 实现，该 API 便于理解，然而性能较差。
* XML 框架移植性差：很难适配高性能和便利性的 XML 框架，如 JAXB。

## 第十一章：Spring资源管理（Resources） (11讲)

### 123 | 引入动机：为什么Spring不使用Java标准资源管理，而选择重新发明轮子？

* Java 标准资源管理强大，然而扩展复杂，资源存储方式并不统一
* Spring 要自立门户（重要的话，要讲三遍）
* Spring “抄”、“超” 和 “潮

124 | Java标准资源管理：Java URL资源管理存在哪些潜规则？

125 | Spring资源接口：Resource接口有哪些语义？它是否“借鉴”了SUN的实现呢？

126 | Spring内建Resource实现：Spring框架提供了多少种内建的Resource实现呢？

127 | Spring Resource接口扩展：Resource能否支持写入以及字符集编码？

128 | Spring资源加载器：为什么说Spring应用上下文也是一种Spring资源加载器？

129 | Spring通配路径资源加载器：如何理解路径通配Ant模式？

130 | Spring通配路径模式扩展：如何扩展路径匹配的规则？

131 | 依赖注入Spring Resource：如何在XML和Java注解场景注入Resource对象？

132 | 依赖注入ResourceLoader：除了ResourceLoaderAware回调注入，还有哪些注入方法？

### 133 | 面试题精选

沙雕面试题 - Spring 配置资源中有哪些常见类型？

答：
* XML 资源
* Properties 资源
* YAML 资源

996 面试题 - 请例举不同类型 Spring 配置资源？

答：
* XML 资源
  * 普通 Bean Definition XML 配置资源 - *.xml
  * Spring Schema 资源 - *.xsd
* Properties 资源
  * 普通 Properties 格式资源 - *.properties
  * Spring Handler 实现类映射文件 - META-INF/spring.handlers
  * Spring Schema 资源映射文件 - META-INF/spring.schemas
* YAML 资源
  * 普通 YAML 配置资源 - *.yaml 或 *.yml

劝退面试题 - Java 标准资源管理扩展的步骤？

答：
* 简易实现
  * 实现 URLStreamHandler 并放置在 sun.net.www.protocol.${protocol}.Handler 包下
* 自定义实现
  * 实现 URLStreamHandler 
  * 添加 -Djava.protocol.handler.pkgs 启动参数，指向 URLStreamHandler 实现类的包下
* 高级实现
  * 实现 URLStreamHandlerFactory 并传递到 URL 之中
  
## 第十二章：Spring国际化（i18n） (5讲)

134 | Spring国际化使用场景

135 | Spring国际化接口：MessageSource不是技术的创造者，只是技术的搬运工？

136 | 层次性MessageSource：双亲委派不是ClassLoader的专利吗？

137 | Java国际化标准实现：ResourceBundle潜规则多？

138 | Java文本格式化：MessageFormat脱离Spring场景，能力更强大？

### 139 | 面试题精选 

沙雕面试题 - Spring 国际化接口有哪些？

答：
* 核心接口 - MessageSource
* 层次性接口 - org.springframework.context.HierarchicalMessageSource

996 面试题 - Spring 有哪些 MessageSource 內建实现？

答：
* org.springframework.context.support.ResourceBundleMessageSource
* org.springframework.context.support.ReloadableResourceBundleMessageSource
* org.springframework.context.support.StaticMessageSource
* org.springframework.context.support.DelegatingMessageSource

劝退面试题 - 如何实现配置自动更新 MessageSource？

答：
* 主要技术
  * Java NIO 2：java.nio.file.WatchService
  * Java Concurrency : java.util.concurrent.ExecutorService
  * Spring：org.springframework.context.support.AbstractMessageSource