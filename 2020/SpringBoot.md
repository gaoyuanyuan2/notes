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



### 启动器




