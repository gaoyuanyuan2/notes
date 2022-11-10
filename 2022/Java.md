# 2022 Java 学习笔记

## Java 7

### 文件系统

* File
* Path

#### ServiceLoader<S> 

* 基于SPI机制来扩展
 * Servlet3.0
 * Java Rest 标准
 * BeanDefinition

## Java 8

### Stream API (JSR 335 )

### CompletableFuture ( J.U.C )

### Annotation on Java Types ( JSR 308 )

### Date and Time API( JSR 310 )

### 可重复 Annotations ( JSR 337 )

@ComponentScan

### JavaScript 运行 ( JSR 223 )

## Java编程模型

### Java面向过程

byte(8) char(16) short(16) int(32) long(64)

#### 泛型设计

 Java泛型属于编译 时处理，运行时擦写。
     
### Java面向切面编程

* Java静态接口
* Java动态代理
 * java.lang.reflect.Proxy
 * java.lang.reflect.InvocationHandler
* 字节码提升
 * ASM ( ObjectWeb )
 * CGLIB
 * Javassist ( JBoss )
 * BCEL ( Apache )

### Java面向元数据编程
    
#### 泛型

泛型设计时啥时候用T ,啥时候用问号?

T有一种类型的概念,通常用T可以用在类型和方法, ?仅用于方法。T存在类型继承性，?就不存在。

#### 反射

Reflection
```java
// 构造器，字段，方法 
java.lang.reflect.Member
// 被标柱的对象，标柱注解 的地方
java.lang.reflect.AnnotatedElement
java.lang.reflect.Executable
java.lang.reflect.Field
java.lang.reflect.Method
java.lang.reflect.Constructor
```

setAccessible(true)
 
`RuntimePermission`可以控制反射入侵

#### 注解

### Java面向函数编程

#### 函数式接口

* 匿名内置类
 * 大多数业务系统属于面向过程的方式，这与面向对象编程在一定程度上存在一些冲突。ava编程语言为了解决这个问题，引入了匿名内置类的方案。

* 典型场景
 * Java Event / Listener
 * Java Concurrent
 * Spring Template
 
* Lambda表达式
 * 实现手段
 * @FunctionalInterface接口
 * Lambda语法  
 * 方法引用
 * 接口default方法实现

SCFP = Supplier + Consumer + Function +  Predicate

Action

#### 默认方法
#### 方法引用

## Java编程思想

### 契约编程

### 设计模式
 
### 模式驱动

## Java设计模式

* 面向对象设计模式
 * 构造模式
 * 结构模式
 * 行为模式
 * 并发模式
* 面向元数据设计模式
 * 泛型接口设计
 * 注解驱动设计
* 面向切面设计模式
 * 判断模式
 * 拦截模式
* 面向函数设计模式
 * 函数式接口 设计( SCFP )
 * Fluent API设计
 * Reactive / Stream API设计
 
## Java 接口设计

* 命名模式
 * 前缀: "Default" 、“Generic" 、“Common” 、“Basic”
 * 后缀:“Impl”  

* 抽象类设计
 * 抽象程度介于类与接口之间(Java 8+可完全由接口代替)
 * 以"Abstract"或"Base”类名前缀
 
* 内置类设计
 * 临时数据存 储类: `java.lang.ThreadLocalThreadLocalMap`
 * 特殊用途的API实现: `java.util.Collections.UnmodifiableCollection`
 * Builder模式(接口) : `java.util.stream.Stream.Builder` 
 
Cloneable接口是一个标记接口，用于表示该类可以克隆。否则抛出  CloneNotSupportedException.
clone比new 更高效

## Java枚举设计

* 枚举实际是final class
* 它的成员修饰符为public static final
* `values（）`是Java编译器做的字节码提升
* 枚举可以使用抽象方法 `TimeUnit`
   
## Java模式驱动

* 接口驱动
 * JavaSE(GoF23模式)
 * Java EE API( Servlet、JSF、 EJB .. )
 * Spring Core API ( interface 21 )

* 配置驱动
 * Java System Properties
 * OS环境变量
 * 文件配置( XML、Properties、 YAML )
 * Java EE配置( JDNI、Servlet、 EJB... )
  
* 注解驱动
 * Java SE ( Java Beans、 JMX .. )
 * Java EE ( Servlet 3.0+、JAX-RS、Bean Validation、EJB 3.0+ ... )
 * Spring ( @Component、@Service、 @Repository ..)
 * Spring Boot ( @SpringBootApplication )
 * Spring Cloud ( @SpringCloudApplication )
  
* 函数驱动
 * Java 8 Stream API
 * Java 9 Flow API
 * RxJava
 * Vert.x
 * Spring Boot WebFlux
 * Spring Cloud Gateway/Function
 
* 模块驱动
 * Java OSGI
 * Java 9 Module
 * Spring @Enable*
 * Spring Boot AutoConfiguration
 * Spring Boot Actuator
   
## Java模块化

* 收益不大，代价不小
* 对团队要求极高,容易出现互喷的情况
* Java 9之前采用jar文件管理, Java 9模块化之后,编程了module-info.java管理,还需要考虑与Maven依赖管理组件如何配合。



## 问答

静态方法没有办法被interface替换,因为interface不允许出现static修饰方法；

子类在初始化时候,会复制一份父类中的数据包括结构；

如果克隆支持的类没有覃盖hashCode方法的话,继承的是Object实现,克隆对象和被
克隆对象的hashCode是不同的,以为两者不是不同的对象, hashCode()方法反应的对
象地址是不同。


字节码提升是通过字节码操作。修改类的定义，达到辅助类一些操作 ，AOP。书籍推荐: Java字节码规范、
深入Java虚拟机关于ClassLoader部分，可以了解一下ASM CGLIB。

## Java泛型设计

### 泛型使用场景
   
* 编译时强类型检查
* 避免类型强转
* 实现通用算法

### 类型参数命名约定

* E:表示集合元素(Element)
* V:表示数值(Value)
* K:表示键(Key)
* T:表示类型

* U：第二个类型
* R：结果

### 泛型有界类型参数

* 单界限
* 多界限
* 泛型方法和有界类型参数

如果是读职泛型数据时,可以运用extends。如果是操作数据,使用super来修饰。

### 问答

如果泛型参数实在属性可以通过字节码的方式获取字符描述 ，然后反推；
如果泛型苏数在类型上面了。那么可以通过反时获取。

## 函数式编程

### 函数式接口类型

* 提供类型- Supplier<T>
* 消费类型- Consumer<T>
* 转换类型- Function<T,R>
* 断定类型- Predicate<T>
* 隐藏类型- Action

`::` 方法引用

是否为并行Stream: Stream#isParallel()