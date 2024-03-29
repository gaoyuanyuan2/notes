# 2022 Java 学习笔记

## Java 7

### 文件系统

*  
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

## 集合

()[https://www.digitalocean.com/community/tutorials/java-collections-interview-questions-and-answers!]


## 线程

* Java 线程编程模型
 * < Java 5：Thread、Runnable
 * Java 5：Executor、Future、Callable
 * Java 7：ForkJoin
 * Java 8：CompletionStage、CompletableFuture
 * Java 9：Flow（Publisher、Subscriber、Subscription、Processor）


* Java 并发框架
 * Java 5：Java Util Concurrent
 * Java 7：Fork/Join
 * Java 8：CompletableFuture、RxJava、Reactor
 * Java 9：Flow API、Reactive Streams

### Java 线程状态

* API - java.lang.Thread.State（Since 1.5）  * NEW：线程已创建 ，尚未启动
 * RUNNABLE：表示线程处于可运⾏状态，不代表⼀定运⾏
 * BLOCKED：被 Monitor 锁阻塞，表示当前线程在同步锁的场景运作
 * WAITTING：线程处于等待状态，由 Object#wait()、Thread#join() 或 LockSupport#park() 引起
 * TIMED_WAITTING：线程处于规定时间内的等待状态
 * TERMINATED：线程执⾏结束


### synchronized 和volatile

synchronized 和volatile 都有锁，但是它们的范围不同，笼统而言。前者锁定一段代码，后者锁定的是变量。

### synchronized
 
synchronized原语是没有读写锁实现，有可能操作系统会实现。但是Java API。ReentrantReadWriteLock对于应用是透明，不依赖于底层实现。

### Thread 和 Object

Thread.suspend() 和 Thread.resume() 方法可以运用任意区域 suspend()：指定线程挂起，resume()：指定线程恢复

Object.wait() 和 Object.notify() 只能用在 synchronized 方法或块通过对象 Monitor 控制线程状态

Object#wait获得的对象 ,释放锁,当前线程又被阻塞
LockSupport#park() 类似

Object#notify 已经获得锁,唤起一个被阻塞的线程
LockSupport#unpark() 类似

join()

Thread#interrupt() 
并不能中止线程，但是可以传递 interrupt 状态
thread.interrupt() 方法在 start() 调用之前是没有效果
调用 wait /join / sleep 抛出InterruptedException异常， 当前 interrupted 状态被清除 == false

Thread#isInterrupted() 不清除
Thread#isInterrupted(true) 清除

Object.wait() 与 Thread.join() 看起来效果类似
实际上 Thread.join() 方法就是调用了 Thread 对象 wait(int) 方法

### 偏向锁

大多数对象在同一个线程中使用，使用偏向锁可以减少开销，第一次获取锁才有cas操作，轻量级锁。多线程使用同一个对象，会升级为重量级锁。

偏向锁是Java 6幵始默人激活,使得synchronized 吾乂与ReentrantLock是性能接近,在Java 5时候，ReentrantLock > synchronized

CAS 是一种相对（MB）较重的比较，轻量级的锁（标量）

同一个线程，不需要锁对象

### Queue

BlockingQueue 尽可能用 put，避免使用 offer，最好不要用 add。

## Java 内存模型

Memory that can be shared between threads is called shared memory or heap memory.

All instance fields, static fields, and array elements are stored in heap memory.

广义的锁和同步或互斥是相同的语义,只不过 狭义的锁是对临界区(代码)互斥,那么 volatile或者CAS操作是对单个变量互斥的。 

如果一个程序没有数据竞争，那么该程序的所有执行都将出现顺序一致。

## 问答

### 有哪些方法创建线程? 

只有Thread一种，Runnable是运行的一种方式。

### 如何销毁一个线程? 

Java 中执行线程Java 是没有办法销毁它的，
但是当Thread.isAlive() 返回false 时，实际底层的Thread 已经被销毁了

stop 可能导致正在锁的对象解锁， 可能导致状态不一致死锁

### Thread interrupt()/ isInterrupted() 以及 interrupted()的区别以及意义?  

interrupt() 设置状态
isInterrupted() 判断状态不清除
interrupted() 判断状态清除状态 

### 线程异常 

线程终止

### Java线程有哪些状态,分别代表什么含义?


### 如何获取当前JVM所有的线程状态?

jps

jstack

### 如何获取线程的资源消费情况?

### 请说明synchronized关键字与ReentrantLock之间的区别?

### 请解释偏向锁对synchronized与ReentrantLock 的价值?

偏向锁对synchronized 有影响，对ReentrantLock无影响

### 当主线程退出时，守候子线程会执行完毕吗?

不一定
 
### 请说明Shutdown Hook线程的使用场景,以及如何触发执行?

### 如何确保在主线程退出前,所有线程执行完毕?

### 请在Java集合框架以及J.U.C框架中各举出List、 Set以及Map的实现?

### 如何将普通List、 Set以及Map转化为线程安全对象?

### 如何在Java 9+实现以上问题?

### 请说明List、 Vector 以及CopyOnWriteArrayList的相同点和不同点?

Vector List实现，同步，iterator：fail-fast

CopyOnWriteArrayList List实现，读不加锁，写加锁 ，iterator：弱一致性的实现，不报错。

### 请说明Collections#synchronizedList(List) 与Vector的相同点和不同点?

相同点：都是synchronized 
不同点：一个是包装了

### Arrays#asList(Object...)方法是线程安全的吗?如果不是的话,如何实现替代方案?

Java < 5 , Collections#synchronizedList
Java 5+ , CopyOnWriteArrayList
Java 9+ List.of(...) 只读

### 请至少举出三种线程安全的Set实现?

SynchronizedSet
CopyOnWriteArraySet
ConcurrentSkipListSet

### 在J.U.C框架中,存在HashSet的线程安全实现?如果不存在的话,要如何实现?

### 当Set#iterator() 方法返回Iterator对象后,能否在其迭代中,给Set对象添加新的元素?

不一定，传统实现的确是，juc是弱一致性

### 请说明Hashtable、HashMap 以及ConcurrentHashMap的区别

Hashtable k v 不能为空
HashMap k v 都不能为空
ConcurrentHashMap  k v 不能为空

### 请说明ConcurrentHashMap在不同的JDK中的实现?

6 分离锁，读部分锁，写完全锁；7 读不要锁，写要锁； 8 读不要锁，写要锁 ，红黑树

### 请说明ConcurrentHashMap与ConcurrentSkipListMap各自的优势与不足?

ConcurrentSkipListMap 写不加锁，内存大，空间换时间，读写稳定 log n

### 请说明BlockingQueue与Queue的区别?

put 队列满了，put被阻塞

### 请说明LinkedBlockingQueue与ArrayBlockingQueue的区别?

一个链表，一个数组
一个无边界，一个有边界

### 请说明LinkedTransferQueue与LinkedBlockingQueue的区别?

LinkedTransferQueue java7提供，性能更高

### 请说明 ReentrantLock 与 ReentrantReadWriteLock 的区别？

ReentrantLock 互斥

ReentrantReadWriteLock 写互斥，读共享 


### 请说明 Lock#lock() 与 Lock#lockInterruptibly() 的区别？ 

### 请解释 ReentrantLock 为什么命名为重进入？

### ReentrantLockQuestion

抛出InterruptedException状态会被清除


### 请举例说明 Condition 使用场景？ 

CyclicBarrier
CountDownLatch
阻塞队列

### 请使用 Condition 实现“生产者-消费者问题”？

### 请解释 Condition await() 和 signal() 与 Object wait() 和 notify() 的相同与差异？ 

### CountDownLatch 与 CyclicBarrier 的区别？

### Java 1.4 的语法实现一个 CountDownLatch ？

### Semaphore 的使用场景？

### 请问 J.U.C 中内建了几种 ExecutorSer vi ce 实现？

### 请分别解释 ThreadPoolExecutor 构造器参数在运行时的作用？

### 如何获取ThreadPoolExecutor 正在运行的线程？

### 如何获取 Future 对象？

### 请举例 Future get() 以及 get(long,TimeUnit) 方法的使用场景？

### 如何利用Future 优雅地取消一个任务的执行？

### 在 Java 中，volatile 保证的是可见性还是原子性？

### 在 Java 中，volatile 的底层实现是基于什么机制？

### 在 Java 中，volatile long 和 double 是线程安全的吗？

### 为什么 AtomicBoolean 内部变量使用 int 实现，而非 boolean？

### 在变量原子操作时，Atomic* CAS 操作比 synchronized 关键字那个更重？

### Atomic* CAS 的底层是如何实现的？









