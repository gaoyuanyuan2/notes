

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




