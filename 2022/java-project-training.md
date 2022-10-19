# Java项目实战

## 第一章    Java EE

### 第一节 Servlet

#### Servlet 是否线程安全

不仅是同步，而且可是是异步，不仅可能线程安全，有可能非线程安全。规范里面有说明。

#### NIO在Web体系不一定有多大提升

#### flushBuffer 读取文件写入缓冲区，然后刷新，防止内存溢出

####  GenericServlet implements  Serializable

可能把状态持久化到本地，重启重新初始化状态

#### jsp性能较高，默认打包编译成 Servlet class文件

development 模式，动态编译生产Servlet

#### Servlet 处理静态内容

Tomcat ：org.apache.catalina.servlets.DefaultServlet

#### Java打包文件
  
基本通过jar命令或者相关实现类完成，类似于ZIP
JAR: Java 归档文件
WAR: Java Web归档文件
EAR: Java 企业级归档文件
FAT JAR:压缩率为0的JAR文件，-0仅存储;不使用任何ZIP压缩，扩展了URL协议

### 第二节 数据存储之 JDBC

#### 多数据库源（Multiple DataSources）

* N 个 DataSources
* DataSource 代理
  * Druid
  
#### JDBC 核心 API 

* 数据源接口 - javax.sql.DataSource 
* JDBC 驱动接口 - java.sql.Driver 
* 驱动管理器接口 - java.sql.DriverManager 
* 数据连接接口 - java.sql.Connection 
* SQL 命令接口 - java.sql.Statement 
* SQL 执行结果接口 - java.sql.ResultSet 
* ResultSet 元数据接口 - java.sql.ResultSetMetaData 
* SQL 执行异常 - java.sql.SQLException 
* 事务保护点接口 - java.sql.Savepoint


### MQTT大势所趋 

### 只能获取一次

getInputStream()
getReader()

### JAX-RS

JAX-RS是JAVA EE6 引入的一个新技术。 JAX-RS即Java API for RESTful Web Services，是一个Java 编程语言的应用程序接口，支持按照表述性状态转移（REST）架构风格创建Web服务。JAX-RS使用了Java SE5引入的Java注解来简化Web服务的客户端和服务端的开发和部署。


### 获取 Driver 实现

前提：数据库驱动 Driver 实现会显示地调用
java.sql.DriverManager#registerDriver 方法

* 通过 ClassLoader 加载 Drvier 实现（用户/应用控制）
* 通过 Java SPI ServiceLoader 获取 Driver 实现加载顺序与 Class Path 的顺序有关系
* 通过 “jdbc.drivers” 系统属性

加载顺序和属性值的顺序有关系
通过读取“jdbc.drivers” 系统属性后，再经过 ":" 的分割，尝试获取多值，再通过 ClassLoader 加载对应的实现类

ServiceLoader 会初始化 Driver 实现类（应用主动配置），包含 Class 加载。

### 获取 Connection

通过 ClassLoader 类加载数据库 JDBC Driver 实现类的方式，增加 java.sql.DriverManager#registeredDrivers 字段的元素，然后通过迭代的方式逐一 尝试 getConnection 方法参数的 JDBC URL 是否可用。

### 问题集合

* 当多个 Driver 同时被加载到 ClassLoader 后，到底用了哪个？

getConnection 方法是通过 JDBC URL 判断的，通过迭代多次，返回第一个成功的 Connection 实例

* java.sql.DriverManager#loadInitialDrivers 方法中 Java SPI 空便利的意义在哪里？
  ```java
  
                try{
                    while(driversIterator.hasNext()) {
                        driversIterator.next();
                    }
                } catch(Throwable t) {
                // Do nothing
                }
  ```
ServiceLoader#next() 方法会主动触发 ClassLoader 加载。

### 多数据库源（Multiple DataSources）

* N 个 DataSources
* DataSource 代理

### 消息

Subscription是Subscriber对Publisher控制对象，也可以称之为"背压控制器"


# 问题

JNDI 

SPI

反射

注解

Spring 常用的模式

泛型

文件流，http
