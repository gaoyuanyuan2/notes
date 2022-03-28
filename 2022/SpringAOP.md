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


### 06 | AOP概念：Aspect、Join Point和Advice等术语应该如何理解？

* AOP定义
  AspectJ: Aspect-oriented programming is a way of modularizing crosscutting concerns much like object-oriented programming is a way of modularizing common concerns.
  Spring: Aspect-oriented Programming (AOP) complements Object-oriented Programming (OOP) by providing another way of thinking about program structure. The key unit of modularity in OOP is the class, whereas in AOP the unit of modularity is the aspect. Aspects enable the modularization of concerns (such as transaction management) that cut across multiple types and objects.
* Aspect概念
  * AspectJ: aspect are the unit of modularity for crosscutting concerns. They behave somewhat like Java classes, but may also include pointcuts, advice and inter-type declarations.
  * Spring: A modularization of a concern that cuts across multiple classes.
* Join point 概念
  * AspectJ: A join point is a well- -defined point in the program flow. A pointcut picks out certain join points and values at those points.
  * Spring: A point during the execution of a program, such as the execution of a method or the handling of an exception. In Spring AOP, a join point always represents a method execution.
* Pointcut 概念
  * AspectJ: pointcuts pick out certain join points in the program flow. 
  * Spring: A predicate that matches join points.
  
* Advice 概念
  * AspectJ: So pointcuts pick out join points. But they don't do anything apart from picking out join points. To actually implement crosscutting behavior, we use advice. Advice brings together a pointcut (to pick out join points) and a body of code (to run at each of those join points).
  * Spring: Action taken by an aspect at a particular join point. Different types of advice include "around", before and after" advice. Many AOP frameworks, including Spring, model an advice as an interceptor and maintain a chain of interceptors around the join point.

* Introduction 概念
  * AspectJ: Inter- -type declarations in AspectJ are declarations that cut across classes and their hierarchies. They may declare members that cut across multiple classes, or change the inheritance relationship between classes.
  * Spring: Declaring additional methods or fields on behalf of a type. Spring AOP lets you introduce new interfaces (and a corresponding implementation) to any advised object.

Aspect是一个类似像一个Class一样的，Join point相当于就是一个方法，Action就相当于说这方法里面的具体的步骤


### 07 | Java AOP设计模式：代理、判断和拦截器模式

* 代理模式:静态和动态代理
* 判断模式:类、方法、注解、参数、昇常.
* 拦截模式:前置、后置、返回、昇常

### 08 | Java AOP代理模式（Proxy）：Java静态代理和动态代理的区别是什么？

* Java静态代理
  * 常用OOP继承和组合相结合
  * Java动态代理
* JDK动态代理
  * 字节码提升，如CGLIB

### 09 | Java AOP判断模式（Predicate）：如何筛选Join Point？


* 判断来源
  * 类型(Class)
  * 方法(Method)
  * 注解(Annotation)
  * 参数(Parameter)
  * 异常(Exception)
  
  
### 10 | Java AOP拦截器模式（Interceptor）：拦截执行分别代表什么？

* 拦截类型
  * 前置拦截(Before)
  * 后置拦截(After)
  * 异常拦截(Exception)


### 11 | Spring AOP 功能概述：核心特性、编程模型和使用限制

* 核心特性
  * 纯Java实现、无编译时特殊处理、不修改和控制ClassL oader
  * 仅支持方法级别的Join Points
  * 非完整AOP实现框架
  * Spring loC容器整合
  * AspectJ注解驱动整合(非竞争关系)

### 12 | Spring AOP编程模型：注解驱动、XML配置驱动和底层API

* 注解驱动
  * 实现: Enable 模块驱动，@EnableAspectJAutoProxy
  * 注解:
     * 激活AspectJ自动代理: @EnableAspectJAutoProxy
     * Aspect : @Aspect
     * Pointcut : @Pointcut
     * Advice : @Before @AfterReturning, @After Throwing, @After @Around
     * Introduction : @DeclareParents

* XML配置驱动
  * 实现: Spring Extensble XML Authoring
  * XML元素

### 13 | Spring AOP设计目标：Spring AOP与 AOP框架之间的关系是竞争还是互补？

Spring AOP处理AOP的方法不同于大多数其他AOP框架。这样做的目的是而不是提供最完整的AOP实现(尽管Spring AOP相当强大)。相反，其目的是在AOP实现和Spring loC之间提供一个紧密的集成帮助解决企业应用程序中的常见问题。

Spring AOP从不努力与AspectJ竞争，以提供一个全面的AOP解决方案。我们相信，无论是基于代理的框架，如Spring AOP，还是成熟的框架。例如AspectJ是有价值的，它们是互补的，而不是竞争的。Spring将Spring AOP和loC与AspectJ无缝集成，使AOP的所有使用都能在一致的基于spring的应用程序体系结构。这种集成不会影响Spring AOP API或AOP联盟API。Spring AOP保持向后兼容。一个是通过Java动态代理，一个是通过像字节码提升，通过Aspectj整合。

### 14 | Spring AOP Advice类型：Spring AOP丰富了哪些AOP Advice呢？

* Advice类型
  * 环绕(Around)
  * 前置（Before）
  * 后置(After) 
    * 方法执行
    * finally执行
  * 异常(Exception)


### 15 | Spring AOP代理实现：为什么Spring Framework选择三种不同AOP实现？

* JDK动态代理实现-基于接口代理
* CGLIB动态代理实现-基于类代理(字节码提升)
* AspectJ适配实现

通常会选择AspectJ的注解驱动或者AspectJ所对应的XML的Schema-Base实现

### 16 | JDK动态代理：为什么Proxy.newProxyInstance会生成新的字节码？



### 17 | CGLIB动态代理：为什么Java动态代理无法满足AOP的需要？

尽管我们推崇面向对象编程，本质主要是面向接口编程，也可以认为它是面向契约编程，用户不需要关注具体实现。
Java毕竟是以类为主导的，这个类也包含了我们的接口，抽象类，以及具体实现类，无法避免开发人员不写接口注解写类的情况。
这个时候我们就需要通过一些字节码提升的手段，帮助我们来做这个事情，所以需要运行时来创建新的Class，这种方式称之为字节码提升。

有性能损失

### 18 | AspectJ代理代理：为什么Spring推荐AspectJ注解？

简化使用

### 19 | AspectJ基础：Aspect、Join Points、Pointcuts和Advice语法和特性

* AspectJ 语法
  * Aspect
  * Join Points
  * Pointcuts
  * Advice
  * Introduction

### 20 | AspectJ注解驱动：注解能完全替代AspectJ语言吗？

* AspectJ 注解
  * 激活AspectJ自动代理: @EnableAspectJAutoProxy
  * Aspect : @Aspect
  * Pointcut : @Pointcut
  * Advice : @Before @AfterReturning @After Throwing @After @Around
  * Introduction : @DeclareParents

### 21 | 面试题精选

* 问: Spring AOP和AspectJ AOP存在哪些区别?

答:
* AspectJ是AOP完整实现，Spring AOP则是部分实现
* Spring AOP比AspectJ使用更简单
* Spring AOP整合AspectJ注解与Spring IoC容器
* Spring AOP仅支持基于代理模式的AOP
* Spring AOP仅支持方法级别的Pointcuts

## 第二章：Spring AOP基础 (20讲)

### 22 | Spring核心基础：《小马哥讲Spring核心编程思想》还记得多少？

### 23 | @AspectJ注解驱动

* @AspectJ注解驱动
  * 激活@AspectJ模块
  * 注解激活- @EnableAspectJAutoProxy
  * XML配置- <aop:aspectj-autoproxy/>
* 声明Aspect
  * @Aspect



### 24 | 编程方式创建 @AspectJ代理

* 实现类
  * org.springframework.aop.aspectj.annotation.AspectJProxyFactory

### 25 | XML配置驱动 – 创建AOP代理

* 实现方法
  * 配置org.springframework.aop.framework.ProxyFactoryBean
  * Spring Schema- Based配置
    * <aop:config>
    * <aop:aspectj-autoproxy/>

### 26 | 标准代理工厂API – ProxyFactory

* 实现类- org.springframework.aop.framework.ProxyFactory


### 27 | @AspectJ Pointcut指令与表达式：为什么Spring只能有限支持？



###  28 | XML配置Pointcut

* XML配置
  * <aop:pointcut />
                
### 29 | API实现Pointcut

### 30 | @AspectJ拦截动作：@Around与@Pointcut有区别吗？

* 注解- @Around
  * 与@Pointcut有什么区别?

* 核心API  - org.springframework.aop.Pointcut
  * org.springframework.aop.ClassFilter
  * org.springframework.aop.MethodMatcher
* 适配实现 - DеfаultРоіntсutАdvіѕоr


Around 和Before 区别在于Before它不需要去显式去触发方法，Around需要去触发目标方法执行

### 31 | XML配置Around Advice

* XML 配置
  * <aop:around />

### 32 | API实现Around Advice

思考： 为什么 Spring AOP 不需要设计 Around Advice？
* 线索
  * AspectJ @Around 与 org.aspectj.lang.ProceedingJoinPoint 配合执行被代理方法
  * ProceedingJoinPoint#proceed() 方法类似于 Java Method#invoke(Object,Object...)
  * Spring AOP 底层 API ProxyFactory 可通过 addAdvice 方法与 Advice 实现关联
  * 接口 Advice 是 Interceptor 的父亲接口， 而接口 MethodInterceptor 又扩展了 Interceptor
  * MethodInterceptor 的invoke 方法参数 MethodInvocation 与 ProceedingJoinPoint 类似

### 33 | @AspectJ前置动作：@Before与@Around谁优先级执行？

Around和Before执行的顺序是没有绝对的，只不过在同一个Aspect里面它Around会优先于Before，具体还是通过Ordered来进行操作。

### 34 | XML配置Before Advice

* XML 元素 - <aop:before>
  * 声明规则
  * <aop:config>
  * <aop:aspect>
  * <aop:before>
  * 属性设置（ 来源于 Spring AOP Schema 类型 basicAdviceType）
  * pointcut： Pointcut 表达式内容
  * pointcut-ref： Pointcut 表达式名称

### 35 | API实现Before Advice

* 核心接口 - org.springframework.aop.BeforeAdvice
* 类型： 标记接口， 与 org.aopalliance.aop.Advice 类似
  * 方法 JoinPoint 扩展 - org.springframework.aop.MethodBeforeAdvice
  * 接受对象 - org.springframework.aop.framework.AdvisedSupport
    * 基础实现类 - org.springframework.aop.framework.ProxyCreatorSupport
      * 常见实现类
        * org.springframework.aop.framework.ProxyFactory
        * org.springframework.aop.framework.ProxyFactoryBean
        * org.springframework.aop.aspectj.annotation.AspectJProxyFactory

### 36 | @AspectJ后置动作 – 三种After Advice之间的关系？

* After Advice 注解
  * 方法返回后： @org.aspectj.lang.annotation.AfterReturning
  * 异常发生后： @org.aspectj.lang.annotation.AfterThrowing
  * finally 执行： @org.aspectj.lang.annotation.After

### 37 | XML配置三种After Advice

* XML 元素 - <aop:after>
  * 声明规则
    * <aop:config>
      * <aop:aspect>
        * <aop:after>
  * 属性设置（ 来源于 Spring AOP Schema 类型 basicAdviceType）
    * pointcut： Pointcut 表达式内容
    * pointcut-ref： Pointcut 表达式名称

### 38 | API实现三种After Advice

* 核心接口 - org.springframework.aop.AfterAdvice
  * 类型： 标记接口， 与 org.aopalliance.aop.Advice 类似
  * 扩展
    * org.springframework.aop.AfterReturningAdvice
    * org.springframework.aop.ThrowsAdvice
  * 接受对象 - org.springframework.aop.framework.AdvisedSupport
    * 基础实现类 - org.springframework.aop.framework.ProxyCreatorSupport
      * 常见实现类
        * org.springframework.aop.framework.ProxyFactory
        * org.springframework.aop.framework.ProxyFactoryBean
        * org.springframework.aop.aspectj.annotation.AspectJProxyFactory

### 39 | 自动动态代理

* 代表实现
  * org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator
  * org.springframework.aop.framework.autoproxy.DefaultAdvisorAutoProxyCreator
  * org.springframework.aop.aspectj.annotation.AnnotationAwareAspectJAutoProxyCreator

### 40 | 替换TargetSource

* 代表实现
  * org.springframework.aop.target.HotSwappableTargetSource
  * org.springframework.aop.target.AbstractPoolingTargetSource
  * org.springframework.aop.target.PrototypeTargetSource
  * org.springframework.aop.target.ThreadLocalTargetSource
  * org.springframework.aop.target.SingletonTargetSource

### 41 | 面试题精选

沙雕面试题 - Spring AOP 支持哪些类型的 Advice？

答：
* Around Advice
* Before Advice
* After Advice
  * After
  * AfterReturning
  * AfterThrowing

996 面试题 - Spring AOP 编程模型有哪些， 代表组件有哪些？
答：
* 注解驱动： 解释和整合 AspectJ 注解， 如 @EnableAspectJAutoProxy
* XML 配置： AOP 与 IoC Schema-Based 相结合
* API 编程： 如 Joinpoint、 Pointcut、 Advice 和 ProxyFactory 等

劝退面试题 - Spring AOP 三种实现方式是如何设计的?

## 第三章：Spring AOP API设计与实现 (49讲)

### 42 | Spring AOP API整体设计

* Join point - Joinpoint
* Pointcut - Pointcut
* Advice 执行动作 - Advice
* Advice 容器 - Advisor
* Introduction - IntroductionInfo
* 代理对象创建基础类 - ProxyCreatorSupport
* 代理工厂 - ProxyFactory、 ProxyFactoryBean
* AopProxyFactory 配置管理器 - AdvisedSupport
* IoC 容器自动代理抽象 - AbstractAutoProxyCreator

### 43 | 接入点接口 – Joinpoint

* Interceptor 执行上下文 - Invocation
  * 方法拦截器执行上下文 - MethodInvocation
  * 构造器拦截器执行上下文 - ConstructorInvocation
* MethodInvocation 实现
  * 基于反射 - ReflectiveMethodInvocation
  * 基于 CGLIB - CglibMethodInvocation

### 44 | Joinpoint条件接口 – Pointcut

* 核心组件
  * 类过滤器 - ClassFilter
  * 方法匹配器 - MethodMatcher

### 45 | Pointcut操作 – ComposablePointcut

* 组合实现 - org.springframework.aop.support.ComposablePointcut
* 工具类
  * ClassFilter 工具类 - ClassFilters
  * MethodMatcher 工具类 - MethodMatchers
  * Pointcut 工具类 - Pointcuts


### 46 | Pointcut便利实现

* 静态 Pointcut - StaticMethodMatcherPointcut
* 正则表达式 Pointcut - JdkRegexpMethodPointcut
* 控制流 Pointcut - ControlFlowPointcut

### 47 | Pointcut AspectJ实现 – AspectJExpressionPointcut

* 实现类 - org.springframework.aop.aspectj.AspectJExpressionPointcut
* 指令支持 - SUPPORTED_PRIMITIVES 字段
* 表达式 - org.aspectj.weaver.tools.PointcutExpression

### 48 | Joinpoint执行动作接口 – Advice

*  Around Advice - Interceptor
  *  方法拦截器 - MethodInterceptor
  *  构造器拦截器 - ConstructorInterceptor
*  前置动作
  *  标准接口 - org.springframework.aop.BeforeAdvice
  *  方法级别 - org.springframework.aop.MethodBeforeAdvice
*  后置动作
  *  org.springframework.aop.AfterAdvice
  *  org.springframework.aop.AfterReturningAdvice
  *  org.springframework.aop.ThrowsAdvice

### 49 | Joinpoint Before Advice标准实现

* 接口
  *  标准接口 - org.springframework.aop.BeforeAdvice
  *  方法级别 - org.springframework.aop.MethodBeforeAdvice
* 实现
  *  org.springframework.aop.framework.adapter.MethodBeforeAdviceInterceptor

### 50 | Joinpoint Before Advice AspectJ实现

* 实现类 - org.springframework.aop.aspectj.AspectJMethodBeforeAdvice

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



