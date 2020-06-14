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

嵌入式容器，无需随Java EE容器启动而装在。

Spring Boot出现嵌入式容器启动方式后，嵌入式容器则成为应用的一部分， 从本质上来说，它属于Spring 应用上下文的组件Beans,
这些组件和其他组件均由自动装配特性组装成Spring Bean 的定义（BeanDefinition），随Spring应用上下文启动而注册并初始化。


### 特征

* 创建独立的Spring应用: 

* 直接嵌入Tomcat、Jetty 或Undertow等Web容器(不需要部署WAR文件);

* 提供固化的 “starter”依赖，简化构建配置;

* 当条件满足时自动地装配Spring或第三方类库;

* 提供运维(Production-Ready) 特性，如指标信息(Metrics)、 健康检查及外部化配置:绝无代码生成，并且不需要XML配置。

## 理解独立的Spring应用

Spring Boot 1.x 中仅有Servlet容器实现；

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
`org.springframework.boot.loader.JarLauncher`会将这些JAR文件作为`com.yan.demo.Application`的库依赖，所以JarLauncher能够
引导反之`com.yan.demo.Application`这不行。

java -java 执行JarLauncher 父类的方法Launcher#launch(String[],String,ClassLoader)

URLStreamHandler 子类

sun.net.www.protocol.file.Handler

sun.net.www.protocol.jar.Handler

sun.net.www.protocol.http.Handler

sun.net.www.protocol.https.Handler

sun.net.www.protocol.ftp.Handler

如需扩展择则需继续URLStreamHandler类


org.springframework.boot.loader.Launcher

ExecutableArchiveLauncher extends Launcher 

WarLauncher extends ExecutableArchiveLauncher

JarLauncher extends ExecutableArchiveLauncher

总而言之，打包WAR文件是一种兼容措施，既能被WarLauncher启动，又能兼容 Servlet容器环境。
换言之，WarLauncher与JarLauncher并无本质差别，所以建议Spring Boot应用使用非传统Weh部署时尽可能地使用JAR归档方式。


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

总而言之，Tomcat Maven插件的版本支持6~8版本，对应的Servlet规范支持2.5~3.1版本。同时，从Servlet 3.0开始， Servlet组件均能
通过ServletContext 
API在运行时装配，如Servlet、Filter和Listener,再结合ServletContainerInitializer生命周期回调，
可实现Servlet组件的自动装配，Spring Framework 3.1同样运用了这些特性，抽象出WebApplicationInitializer接口，
降低ServletContainerInitializer接口的理解成本

spring-boot-starter-web 与spring-boot-starter-webflux同时使用时，webflux会被忽略。


当前应用属于Spring Boot WebFlux 应用，并且使用基于Servlet 技术所构建的UndertowServletWebServer实例作为嵌入式
Reactive Web服务器。

Spring Boot 2.0新引入了一种ApplicationContext实现实现WebServerApplicationContext,
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

### 组合注解

Spring Framework并没有考迪使用Java反射的手段来解析元注解信息，而是抽家出AnnotationMetadata接口，
其实现类为AnnotationMetadataReadingVisitor.并且从Spring Framework 4.0开始，
AnnotationMetadataReadingVisitor所关联的AnnotationMetadataReadingVisitor
采用递归查找元注解，使得多层次元注解信息保存在AnnotationMetadataReadingVisitor的metaAnnotationMap字段中。

SpringFramework的类加教则通过ASM实现如ClassReader. 相对于ClassLoader体系。
SprigASM更为账展，读取的是类资源，直接操作其中的字节码，获取相关元信息，
同时便于Spring相关的字节码提升、在读取元信息方面，Spring 抽象出MetadataReader接口。






