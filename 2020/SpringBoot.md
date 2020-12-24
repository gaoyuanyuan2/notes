# Spring Boot 编程思想

## 版本
|Spring Boot  | Spring Framework | JDK|
|---|---|---|
|2.1.0.RELEASE|	 5.1.2.RELEASE |1.8+|
|2.0.2.RELEASE|	 5.0.6.RELEASE| 1.8+|
|2.0.0.RELEASE|	 5.0.4.RELEASE| 1.8+|
|1.5.10.RELEASE	 |4.3.14.RELEASE| 1.6+|
|1.4.7.RELEASE	 |4.3.9.RELEASE| 1.6+|
|1.4.7.RELEASE	 |4.3.9.RELEASE| 1.6+|
|1.3.8.RELEASE	 |4.2.8.RELEASE| 1.6+|
|1.2.8.RELEASE    |4.1.9.RELEASE| 1.6+|
|1.1.9.RELEASE    |4.0.8.RELEASE| 1.6+|
|1.0.2.RELEASE    |4.0.3.RELEASE| 1.6+|

## Spring Boot 初步了解

嵌入式容器，无需随Java EE容器启动而装载。

Spring Boot出现嵌入式容器启动方式后，嵌入式容器则成为应用的一部分， 从本质上来说，它属于Spring 应用上下文的组件Beans，
这些组件和其他组件均由自动装配特性组装成Spring Bean 的定义（BeanDefinition），随Spring应用上下文启动而注册并初始化。


### 特征

* 创建独立的Spring应用

* 直接嵌入Tomcat、Jetty 或Undertow等Web容器(不需要部署WAR文件)

* 提供固化的 “starter”依赖，简化构建配置

* 当条件满足时自动地装配Spring或第三方类库

* 提供运维(Production-Ready) 特性，如指标信息(Metrics)、 健康检查及外部化配置：绝无代码生成，并且不需要XML配置

传统容器启动是Servlet引导

SpringBoot 2.0 是由SpringApplication启动的


## 理解独立的Spring应用

Spring Boot 1.x 中仅有Servlet容器实现

Spring Boot 2.0开始增加了Reactive Web 容器的实现 ->Spring 5.0 WebFlux

### 运行方式

java -jar  生产环境运行方式

mvn spring-boot:run 开发阶段运行方式

### Jar 结构

demo-0.0.1-SNAPSHOT.jar  包含第三方依赖

demo-0.0.1-SNAPSHOT.jar.original 不包含第三方依赖

执行 maven 插件后， .jar.original被 repackage成 .jar


解压jar包（模仿JavaEE的War包结构）

BOOT-INF/classes 存放编译的class文件

BOOT-INF/lib   存放应用依赖的JAR包

META-INF/ 存放应用相关的元信息 MANIFEST.MF

org/ 存放Spring Boot相关的class文件

MANIFEST.MF
```properties
Manifest-Version: 1.0
Implementation-Title: spring-boot-demo
Implementation-Version: 0.0.1-SNAPSHOT
Start-Class: com.yan.demo.Application
Spring-Boot-Classes: BOOT-INF/classes/
Spring-Boot-Lib: BOOT-INF/lib/
Build-Jdk-Spec: 1.8
Spring-Boot-Version: 2.2.0.RELEASE
Created-By: Maven Archiver 3.4.0
## Jar包的启动器
Main-Class: org.springframework.boot.loader.JarLauncher
```
`org.springframework.boot.loader.JarLauncher`会将这些JAR文件作为`com.yan.demo.Application`的库依赖，所以JarLauncher能够引导，
反之`com.yan.demo.Application`这不行。

java -java 执行JarLauncher 父类的方法Launcher#launch(String[],String,ClassLoader)

URLStreamHandler 子类

`sun.net.www.protocol.file.Handler`

`sun.net.www.protocol.jar.Handler`

`sun.net.www.protocol.http.Handler`

`sun.net.www.protocol.https.Handler`

`sun.net.www.protocol.ftp.Handler`

如需扩展择则需继续URLStreamHandler类


org.springframework.boot.loader.Launcher

ExecutableArchiveLauncher extends Launcher 

WarLauncher extends ExecutableArchiveLauncher

JarLauncher extends ExecutableArchiveLauncher

总而言之，打包WAR文件是一种兼容措施，既能被WarLauncher启动，又能兼容 Servlet容器环境。
换言之，WarLauncher与JarLauncher并无本质差别，所以建议Spring Boot应用使用非传统Web部署时尽可能地使用JAR归档方式。


## 嵌入式容器

* Tomcat

* Jetty

* Undertow

### 说明

* Netty Web Server仅属于版本的新特性

* Reactive Web 默认实现为Netty Web Server

* Servlet 3.1+ 容器同样满足Reactive 异步非阻塞的特性


反观Spring Boot 2.0的实现，它利用嵌入式Tomcat API 构建为TomcatWebServer Bean，由Spring应用上下文将其引导，其嵌入式Tomcat
组件的运行（如Context，Connector等），以及ClassLoader的装载均有Spring Boot架构代码实现。

Spring Boot 可执行WAR文件则需要在不解压当前War文件的前提下读取其中的资源，这就是为什么spring-boot-loader需要覆盖内建JAR
协议的URLStreamHandler实现的原因。

总而言之，Tomcat Maven插件的版本支持6-8版本，对应的Servlet规范支持2.5-3.1版本。同时，从Servlet 3.0开始， Servlet组件均能
通过ServletContext 
API在运行时装配，如Servlet、Filter和Listener,再结合ServletContainerInitializer生命周期回调，
可实现Servlet组件的自动装配，Spring Framework 3.1同样运用了这些特性，抽象出WebApplicationInitializer接口，
降低ServletContainerInitializer接口的理解成本

spring-boot-starter-web 与spring-boot-starter-webflux同时使用时，webflux会被忽略。


当前应用属于Spring Boot WebFlux 应用，并且使用基于Servlet 技术所构建的UndertowServletWebServer实例作为嵌入式
Reactive Web服务器。

Spring Boot 2.0新引入了一种ApplicationContext实现，实现WebServerApplicationContext,
它提供获取WebServer的接口方法getWebServer():


## 理解自动装配


### 注解

@SpringBootApplication 聚合注解，包含以下三个注解

@SpringBootConfiguration

@EnableAutoConfiguration

@ComponentScan ->@Configuration->@Component(派生注解)


@AliasFor 用于桥接其他注解属性,Spring Framework 4.2才支持


@ConditionalOnClass 标注@Configuration类上是，当且仅当目标类存在于Class Path下是才予以装配


## 为生产准备的特性

metrics（指标）

health checks（健康检查）

externalized configuration（外部配置）

Spring Boot Actuator

Endpoints 仅有health和info为默认暴露的Web Endpoints

@ConfigurationProperties 绑定到结构化对象

### ImportSelector接口

ImportSelector接口(实现selectImports (AnnotationMetadata)方法)，程序动态地决定哪些Spring Bean需要被导入。可是ImportSelector 实现类必须暴露成
Spring Bean否则selectImports(AnnotationMetadata)方法不会被Spring容器调用。

## 走向注解驱动编程

@RestControllerAdvice,作为@RestController AOP拦截通知，它扮演类似于@ControllerAdvice 对于@Controller的角色。
在浏览器跨域资源访问方面，Spring Framework 4.2开始引入@Cross0rigin。



@Indexed 不能孤立地存在，需要在工程pom.xml中增加org. springframework:spring-context-indexer依赖:

```xml
<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context-indexer</artifactId>
        <version>5.0.6.RELEASE</version>
        <optional>true</optional>
</dependency>
```

当工程打包为JAR或在IDE工具中重新构建后，META- INF/spring.components文件将自动生成。
换言之，该文件在编译时生成。当Spring应用上下文执行ComponentScan扫描时，META- INF/spring.components
将被CandidateComponentsIndexLoader 读取并加载，转化为CandidateComponentsIndex对象，
进而@ComponentScan不再扫描指定的package。
而是读取CandidateComponentsIndex对象，从而达到提升性能的目的。

元注解：是指一个能声明在其他注解上的注解

MetaDataReader接口，包含了类和注解的元信息读取方法

Spring Framework从4.0版本开始支持多层次@Component“派生性”。由于Spring Boot 1.x最低依赖Spring Framework 4.0,
因此多层次@Component“派生性”被Spring Boot继承。

在Java反射编程模型中，注解之间无法继承，也不能实现接口

Annotation所有的注解都实现了该接口，基于Java反射API获取元（嵌套）注解及属性信息的实现是颇为复杂的，
需要递归的获取元注解信息

较低层注解能够覆盖其元注解的同名属性

### 组合注解

Spring Framework并没有考迪使用Java反射的手段来解析元注解信息，而是抽象出AnnotationMetadata接口，
其实现类为AnnotationMetadataReadingVisitor。并且从Spring Framework 4.0开始，
AnnotationMetadataReadingVisitor所关联的AnnotationMetadataReadingVisitor
采用递归查找元注解，使得多层次元注解信息保存在AnnotationMetadataReadingVisitor的metaAnnotationMap字段中。

SpringFramework的类加教则通过ASM实现如ClassReader。 相对于ClassLoader体系。
Spring ASM更为底层，读取的是类资源，直接操作其中的字节码，获取相关元信息，
同时便于Spring相关的字节码提升、在读取元信息方面，Spring 抽象出MetadataReader接口。



## Spring 注解驱动设计模式

|框架实现 | @Enable注解模块 |激活模块|
|---|---|---|
|Spring Framework|@EnableWebMvc|Web MVC模块|
||@EnableTransactionManagement|事务管理模块|
||@EnableCaching|Caching模块|
||@EnableMBeanExport|JMX模块|
||@EnableAsync|异步处理模块|
||@EnableWebFlux|Web Flux模块|
||@EnableAspectJAutoProxy|AspectJ代理模块|
|Spring Boot|@EnableAutoConfiguration|自动装配模块|
||@EnableManagementContext|Actuator管理榄块|
||@EnableConfigurationProperties|配置属性绑定模块|
||@EnableOAuth2Sso|OAuth2单点登录模块|
|Spring Cloud|@EnableEurekaServer|Eureka 服务器模块|
||@EnableConfigServer|配置服务器模块|
||@EnableFeignClients|Feign客户端模块|
||@EnableZuulProxy|服务网关Zuul模块|
||@EnableCircuitBreaker|服务熔断模块|


引入“@Enable模块驱动”的意义在能够简化装配步骤， 实现了“按需装配”， 同时屏蔽组件集合装配的细节。

然而在Spring Framework 3.1中，@Import的职责范围有所扩大、还可以用于声明至少一个@Bean方法的类，
以及ImportSelector或ImportBeanDefinitionRegistrar的实现类。

将@Configuration 类和@Bean方法声明类归类为“注解驱动”，而ImportSelector 或ImportBeanDefinitionRegistrar
的实现类则归于“接口编程”。

ImportBeanDefinitionRegistrar相对于ImportSelector 而言，
其编程复杂度更高，除注解元信息AnnotationMetadata作为入参外，接口将Bean定文(BeanDefinition)的注册交给开发人员决定。


@Enable 模块驱动模块无论来自Spring 内建，还是自定义，均使用@Import实现，并且@Import的职责在于装载导入类(Importing Class)，
将其定义为Spring Bean。结合当前场景，导入类主要为@Configuration Class、 ImportSelector实现及ImportBeanDefinitionRegistrar实现。

### 装载ImportSelector和ImportBeanDefinitionRegistrar实现
    
由于ImportSelector和ImportBeanDefinitionRegistrar从Spring Framework 3.1才开始引入，所以3.0版本中不会出现两者的实现。
由于BeanDefinitionRegistryPostProcessor从Spring Framework 3.0.1开始引入，
ConfigurationClassPostProcessor的实现也随之发生变化，其实现接口从BeanFactoryPostProcessor替换为BeanDefinitionRegistryPostProcessor,
且BeanDefinitionRegistryPostProcessor扩展了BeanFactoryPostProcessor接口，
所以ConfigurationClassPostProcessor存在两阶段实现。

通过AssignableTypeFilter判断当前候选Class元注解@Import是否赋值ImportSelector或ImportBeanDefinitionRegistrar实现，
从而决定是否执行ImportSelector或ImportBeanDefinitionRegistrar的处理，
其中importingClassMetadata 就是当前元注解@Import的AnnotationMetadata对象。

综上所述，ConfigurationClassPostProcessor 负责筛选@Component Class 、@Configuration Class 及@Bean方法的Bean 定义(BeanDefinition)
, ConfigurationClassParser则从候选的Bean定义中解析出ConfigurationClass集合，
随后被ConfigurationClassBeanDefinitionReader转化并注册BeanDefinition.

### Web 自动装配原理

正是Servlet3.0技术，其中“ServletContext配置方法”和“运行时插拔”大特性是"Web自动化装配的技术保障。

在传统的Java Web应用中，Servlet 技术的运用占比绝对领先。(基于Servlet 编程习惯，当装配Servlet. Filter 及各种Listener时，
离不开web.xml文件(Deployment Descriptor) 的配置，如<servlet>、<fllter>和<listener>元素。 而web.xml
文件一旦配置，运行时就无法调整，显然这种方式的灵话度不够，既不支持占位符，也无法支持条件、循环等逻辑。
servlet 3.0开始，这种限制被打破，其中ServletContext配置方法是Servlet 3.0 API的新特性。


* 运行时插拔

ServletContext 配置方法， 它们仅能在ServletContextListener#contexInitallzed或ServletContexInitializer#onStartup
方法中被调用。规范也定义了ServletContextListener的职责，它用于监听Servlet 上下文(ServletContext
)的生命周期事件，包括“初始化”和“销毁”两个事件。
其中“初始化”事件由ServletContextListener#contextTnitialized方法监听。
不难理解，Servlet和Filter对外提供服务前，必然经过Servlet上下文(ServletContext)初始化事件。

ContextLoaderListener是标准的ServletContextListener实现，监听ServletContext生命周期。当Web应用启动时，首先，Servlet
 容器调用ServletContextListener实现类的默认构造器，随后ContextInitialized(ServletContextEvent)方法被调用。
 反之，当Web应用关闭时，Servlet容器调用其contextDestroyed(ServletContextEvent)方法。
 
SpringServletContainerInitializer 通过实现Servlet 3.0 SPI接口ServletContainerInitializer,与@HandlesTypes
 配合过滤出WebApplicationInitializer具体实现类集合，随后顺序迭代地执行该集合元素，
 进而利用Servlet 3.0配置AP1实现Web自动装配的目的。同时，结合Spring Framework 3.2
  抽象实现AbstractAnnotationConfigDispatcherServletInitializer。极大地简化了注解驱动开发的成本。
  以上就是Spring Framework基于Servlet3.0特性而构建的Web自动装配的原理。
  

### Spring 条件装配

Java系统属性或者操作系统环境变量作为Spring外部化配置，贯穿Spring Framework和Spring Boot 时代。


### 自动装配

常规的@ConditionalOnClass 判断需要依赖自动装配Class必须被CassLoader提前装载，然后解析其注解元信息，从而根据依赖类是否存在来判断装配与否，
同时，Spring应用上下文处理@Conditional的时机较晚。然而通过读取META-INF/spring-autoconfigure-metadata.properties资源的
“ConditionalOnClass"配置元信息，并判断其依赖类的存在性，不但实现的逻辑直接，而且减少了自动装配的计算时间。

总而言之，AutoConfigurationImportSelector 读取自动装配Class的流程为:

(1)通过SpringFactoriesLoader#loadFactoryNames(Class ,ClassLoader)方法读取所有META-INF/spring.factories
资源中@EnableAutoConfiguration所关联的自动装配Class集合。

(2)读取当前配置类所标注的@EnableAutoConfiguration属性exclude和excludeName,与spring autoconfigure exclude配置属性合井为自动装配
Class排除集合。

(3)检查自动装配Class排除集合是否合法。

(4)排除候选自动装配Class集合中的排除名单。

(5)再次过滤候选自动装配Class集合中Class不存在的成员。

当自动装配Class读取完毕后，fireAutoConfigurationImportEvents(List,Set)方法执行，可能触发了一个自动装配的导入事件。

@EnableAutoConfiguration除了利用AutoConfigurationImportSelector自动装配Class，他还将标注类所在的package添加至BasePackages中，
为后续扫描提供BasePackages数据来源。

AutoConfigurationPackages.Registrar是自动装配BasePackages的核心实现。


@ConditionalOnBean 和 @ConditionalOnMissingBean 的JavaDoc强烈建议开发人员仅在自动装配中使用该条件注解。基于BeanDefinition进行名称或
类型的匹配。









资源跨域
* CrossOrigin
* WebMvcConfigurer#addCorsMappings
* 传统解决方案
  * IFrame
  * JSONP


* 自定义Servlet Web Server
  * WebServerFactoryCustomizer
* 自定义Reactive Web Server
  * ReactiveWebServerFactoryCustomizer
  
* Spring事务抽象
  * PlatformTransactionManager
* JDBC事务处理
  * DataSourceTransactionManager
* 自动装配
  * TransactionAutoConfiguration


Spring Boot配置
* 外部化配置
  * ConfigurationProperty
* @Profile
* 配置属性
  * PropertySources


Spring Boot Actuator
* 端点:各类Web和JMX Endpoints
* 健康检查: Health、HealthIndicator
* 指标:内建Metrics、自定义Metrics

Spring模式注解装配
模式注解是一种用于明在应用中扮演“组件“角色的注解。如Spring Framework中的@Repository 标注在任何类 上, 用于扮演仓储角色的模式
注解。
@Component作为一种由Spring容器托管的通用模式组件,任何被@Component标准的组件均为组件扫描的候选对象。类似地,凡是被
@Component元标注( meta-annotated )的注解,如@Service, 当任何组件标注它时 ,也被视作组件扫描的候选对象

Spring条件装配
* 定义: Bean装配的前置判断
* 举例: @Profile、@Conditional
* 实现:注解方式、编程方式



Spring厂加载机制
* 实现类: SpringFactoriesLoader
* 配置资源: META-INF/spring.factories

实现方法
* 1.激活自动装配@EnableAutoConfiguration
* 2.实现自动装配XXXAutoConfiguration
* 3.配置自动装配实现 META-INF/spring.factories


### 准备阶段

* 配置: Spring Bean来源
* 推断:Web应用类型和主引导类(MainClass)
* 加载:应用上下文初始器和应用事件监听器

#### 配置Spring Boot Bean源

Java配置Class或XML上下文配置文件集合,用于Spring Boot BeanDefinitionLoader 读取, 并且将配置源解析加载为Spring Bean定义
* 数量:一个或多个以上

#### Java配置Class

用于Spring注解驱动中Java配置类,大多数情况是Spring模式注解所标注的类, 如eConfiguration

#### XML上下文配置文件

用于Spring 传统配置驱动中的XML文件。

#### 推断Web应用类型

根据当前应用ClassPath中是否存在相关实现类来推断Web应用的类型,包括: 
* Web Reactive : WebApplicationType.REACTIVE
* Web Servlet : WebApplicationType.SERVLET
* 非Web : WebApplicationType.NONE

### 运行阶段
* 加载: SpringApplication运行监听器
* 运行: SpringApplication运行监听器
* 监听: Spring Boot事件、Spring 事件

* 创建:应用上下文、Environment、 其他(不重要)
* 失败:故障分析报告
* 回调: CommandLineRunner、ApplicationRunner


* 加载SpringApplication 运行监听器( SpringApplicationRunListeners )
利用Spring工厂加载机制,读取SpringApplicationRunListener对象集合,并且封装到组合类SpringApplicationRunListeners
* 运行SpringApplication 运行监听器( SpringApplicationRunListeners )
SpringApplicationRuntListener监听多个运行状态方法:

#### 监听Spring Boot事件Spring事件

Spring Boot通过Spr ingApplicationRunListener的实现类EventPublishingRunListener 
利用Spring Framework事件API , 广播SpringBoot事件。

#### Spring Framework事件/监听器编程模型
* Spring 应用事件
  * 普通应用事件: ApplicationEvent
  * 应用上下文事件: ApplicationContextEvent
* Spring 应用监听器
  * 接口编程模型: ApplicationListener
  * 注解编程模型: @EventListener
* Spring 应用事广播器
  * 接口: ApplicationEventMulticaster
  * 实现类: SimpleApplicationEventMulticaster
    * 执行模式:同步或异步


#### 创建Spring应用上下文( ConfigurableApplicationContext )

根据准备阶段的推断Web应用类型创建对应的ConfigurableApplicationContext实例:
* Web Reactive : AnnotationConfigReactiveWebServerApplicationContext
* Web Servlet : AnnotationConfigServletWebServerApplicationContext
* 非Web: AnnotationConfigApplicationContext


#### 创建Environment

根据准备阶段的推断Web应用类型创建对应的ConfigurableEnvironment实例:
* Web Reactive : StandardEnvironment
* Web Servlet : StandardServletEnvironment
* 非Web : StandardEnvironment

#### 认识Spring Web MVC

Spring Framework时代的一般认识
* 实现Controller
* 配置WebMVC组件
* 部署DispatcherServlet

配置Web MVC组件
* Component-scan
* RequestMappingHandlerMapping
* RequestMappingHandlerAdapter
* InternalResourceViewResolver

部署DispatcherServlet

mvn -Dmaven.test.skip -U clean package

#### Spring Framework时代的重新认识

* Web MVC核心组件
* Web MVC注解驱动
* Web MVC自动装配

处理器管理
* 映射: HandlerMapping
* 适配: HandlerAdapter
* 执行: HandlerExecutionChain

页面渲染
* 视图解析: ViewResolver
* 国际化: LocaleResolver、LocaleContextResolver
* 个性化: ThemeResolver

异常处理
* 异常解析: HandlerExceptionResolver


HandlerMapping
映射请求( Request )到处理器( Handler )加上其关联的拦截器( HandlerInterceptor )列表，其映射关系
基于不同的HandlerMapping实现的一些标准细节。其中两种主要HandlerMapping 实现，
RequestMappingHandlerMapping支持标注@RequestMapping 的方法，SimpleUr lHandlerMapping维护精
确的URI路径与处理器的映射

HandlerAdapter
帮助DispatcherServlet 调用请求处理器( Handler),无需关注其中实际的调用细节。 比如,调用注解实
现的Controller需要解析其关联的注解. HandlerAdapter 的主要目的是为了屏蔽与DispatcherServlet 之
间的诸多细节。

HandlerExceptionResolver
解析异常,可能策略是将异常处理映射到其他处理器( Handlers)、或到某个 HTML错误页面,或者其他。

ViewResolver
从处理器( Handler )返回字符类型的逻辑视图名称解析出实际的View 对象,该对象将渲染后的内容输出
到HTTP响应中。

LocaleResolver/LocaleContextResolver
从客户端解析出locale, 为其实现国际化视图。

MultipartResolver
解析多部分请求(如Web浏览器文件上传)的抽象实现

Web MVC注解驱动
* 注解配置: @Configuration ( Spring 范式注解)
* 组件激活: @EnableWebMvc ( Spring模块装配)
* 自定义组件: WebMvcConfigurer ( Spring Bean )

* 模型属性: @ModelAttribute
* 请求头: @RequestHeader
* Cookie : @CookieValue

* 校验参数: @Valid、@Validated
* 注解处理: @ExceptionHandler
* 切面通知 : @ControllerAdvice

Web MVC自动装配

* Servlet依赖: Servlet 3.0+
* Servlet SPI : ServletContainerInitializer  启动回调onStartup()
* Spring适配: SpringServletContainerInitializer

@HandlesTypes(WebApplicationInitializer.class) 筛选器

* Spring SPI : WebApplicationInitializer
* 编程驱动 : AbstractDispatcherServletInitializer
* 注解驱动 : AbstractAnnotationConfigDispatcherServletInitializer


Spring Boot时代的简化

Spring Boot时代的简化-完全自动装配
* DispatcherServlet : DispatcherServletAutoConfiguration
* 替换 @EnableWebMvc : WebMvcAutoConfiguration
* Servlet容器: ServletWebServerFactoryAutoConfiguration

Spring Boot时代的简化-装配条件
* Web类型: Servlet
* API 依赖: Servlet、Spring Web MVC
* Bean依赖: WebMvcConfigurationSupport

装配条件

Web类型判断(ConditionalOnWebApplication )
* WebApplicationType
  * Servlet类型: WebApplicationType.SERVLET
  
API判断(@ConditionalOnClass )
* Servlet
  * Servlet
* Spring Web MVC
  * DispatcherServlet
  * WebMvcConfigurer


Spring Boot时代的简化-外部化配置
* Web MVC配置: WebMvcProperties
* 资源配置: ResourceProperties

理解自动配置顺序性
* 绝对顺序: @AutoConfigureOrder
* 相对顺序: @AutoConfigureAfter

* 模板引擎
* 视图处理
* 视图内容协商

Cross-Origin Resource Sharing (CORS)
* 注解驱动: @CrossOrigin
* 代码驱动: WebMvcConfigurer# addCorsMappings
* Filter 组件: CorsFilter


* 传统Servlet部署
* 传统Servlet组件
  * 传统web.xml注册方式
  * 注解注册方式
  * 编码注册方式

* HandlerMethodReturnValueHandler
* DispatcherServlet
* Web自动装配


Spring Boot Servlet 注册
通过RegistrationBean 注册
* ServletContextInitializer
  * RegistrationBean
    * ServletListenerRegistrationBean
      * @WebListener
    * FilterRegistrationBean
      * @webFilter
    * ServletRegistrationBean
      * @WebServlet

@ServletComponentScan 扫描package ->@web* -> RegistrationBean Bean 定义-> RegistrationBean Bean

Spring Boot Servlet注册
* @Bean方式: RegistrationBean、Servlet 组件
* 注解方式: @ServletComponentScan
* 编程方式: ServletContextInitializer

### 从 Reactive 到 WebFlux

技术回顾

* 反应堆模式( Reactor )
* Proactor 模式
* 观察者模式( Observer )
* 迭代器模式( Iterator )
* Java 并发模型

关于Reactive的一些讲法
* Reactive 是异步非阻塞编程？
* Reactive 能够提升程序性能？
* Reactive 能解决传统编程模型遇到的困境？

Reactive实现框架
* RxJava: Reactive Extensions
* Reactor: Spring WebFlux Reactive类库
* FlowAPI: Java9 FlowAPI实现

观点归纳
* 阻塞导致性能瓶颈和浪费资源
* 增加线程可能会引|起资源竞争和并发问题
* 并行的方式不是银弹(不能解决所有问题)

1.如果阻塞导致性能瓶颈和资源浪费的话，Reactive也能解决这个问题?
2.为什么不直接使用Future#get() 方法强制所有 任务执行完毕,然后再统计总耗时?
3.由于以上三个方法之间没有数据依赖关系,所以执行方式由串行调整为并行后,能够达到性能提升的效果。如果方法之间
存在依赖关系时,那么提升效果是否还会如此明显,并且如何确保它们的执行顺序?

* Spring事件/监听器(同步/异步) :
  * 事件: ApplicationEvent
  * 事件监听器: ApplicationListener
  * 事件广播器: ApplicationEventMulticaster
  * 事件发布器: ApplicationEventPublisher
* Servlet事件/监听器
  * 同步
    * 事件: ServletContextEvent
    * 事件监听器: ServletContextListener
  * 异步
    * 事件: AsyncEvent
    * 事件监听器: AsyncListener

* 关键字:
  * 数据流( data streams )
  * 传播变化( propagation of change )
* 侧重点:
  * 数据结构
    * 数组( arrays )
    * 事件发射器( event emitters )
  * 数据变化

* 技术连接:
  * 观察者模式: Java observable / observer
  * 响应流模式: Java 8 Stream
  * 迭代器模式: Java Iterator



* 关键字:
  * 异步( asynchronous )
  * 数据流( data streams )
  * 并非新鲜事物( not anything new )
  * 过于理想化( idea on steroids )
* 侧重点:
  * 并发模型
  * 数据结构
  * 技术本质
* 技术连接:
  * 异步:Java Future 
  * 数据流:Java8 stream
  
  
* Reactive编程模型
  * 语言模型:响应式编程+函数式编程(可选)
  * 并发模型:多线程编程
  * 对立模型:命令式编程

* 数据结构( Data Structure )
  * 流式( Streams )
  * 序列( Sequences )
  * 事件( Events )
  
* Reactive设计模式
  * 扩展模式:观察者(Observer )
  * 对立模式:迭代器( Iterator )
  * 混合模式:反应堆( Reactor)、Proactor

* 主要目的:
  * 通常并非让应用运行更快速
  * 利用较少的资源提升伸缩性
  
* 主要目的:
  * 结构性和可读性(Composability and readability )
  * 高层次并发抽象( High level abstraction )。
* 核心技术:
  * 丰富的数据操作符( rich vocabulary of operators )
  * 背压( Backpressure )
  * 订阅式数据消费( Nothing happens until you subscribe )

总结Reactive Programming
Reactive Programming作为观察者模式( Observer )的延伸,不同于传统的命令编程方式( Imperative programming )同
步拉取数据的方式,如迭代器模式( Iterator)。而是采用数据发布者同步或异步地推送到数据流( Data Streams )的方案。
当该数据流( Data Steams )订阅者监听到传播变化时,立即作出响应动作。在实现层面上, Reactive Programming可结合
函数式编程简化面向对象语言语法的雕肿性,屏蔽并发实现的复杂细节,提供数据流的有序操作,从而达到提升代码的可读
性,以及减少Bugs出现的目的。同时, Reactive Programming结合背压( Backpressure )的技术解决发布端生成数据的速
率高于订阅段消费的问题。


Reactive Streams规范

* API组件
  * Publisher :数据发布者(上游)
  * Subscriber :数据订阅者(下游)
  * Subscription :订阅信号.
  * Processor : Publisher 和Subscriber混合体

* Subscriber信号事件
  * onSubscribe :当下游订阅时
  * onNext :当下游接收数据时
  * onComplete :当数据流( Data Streams )执行完成时
  * onError :当数据流( Data Streams )执行错误时

* 背压( Backpressure )
  * 1/O切换(I/O switch)
  * 缓冲填满( the buffers are full )
  * 数据无法接受( incapable of receiving any more data )
  * 传输设备( transmitting device )
  * 停止发送数据包( halts the sending of data packets )

* Reactive Streams JVM
  * 线程和边界间调停( mediate between threads to be bounded )
  * 发布者维持速率高于订阅者( publisher side maintains a higher rate than the subscriber )
  * 背压处理( handled by backpressure )

* Reactor
  * Propagating signals upstream (传播上游信号)
  * 无边界模式( unbounded mode )
  * 处理最大元素数量( process at most n elements )

* Subscription
* 订阅信号控制
  * request:请求上游元素的数量
  * cancel:请求停止发送数据并且清除资源

总结背压
假设下游Subscriber.工作在无边界大小的数据流水线时,当上游Publisher提供数据的速率快于下游Subscriber的消费数据速
率时,下游Subscriber将通过传播信号( request )到.上游Publisher ,请求限制数据的数量( Demand )或通知.上游停止数
据生产。

Spring实际动机
从Spring MVC注解驱动的时代开始, Spring官方有意识地去Servlet化。不过在Spring MVC的时代，
Spring扔拜托不了Servlet 容器的依赖,然而Spring借助Reactive Programming的势头, WebFlux将
Servlet容器从必须项变为可选项,并且默认采用Netty Web Server作为基础,从而组件地形成Spring全新
技术体系,包括数据存储等技术栈:


* 消费函数- Consumer
  * 只有输入,没有输出
* 生产函数- Supplier
  * 没有输入,只有输出
* 处理函数- Function
  * 有输出,有输出
* 判定函数- Predicate
  * 判定输入真伪性

结论

没有明显的速度提升(甚至性能结果稍微更恶劣)

关注编程用户友好性, Reactive编程尽管没有新增大量的代码,然而编码(和调试)却是变得更为复杂

现在面临的最大问题是缺少文档。在生成测试应用中,它已经给我们造成了最大障碍,并使得我们可能已
经缺少了关键点。因此,我们并不会太快地投入Reactive编程,同时等待关于它的更多反馈。因此，
Spring WebFlux尚未证明自身明显地优于Spring MVC。

## 外部化配置

优先级配置
* Java System Properties: 
  * `-Duser.city.post_code`
* OS Environment Variables（环境变量）
  * USER_CITY_POST_CODE=001
* application.properties

@ConditionalOnProperty prefix name 要与application.properties完全一致,在环境变量里面,允许
松散绑定。

### 定位外部化配置属性源

如何理解PropertySource 顺序
* @TestPropertySource#properties
* @SpringBootTest#properties
* @TestPropertySource#locations

* 如何理解PropertySource

带有名称的属性源，Properties 文件、Map、 YAML 文件

* 什么是Environment抽象?
Environment与PropertySources 是1对1， PropertySources 与PropertySource 是1对N

理解Spring Boot Environment生命周期

Spring Framework中,尽量在
`org.springframework.context.support.AbstractApplicationContext#prepareBeanFactory`方法前
初始化。

`Spring Boot中,尽量在org.springframework.boot.SpringApplication#refreshContext(context)`
方法前初始化。
