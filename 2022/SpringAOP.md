# Spring AOP编程思想

## 第一章：Spring AOP总览 (21讲)

### 01 | 课程介绍

Spring AOP在Spring Framework中启到至关重要的作用，它即是面向对象设计和面向切面设计的纽带，也是连接Spring IoC容器和AOP编程模型的桥梁，Spring AOP与Spring IoC相辅相成，共同衍生出庞大的Spring生态。

Spring Framework有诸多的特性与Spring AOP密切相关，比如Spring事务、Spring数据、Spring缓存抽象等等

无侵入性的运行时日志、数据监控、安全防护等

### 02 | 内容综述

### 03 | 知识储备：基础、基础，还是基础！

* Java基础
  * Java Classloading
  * Java动态代理
  * Java反射
  * 字节码框架: ASM、CGLIB

* OOP概念
  * 封装
  * 继承
  * 多态
  
* GoF23设计模式
  * 创建模式(Creational patterns)
    * 抽象工厂模式(Abstract factory)
    * 构建器模式(Builder)
    * 工厂方法模式(Factory method)
    * 原型模式(Prototype)
    * 单利模式(Singleton)
  * 结构模式(Structural patterns)
    * 适配器模式(Adapter)
    * 桥接模式(Bridge)
    * 组合模式(Composite)
    * 装饰器模式(Decorator)
    * 门面模式(Facade)
    * 享元模式(Flyweight)
    * 代理模式(Proxy) 
  * 行为模式(Behavioral patterns)
    * 模板方法模式(Template Method)
    * 中继器模式(Mediator)
    * 责任链模式(Chain of Responsibility)
    * 观察者模式(Observer)
    * 策略模式(Strategy)
    * 命令模式(Command)
    * 状态模式(State)
    * 访问者模式(Visitor)
    * 解释器模式(Interpreter)、 迭代器模式 (Iterator)、 备忘录模式(Memento)

* Spring核心基础
  * Spring IoC容器
  * Spring Bean生命周期(Bean Lifecycle)
  * Spring配置元信息(Configuration Metadata)
  * Spring事件(Events)
  * Spring注解(Annotations)

  

### 04 | AOP引入：OOP存在哪些局限性？

* Java OOP存在哪些局限性?
  * 静态化语言:类结构一旦定义，不容易被修改
  * 侵入性扩展:通过继承和组合组织新的类结构
  
  

### 05 | AOP常见使用场景

* 日志场景
  * 诊断上下文，如: log4j或logback中的MDC
  * 辅助信息，如:方法执行时间
  
* 统计场景
  * 方法调用次数
  * 执行异常次数
  * 数据抽样
  * 数值累加

* 安防场景
  * 熔断，如: Netflix Hystrix
  * 限流和降级:如: Alibaba Sentinel
  * 认证和授权，如: Spring Security
  * 监控,如: JMX

* 性能场景
  * 缓存，如Spring Cache
  * 超时控制


06 | AOP概念：Aspect、Join Point和Advice等术语应该如何理解？
07 | Java AOP设计模式：代理、判断和拦截器模式
08 | Java AOP代理模式（Proxy）：Java静态代理和动态代理的区别是什么？
09 | Java AOP判断模式（Predicate）：如何筛选Join Point？
10 | Java AOP拦截器模式（Interceptor）：拦截执行分别代表什么？
11 | Spring AOP 功能概述：核心特性、编程模型和使用限制
12 | Spring AOP编程模型：注解驱动、XML配置驱动和底层API
13 | Spring AOP设计目标：Spring AOP与 AOP框架之间的关系是竞争还是互补？
14 | Spring AOP Advice类型：Spring AOP丰富了哪些AOP Advice呢？
15 | Spring AOP代理实现：为什么Spring Framework选择三种不同AOP实现？
16 | JDK动态代理：为什么Proxy.newProxyInstance会生成新的字节码？
17 | CGLIB动态代理：为什么Java动态代理无法满足AOP的需要？
18 | AspectJ代理代理：为什么Spring推荐AspectJ注解？
19 | AspectJ基础：Aspect、Join Points、Pointcuts和Advice语法和特性
20 | AspectJ注解驱动：注解能完全替代AspectJ语言吗？
21 | 面试题精选
第二章：Spring AOP基础 (20讲)
22 | Spring核心基础：《小马哥讲Spring核心编程思想》还记得多少？
23 | @AspectJ注解驱动
24 | 编程方式创建 @AspectJ代理
25 | XML配置驱动 – 创建AOP代理
26 | 标准代理工厂API – ProxyFactory
27 | @AspectJ Pointcut指令与表达式：为什么Spring只能有限支持？
28 | XML配置Pointcut
29 | API实现Pointcut
30 | @AspectJ拦截动作：@Around与@Pointcut有区别吗？
31 | XML配置Around Advice
32 | API实现Around Advice
33 | @AspectJ前置动作：@Before与@Around谁优先级执行？
34 | XML配置Before Advice
35 | API实现Before Advice
36 | @AspectJ后置动作 – 三种After Advice之间的关系？
37 | XML配置三种After Advice
38 | API实现三种After Advice
39 | 自动动态代理
40 | 替换TargetSource
41 | 面试题精选
第三章：Spring AOP API设计与实现 (49讲)
42 | Spring AOP API整体设计
43 | 接入点接口 – Joinpoint
44 | Joinpoint条件接口 – Pointcut
45 | Pointcut操作 – ComposablePointcut
46 | Pointcut便利实现
47 | Pointcut AspectJ实现 – AspectJExpressionPointcut
48 | Joinpoint执行动作接口 – Advice
49 | Joinpoint Before Advice标准实现
50 | Joinpoint Before Advice AspectJ实现
51 | Joinpoint After Advice标准实现
52 | Joinpoint After Advice AspectJ实现
53 | Advice容器接口 – Advisor
54 | Pointcut与Advice连接器 – PointcutAdvisor
55 | Introduction与Advice连接器 – IntroductionAdvisor
56 | Advisor的Interceptor适配器 – AdvisorAdapter
57 | AdvisorAdapter实现
58 | AOP代理接口 – AopProxy
59 | AopProxy工厂接口与实现
60 | JDK AopProxy实现 – JdkDynamicAopProxy
61 | CGLIB AopProxy实现 – CglibAopProxy
62 | AopProxyFactory配置管理器 – AdvisedSupport
63 | Advisor链工厂接口与实现 – AdvisorChainFactory
64 | 目标对象来源接口与实现 – TargetSource
65 | 代理对象创建基础类 – ProxyCreatorSupport
66 | AdvisedSupport事件监听器 – AdvisedSupportListener
67 | ProxyCreatorSupport标准实现 – ProxyFactory
68 | ProxyCreatorSupport IoC容器实现 – ProxyFactoryBean
69 | ProxyCreatorSupport AspectJ实现 – AspectJProxyFactory
70 | IoC容器自动代理抽象 – AbstractAutoProxyCreator
71 | IoC容器自动代理标准实现
72 | IoC容器自动代理 AspectJ 实现 – AspectJAwareAdvisorAutoProxyCreator
73 | AOP Infrastructure Bean接口 – AopInfrastructureBean
74 | AOP上下文辅助类 – AopContext
75 | 代理工厂工具类 – AopProxyUtils
76 | AOP工具类 – AopUtils
77 | AspectJ Enable模块驱动实现 – @EnableAspectJAutoProxy
78 | AspectJ XML配置驱动实现 –
79 | AOP配置Schema-based 实现 –
80 | Aspect Schema-based实现 –
81 | Pointcut Schema-based实现 –
82 | Around Advice Schema-based实现 –
83 | Before Advice Schema-based实现 –
84 | After Advice Schema-based实现 –
85 | After Returning Advice Schema-based实现 –
86 | After Throwing Advice Schema-based实现 –
87 | Adviser Schema-based实现 –
88 | Introduction Schema-based实现 –
89 | 作用域代理Schema-based实现 –
90 | 面试题精选
第四章：Spring AOP设计模式 (17讲)
91 | 抽象工厂模式（Abstract factory）实现
92 | 构建器模式（Builder）实现
93 | 工厂方法模式（Factory method）实现
94 | 原型模式（Prototype）实现
95 | 单例模式（Singleton）实现
96 | 适配器模式（Adapter）实现
97 | 组合模式（Composite）实现
98 | 装饰器模式（Decorator）实现
99 | 享元模式（Flyweight）实现
100 | 代理模式（Proxy）实现
101 | 模板方法模式（Template Method）实现
102 | 责任链模式（Chain of Responsibility）实现
103 | 观察者模式（Observer）实现
104 | 策略模式（Strategy）实现
105 | 命令模式（Command）实现
106 | 状态模式（State）实现
107 | 面试题精选
第五章：Spring AOP在Spring Framework内部应用 (7讲)
108 | Spring AOP在 Spring 事件（Events）
109 | Spring AOP在Spring 事务（Transactions）理论基础
110 | Spring AOP在Spring 事务（Transactions）源码分析
111 | Spring AOP在Spring 缓存（Caching）
112 | Spring AOP在Spring本地调度（Scheduling）
113 | 面试题精选
114 | 结束语



