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

### 51 | Joinpoint After Advice标准实现

* 接口
  * org.springframework.aop.AfterAdvice
  * org.springframework.aop.AfterReturningAdvice
  * org.springframework.aop.ThrowsAdvice
* 实现
  * org.springframework.aop.framework.adapter.ThrowsAdviceInterceptor
  * org.springframework.aop.framework.adapter.AfterReturningAdviceInterceptor

### 52 | Joinpoint After Advice AspectJ实现

* 接口
  * org.springframework.aop.AfterAdvice
  * org.springframework.aop.AfterReturningAdvice
  * org.springframework.aop.ThrowsAdvice
* 实现
  * org.springframework.aop.aspectj.AspectJAfterAdvice
  * org.springframework.aop.aspectj.AspectJAfterReturningAdvice
  * org.springframework.aop.aspectj.AspectJAfterThrowingAdvice

Aspect的实现，AfterAdvice的实现，最重要还是核心API AbstractAspectjAdvice，这个实现里面有个方法可以查询对应的AdviceMethod。
这个查询的能力是来自于Aspect，Spring只是利用AspectJ，利用它Pointcut表达式的方式来定位到相关的方法，然后通过方法参数的方式来进行调用。
简而言之，AspectJ在Spring里面的实现，它是采用了反射的方式来进行定位的。

### 53 | Advice容器接口 – Advisor

* 接口 - org.springframework.aop.Advisor
  * 通用实现 - org.springframework.aop.support.DefaultPointcutAdvisor

Advice和Advisor之间是一-对一的关系，Spring在我们说传输或者传递Advice的时候，它实际上都是通过Advisor的方式。

### 54 | Pointcut与Advice连接器 – PointcutAdvisor

* 接口 - org.springframework.aop.PointcutAdvisor
  * 通用实现
    * org.springframework.aop.support.DefaultPointcutAdvisor
  * AspectJ 实现
    * org.springframework.aop.aspectj.AspectJExpressionPointcutAdvisor
    * org.springframework.aop.aspectj.AspectJPointcutAdvisor
  * 静态方法实现
    * org.springframework.aop.support.StaticMethodMatcherPointcutAdvisor
    * IoC 容器实现
    * org.springframework.aop.support.AbstractBeanFactoryPointcutAdvisor

### 55 | Introduction与Advice连接器 – IntroductionAdvisor

* 接口 - org.springframework.aop.IntroductionAdvisor
  * 元信息
    * org.springframework.aop.IntroductionInfo
      * 动态地来管理当前代理对象它实现的接口
  * 通用实现
    * org.springframework.aop.support.DefaultIntroductionAdvisor
  * AspectJ 实现
    * org.springframework.aop.aspectj.DeclareParentsAdvisor

### 56 | Advisor的Interceptor适配器 – AdvisorAdapter

* 接口 - org.springframework.aop.framework.adapter.AdvisorAdapter
  * MethodBeforeAdvice 实现
    * org.springframework.aop.framework.adapter.MethodBeforeAdviceAdapter
  * AfterReturningAdvice 实现
    * org.springframework.aop.framework.adapter.AfterReturningAdviceAdapter
  * ThrowsAdvice 实现
    * org.springframework.aop.framework.adapter.ThrowsAdviceAdapter
  
### 57 | AdvisorAdapter实现

* MethodBeforeAdvice 实现
  * org.springframework.aop.framework.adapter.MethodBeforeAdviceAdapter
* AfterReturningAdvice 实现
  * org.springframework.aop.framework.adapter.AfterReturningAdviceAdapter
* ThrowsAdvice 实现
  * org.springframework.aop.framework.adapter.ThrowsAdviceAdapter

### 58 | AOP代理接口 – AopProxy

* 接口 - org.springframework.aop.framework.AopProxy
* 实现
  * JDK 动态代理
    * org.springframework.aop.framework.JdkDynamicAopProxy
  * CGLIB 字节码提升
    * org.springframework.aop.framework.CglibAopProxy
      * org.springframework.aop.framework.ObjenesisCglibAopProxy

### 59 | AopProxy工厂接口与实现

* 接口 - org.springframework.aop.framework.AopProxyFactory
* 默认实现： org.springframework.aop.framework.DefaultAopProxyFactory
  * 返回类型
    * org.springframework.aop.framework.JdkDynamicAopProxy
    * org.springframework.aop.framework.CglibAopProxy
      * org.springframework.aop.framework.ObjenesisCglibAopProxy

也可以使用动态编译，在运行时的编译相应的class

### 60 | JDK AopProxy实现 – JdkDynamicAopProxy

* 实现 - org.springframework.aop.framework.JdkDynamicAopProxy
  * 配置 - org.springframework.aop.framework.AdvisedSupport
  * 来源 - org.springframework.aop.framework.DefaultAopProxyFactory

### 61 | CGLIB AopProxy实现 – CglibAopProxy

* 实现 - org.springframework.aop.framework.CglibAopProxy
  * 配置 - org.springframework.aop.framework.AdvisedSupport
  * 来源 - org.springframework.aop.framework.DefaultAopProxyFactory

### 62 | AopProxyFactory配置管理器 – AdvisedSupport

* 核心 API - org.springframework.aop.framework.AdvisedSupport
  * 语义 - 代理配置
  * 基类 - org.springframework.aop.framework.ProxyConfig
  * 实现接口 - org.springframework.aop.framework.Advised
  * 使用场景 - org.springframework.aop.framework.AopProxy 实现

### 63 | Advisor链工厂接口与实现 – AdvisorChainFactory

* 核心 API - org.springframework.aop.framework.AdvisorChainFactory
  * 特殊实现 - org.springframework.aop.framework.InterceptorAndDynamicMethodMatcher
  * 默认实现 - org.springframework.aop.framework.DefaultAdvisorChainFactory

### 64 | 目标对象来源接口与实现 – TargetSource

* 核心 API - org.springframework.aop.TargetSource
  * 实现
    * org.springframework.aop.target.HotSwappableTargetSource
    * org.springframework.aop.target.AbstractPoolingTargetSource
    * org.springframework.aop.target.PrototypeTargetSource
    * org.springframework.aop.target.ThreadLocalTargetSource
    * org.springframework.aop.target.SingletonTargetSource

### 65 | 代理对象创建基础类 – ProxyCreatorSupport

* 核心 API - org.springframework.aop.framework.ProxyCreatorSupport
  * 语义 - 代理对象创建基类
  * 基类 - org.springframework.aop.framework.AdvisedSupport

### 66 | AdvisedSupport事件监听器 – AdvisedSupportListener

* 核心 API - org.springframework.aop.framework.AdvisedSupportListener
  * 事件对象 - org.springframework.aop.framework.AdvisedSupport
  * 事件来源 - org.springframework.aop.framework.ProxyCreatorSupport
  * 激活事件触发 - ProxyCreatorSupport#createAopProxy
  * 变更事件触发 - 代理接口变化时、 Advisor 变化时、 配置复制

### 67 | ProxyCreatorSupport标准实现 – ProxyFactory

* 核心 API - org.springframework.aop.framework.ProxyFactory
  * 基类 - org.springframework.aop.framework.ProxyCreatorSupport
  * 特性增强
    * 提供一些便利操作

### 68 | ProxyCreatorSupport IoC容器实现 – ProxyFactoryBean

* 核心 API - org.springframework.aop.framework.ProxyFactoryBean
  * 基类 - org.springframework.aop.framework.ProxyCreatorSupport
  * 特点
    * Spring IoC 容器整合
      * org.springframework.beans.factory.BeanClassLoaderAware
      * org.springframework.beans.factory.BeanFactoryAware
  * 特性增强
    * 实现 org.springframework.beans.factory.FactoryBean


### 69 | ProxyCreatorSupport AspectJ实现 – AspectJProxyFactory

* 核心 API - org.springframework.aop.aspectj.annotation.AspectJProxyFactory
  * 基类 - org.springframework.aop.framework.ProxyCreatorSupport
  * 特点
    * AspectJ 注解整合
  * 相关 API
    * AspectJ 元数据 - org.springframework.aop.aspectj.annotation.AspectMetadata
    * AspectJ Advisor 工厂 - org.springframework.aop.aspectj.annotation.AspectJAdvisorFactory

Spring对Aspect的注解的支持，并不是对Aspect的编译器和语法的支持，这些东西实际上是AspectJ它目身本采就有的能力。
Spring只是借助它部分的API来实现它的需要的一些流程，Aspect的原生语义和Spring里面它并不是完全对等的。

### 70 | IoC容器自动代理抽象 – AbstractAutoProxyCreator

* API - org.springframework.aop.framework.autoproxy.AbstractAutoProxyCreator
  * 基类 - org.springframework.aop.framework.ProxyProcessorSupport
  * 特点
    * 与 Spring Bean 生命周期整合
      * org.springframework.beans.factory.config.SmartInstantiationAwareBeanPostProcessor

### 71 | IoC容器自动代理标准实现

* 基类 - org.springframework.aop.framework.autoproxy.AbstractAutoProxyCreator
  * 默认实现 - DefaultAdvisorAutoProxyCreator
  * Bean 名称匹配实现 - BeanNameAutoProxyCreator
  * Infrastructure Bean 实现 - InfrastructureAdvisorAutoProxyCreator

### 72 | IoC容器自动代理 AspectJ 实现 – AspectJAwareAdvisorAutoProxyCreator

* org.springframework.aop.aspectj.autoproxy.AspectJAwareAdvisorAutoProxyCreator
  * 基类 - org.springframework.aop.framework.autoproxy.AbstractAdvisorAutoProxyCreator

### 73 | AOP Infrastructure Bean接口 – AopInfrastructureBean

*  接口 - org.springframework.aop.framework.AopInfrastructureBean
  *  语义 - Spring AOP 基础 Bean 标记接口
  *  实现
    *  org.springframework.aop.framework.autoproxy.AbstractAutoProxyCreator
    *  org.springframework.aop.scope.ScopedProxyFactoryBean
  *  判断逻辑
    *  AbstractAutoProxyCreator#isInfrastructureClass
    *  ConfigurationClassUtils#checkConfigurationClassCandidate

### 74 | AOP上下文辅助类 – AopContext

*  API - org.springframework.aop.framework.AopContext
  *  语义 - ThreadLocal 的扩展， 临时存储 AOP 对象

### 75 | 代理工厂工具类 – AopProxyUtils

* API - org.springframework.aop.framework.AopProxyUtils
  * 代表方法
    * getSingletonTarget - 从实例中获取单例对象
    * ultimateTargetClass - 从实例中获取最终目标类
    * completeProxiedInterfaces - 计算 AdvisedSupport 配置中所有被代理的接口
    * proxiedUserInterfaces - 从代理对象中获取代理接口

### 76 | AOP工具类 – AopUtils

* API - org.springframework.aop.support.AopUtils
  * 代表方法
    * isAopProxy- 判断对象是否为代理对象
    * isJdkDynamicProxy - 判断对象是否为 JDK 动态代理对象
    * isCglibProxy - 判断对象是否为 CGLIB 代理对象
    * getTargetClass - 从对象中获取目标类型
    * invokeJoinpointUsingReflection - 使用 Java 反射调用 Joinpoint（ 目标方法）

代理对象是用于拦截，ointcut是继续去筛选，Advice是进行一个围绕，最终会被底层invokejoinpointUsingReflection这个方法来调用。


### 77 | AspectJ Enable模块驱动实现 – @EnableAspectJAutoProxy

* 注解 - org.springframework.context.annotation.EnableAspectJAutoProxy
  * 属性方法
    * proxyTargetClass - 是否已类型代理
    * exposeProxy - 是否将代理对象暴露在 AopContext 中
  * 设计模式 - @Enable 模块驱动
    * ImportBeanDefinitionRegistrar 实现 -org.springframework.context.annotation.AspectJAutoProxyRegistrar
  * 底层实现
    * org.springframework.aop.aspectj.annotation.AnnotationAwareAspectJAutoProxyCreator

### 78 | AspectJ XML配置驱动实现 

* XML 元素 - <aop:aspectj-autoproxy/>
  * 属性
    * proxy-target-class - 是否已类型代理
    * expose-proxy - 是否将代理对象暴露在 AopContext 中
  * 设计模式 - Extensible XML Authoring
  * 底层实现
   * org.springframework.aop.config.AspectJAutoProxyBeanDefinitionParser

### 79 | AOP配置Schema-based 实现 

* XML 元素 - <aop:config/>
  * 属性
    * proxy-target-class - 是否已类型代理
    * expose-proxy - 是否将代理对象暴露在 AopContext 中
  * 嵌套元素
    * pointcut
    * advisor
    * aspect
  * 底层实现
    * org.springframework.aop.config.ConfigBeanDefinitionParser

### 80 | Aspect Schema-based实现

* XML 元素 - <aop:aspect/>
  * 父元素 - <aop:config/>
  * 属性
    * ref - Spring Bean 引用的名称
    * order - Aspect 顺序数
  * 嵌套元素
    * pointcut
    * declare-parents
    * before
    * after
    * after-returning
    * after-throwing
    * around

### 81 | Pointcut Schema-based实现

* XML 元素 - <aop:pointcut/>
  * 父元素 - <aop:aspect/> 或 <aop:config/>
  * 属性
    * id - Pointcut ID
    * expression - （ 必须） AspectJ 表达式
  * 底层实现
    * org.springframework.aop.Pointcut


### 82 | Around Advice Schema-based实现

* XML 元素 - <aop:around/>
  * 父元素 - <aop:aspect/>
  * 属性
    * pointcut - AspectJ Pointcut 表达式
    * pointcut-ref - 引用的 AspectJ Pointcut 名称
    * method - 拦截目标方法
    * arg-names - 目标方法参数名称

### 83 | Before Advice Schema-based实现 

* XML 元素 - <aop:around/>
  * 父元素 - <aop:aspect/>
  * 属性
    * pointcut - AspectJ Pointcut 表达式
    * pointcut-ref - 引用的 AspectJ Pointcut 名称
    * method - 拦截目标方法
    * arg-names - 目标方法参数名称

### 84 | After Advice Schema-based实现 

* XML 元素 - <aop:after/>
  * 父元素 - <aop:aspect/>
  * 属性
    * pointcut - AspectJ Pointcut 表达式
    * pointcut-ref - 引用的 AspectJ Pointcut 名称
    * method - 拦截目标方法
    * arg-names - 目标方法参数名称

### 85 | After Returning Advice Schema-based实现

* XML 元素 - <aop:after-returning/>
  * 父元素 - <aop:aspect/>
  * 属性
    * pointcut - AspectJ Pointcut 表达式
    * pointcut-ref - 引用的 AspectJ Pointcut 名称
    * method - 拦截目标方法
    * arg-names - 目标方法参数名称
    * returning - 方法参数名称

### 86 | After Throwing Advice Schema-based实现

* XML 元素 - <aop:after-throwing/>
  * 父元素 - <aop:aspect/>
  * 属性
    * pointcut - AspectJ Pointcut 表达式
    * pointcut-ref - 引用的 AspectJ Pointcut 名称
    * method - 拦截目标方法
    * arg-names - 目标方法参数名称
    * throwing - 方法参数名称

### 87 | Adviser Schema-based实现

* XML 元素 - <aop:advisor/>
  * 父元素 - <aop:config/>
  * 属性
    * advice-ref - Advice Bean 引用
    * pointcut - AspectJ Pointcut 表达式
    * pointcut-ref - AspectJ Pointcut Bean 引用
    * order - Advisor 顺序数

### 88 | Introduction Schema-based实现

* XML 元素 - <aop:declare-parents/>
  * 父元素 - <aop:aspect/>
  * 属性
    * types-matching - 是否已类型代理
    * implement-interface - 实现接口全类名
    * default-impl - 默认实现全类名
    * delegate-ref - 委派实现 Bean 引用

### 89 | 作用域代理Schema-based实现

* XML 元素 - <aop:scoped-proxy/>
  * 属性
    * proxy-target-class - 是否已类型代理

### 90 | 面试题精选

沙雕面试题 - Spring AOP Advice XML 标签有哪些？

答：
* Around Advice : <aop:around/>
* Before Advice : <aop:before/>
* After: <aop:after/>
* AfterReturning : <aop:after-returning/>
* AfterThrowing : <aop:after-throwing/>


996 面试题 - 请解释 Spring @EnableAspectJAutoProxy的原理？

答： 参考 @EnableAspectJAutoProxy

劝退面试题 - Spring Configuration Class CGLIB 提升与 AOP 类代理的关系?


## 第四章：Spring AOP设计模式 (17讲)

### 91 | 抽象工厂模式（Abstract factory）实现

* 基本概念
抽象工厂模式提供了一种方式， 可以将一组具有同一主题的单独的工厂封装起来。 在正常使用中， 客户端程序需要创建抽象工厂的具体实现， 然后使用抽象工厂作为接口来创建这一主题的具体对象。 客户端程序不需要知道（ 或关心） 它从这些内部的工厂方法中获得对象的具体类型， 因为客户端程序仅使用这些对象的通用接口。 抽象工厂模式将一组对象的实现细节与他们的一般使用分离开来。

* Spring AOP 举例实现
  * 接口 - org.springframework.aop.framework.AopProxyFactory
  * 实现 - org.springframework.aop.framework.DefaultAopProxyFactory

### 92 | 构建器模式（Builder）实现

* 基本概念
建造模式， 是一种对象构建模式。 它可以將複雜對象的建造過程抽象出來（ 抽象類別） ， 使这个抽象过程的不同实现方法可以构造出不同表现（ 属性） 的对象。

* Spring AOP 举例实现
  * 实现 -org.springframework.aop.aspectj.annotation.BeanFactoryAspectJAdvisorsBuilder

### 93 | 工厂方法模式（Factory method）实现

* 基本概念
就像其他创建型模式一样， 它也是处理在不指定对象具体类型的情况下创建对象的问题。 工厂方法模式的实质是“ 定义一个创建对象的接口， 但让实现这个接口的类来决定实例化哪个类。 工厂方法让类的实例化推迟到子类中进行。 ”

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.framework.ProxyFactory

### 94 | 原型模式（Prototype）实现

* 基本概念
创建型模式的一种， 其特点在于通过「 复制」 一个已经存在的实例来返回新的实例,而不是新建实例。被复制的实例就是我们所称的「 原型」 ， 这个原型是可定制的。
原型模式多用于创建复杂的或者耗时的实例， 因为这种情况下， 复制一个已经存在的实例使程序运行更高效； 或者创建值相等， 只是命名不一样的同类数据。

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.target.PrototypeTargetSource

### 95 | 单例模式（Singleton）实现

* 基本概念
属于创建型模式的一种。 在应用这个模式时， 单例对象的类必须保证只有一个实例存在。 许多时候整个系统只需要拥有一个的全局对象， 这样有利于我们协调系统整体的行为。 比如在某个服务器程序中， 该服务器的配置信息存放在一个文件中， 这些配置数据由一个单例对象统一读取， 然后服务进程中的其他对象再通过这个单例对象获取这些配置信息。 这种方式简化了在复杂环境下的配置管理。

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.target.SingletonTargetSource

### 96 | 适配器模式（Adapter）实现

* 基本概念
有时候也称包装样式或者包装（ 英語： wrapper） 。 将一个类的接口轉接成用户所期待的。 一个适配使得因接口不兼容而不能在一起工作的类能在一起工作， 做法是将类自己的接口包裹在一个已存在的类中。

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.framework.adapter.AdvisorAdapter
  * 适配对象 - org.aopalliance.aop.Advice
  * 目标对象 - org.aopalliance.intercept.MethodInterceptor

### 97 | 组合模式（Composite）实现

* 基本概念
The composite pattern describes a group of objects that are treated the same way as a single instance of the same type of object. The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies. Implementing the composite pattern lets clients treat individual objects and compositions uniformly.

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.support.ComposablePointcut
  * 接口 - org.springframework.aop.Pointcut
  * 成员 - org.springframework.aop.Pointcut


### 98 | 装饰器模式（Decorator）实现

* 基本概念
一种动态地往一个类中添加新的行为的设计模式。 就功能而言， 修饰模式相比生成子类更为灵活， 这样可以给某个对象而不是整个类添加一些功能。

* Spring AOP 举例实现
  * 实现 -org.springframework.aop.aspectj.annotation.LazySingletonAspectInstanceFactoryDecorator

### 99 | 享元模式（Flyweight）实现

 * 基本概念
它使用物件用來尽可能減少内存使用量； 便于相似物件中分享更多的数据。 复杂对象缓存，数据共享。

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.framework.adapter.AdvisorAdapterRegistry


### 100 | 代理模式（Proxy）实现

* 基本概念
所謂的代理者是指一個類別可以作為其它東西的介面。 代理者可以作任何東西的介面： 網路連接、 記憶體中的大物件、 檔案或其它昂貴或無法複製的資源。

* Spring AOP 举例实现
  * 实现 - org.springframework.aop.framework.AopProxy
    * JDK - org.springframework.aop.framework.JdkDynamicAopProxy
    * CGLIB - org.springframework.aop.framework.CglibAopProxy

### 101 | 模板方法模式（Template Method）实现

* 基本概念
模板方法是一個定義在父類別的方法， 在模板方法中會呼叫多個定義在父類別的其他方法， 而這些方法有可能只是抽象方法並沒有實作， 模板方法僅決定這些抽象方法的執行順序， 這些抽象方法的實作由子類別負責， 並且子類別不允許覆寫模板方法。

* Spring AOP 举例实现
  * 模板类 - org.springframework.aop.framework.autoproxy.AbstractAutoProxyCreator
  * 模板方法 - getAdvicesAndAdvisorsForBean(Class,String,TargatSource)
  * 子类实现
    * org.springframework.aop.framework.autoproxy.InfrastructureAdvisorAutoProxyCreator(XML)
    * org.springframework.aop.aspectj.annotation.AnnotationAwareAspectJAutoProxyCreator(注解）


### 102 | 责任链模式（Chain of Responsibility）实现

* 基本概念
包含了一些命令对象和一系列的处理对象。 每一个处理对象决定它能处理哪些命令对象， 它也知道如何将它不能处理的命令对象传递给该链中的下一个处理对象。 该模式还描述了往该处理链的末尾添加新的处理对象的方法。

* Spring AOP 举例实现
  * 接口 - org.springframework.aop.framework.AdvisorChainFactory
  * 实现 - org.springframework.aop.framework.DefaultAdvisorChainFactory

### 103 | 观察者模式（Observer）实现

* 基本概念
一個目標物件管理所有相依於它的觀察者物件， 並且在它本身的狀態改變時主動發出通知。 這通常透過呼叫各觀察者所提供的方法來實現。 此種模式通常被用來實时事件處理系統。

* Spring AOP 举例实现
  * 观察者 - org.springframework.aop.framework.ProxyCreatorSupport
  * 被观察者 - org.springframework.aop.framework.AdvisedSupportListener
  * 通知对象 - org.springframework.aop.framework.AdvisedSupport

### 104 | 策略模式（Strategy）实现

* 基本概念
指對象有某個行爲， 但是在不同的場景中， 該行爲有不同的實現算法。 比如每個人都要“ 交個人所得 稅” ， 但是每國交個人所得稅就有不同的算稅方法。

* Spring AOP 举例实现
  * org.springframework.aop.framework.DefaultAopProxyFactory#createAopProxy
  * org.springframework.aop.config.ConfigBeanDefinitionParser#getAdviceClass

### 105 | 命令模式（Command）实现


* 基本概念
  * 它嘗試以物件來代表實際行動。 命令物件可以把行動(action) 及其參數封裝起來， 於是這些行動可以被：
    * 重複多次
    * 取消（ 如果該物件有實作的話）
    * 取消後又再重做
    
* Spring AOP 举例实现
  * org.aopalliance.intercept.MethodInvocation
  * org.aspectj.lang.ProceedingJoinPoint

### 106 | 状态模式（State）实现

* 基本概念
允许对象在内部状态发生变化时更改其行为。 这种模式接近于有限状态机的概念。 状态模式可以解释为策略模式， 它能够通过调用模式接口中定义的方法来切换策略。

* Spring AOP 举例实现
  * 状态对象 - org.springframework.aop.framework.ProxyConfig
  * 影响对象 - org.springframework.aop.framework.AopProxy
    * org.springframework.aop.framework.JdkDynamicAopProxy
    * org.springframework.aop.framework.CglibAopProxy

### 107 | 面试题精选

沙雕面试题 - GoF 23 设计模式和它的归类？

答：
* Creational（ 创建模式） ： Abstract factory、 Builder、 Factorymethod、 Prototype 和 Singleton
* Structural（ 结构模式） ： Adapter、 Bridge、 Composite、Decorator、 Facade、 Flyweight 和 Proxy
* Behavioral（ 行为模式） ： Chain of responsibility、 Command、Interpreter、 Iterator、 Mediator、 Memento、 Observer、 State、 Strategy、 Template method 和 Visitor


996 面试题 - 举例介绍装饰器模式和代理模式的区别？

答： 代理模式不要求和被代理对象存在层次关系装饰器模式则需要和被装饰者存在层次关系

装饰器模式通常来说会生成或者会新建些扩展的行为，这个行为它并不隶属于被装饰者之间。
比如说你要去实现一个比如说像ServletRequestWrapper这种东西， 也可能在那个方法里面增加一些新的关于这种行为的一个扩展。
但是代理模式通常不会，代理模式它的功能是被代理者的子集或最多是全集，不会是什么不会是超集。
通常来说代理模式它可以是比如说直接代理或者间接代理这种方式来进行操作，或者通过我们所说的静态代理和动态代理两种实现方式，而装饰器模式通常来说它只有静态方式来进行操作。
也就是说它要通过编译的方式来生成相应的文件，比如说我们举个例子比如说像InputStream和BufferInputStream。
比如说像我们说Java里面的动态代理，那么Proxy API里面就会有相应的对象。
比如说InvocationHandler它其实也是一种类似像代理的方式操作。

劝退面试题 - 请举例说明 Spring Framework 中使用设计模式的实现?


## 第五章：Spring AOP在Spring Framework内部应用 (7讲)

### 108 | Spring AOP    在 Spring 事件（Events）

* 核心 API - org.springframework.context.event.EventPublicationInterceptor
* 特性描述
 * 当 Spring AOP 代理 Bean 中的 JoinPoint 方法执行后， Spring ApplicationContext 将发布一个自定义事件（ ApplicationEvent 子类）
* 使用限制
  * EventPublicationInterceptor 关联的 ApplicationEvent 子类必须存在单参数的构造器
  * EventPublicationInterceptor 需要被声明为 Spring Bean

### 109 | Spring AOP在Spring 事务（Transactions）理论基础

* 核心 API
  * Spring 事务 @Enable 模块驱动 -@EnableTransactionManagement
  * Spring 事务注解 - @Transactional
  * Spring 事务事件监听器 - @TransactionalEventListener
  * Spring 事务定义 - TransactionDefinition
  * Spring 事务状态 - TransactionStatus
  * Spring 平台事务管理器 - PlatformTransactionManager
  * Spring 事务代理配置 - ProxyTransactionManagementConfiguration
  * Spring 事务 PointcutAdvisor 实现 - BeanFactoryTransactionAttributeSourceAdvisor
  * Spring 事务 MethodInterceptor 实现 - TransactionInterceptor
  * Spring 事务属性源 - TransactionAttributeSource


Spring AOP 在 Spring 事务（ Transactions）

* 理解 TransactionDefinition（ Spring 事务定义）
  * 说明： Interface that defines Spring-compliant transaction properties. Based on the propagation behavior definitions analogous to EJB CMT attributes.
  
  * 核心方法
    * getIsolationLevel() ： 获取隔离级别， 默认值 ISOLATION_DEFAULT 常量， 参考org.springframework.transaction.annotation.Isolation
    * getPropagationBehavior()： 获取事务传播， 默认值： PROPAGATION_REQUIRED 常量， 参考org.springframework.transaction.annotation.Propagation
    * getTimeout()： 获取事务执行超时时间， 默认值： TIMEOUT_DEFAULT 常量
    * isReadOnly()： 是否为只读事务， 默认值： false

* 理解 TransactionStatus（ Spring 事务状态）
  * 说明： Interface that specifies an API to programmatically manage transaction savepoints in a generic fashion. Extended by TransactionStatus to expose savepoint management functionality for a specific transaction.
  * 核心方法
    * isNewTransaction() ： 当前事务执行是否在新的事务
    * setRollbackOnly()： 将当前事务设置为只读
    * isRollbackOnly()： 当前事务是否为只读
    * isCompleted()： 当前事务是否完成
    
* 理解 PlatformTransactionManager（ 平台事务管理器）
  * 说明： the central interface in Spring's transaction infrastructure. Applications can use this directly, but it is not primarily meant as API: Typically, applications will work with either TransactionTemplate or declarative transaction demarcation through AOP.
  * 核心方法
    * getTransaction(TransactionDefinition) ： 获取事务状态
    * commit(TransactionStatus)： 提交事务
    * rollback(TransactionStatus)： 回滚事务

* 理解 Spring 事务传播（ Transaction Propagation）
  * 官方文档： https://docs.spring.io/springframework/docs/current/reference/html/data-access.html#tx-propagation

### 110 | Spring AOP在Spring 事务（Transactions）源码分析



### 111 | Spring AOP在Spring 缓存（Caching）

* 核心 API
  * Spring 缓存 @Enable 模块驱动 - @EnableCaching
  * 缓存操作注解 - @Caching、 @Cachable、 @CachePut、 @CacheEvict
  * 缓存配置注解 - @CacheConfig
  * 缓存注解操作数据源 - AnnotationCacheOperationSource
  * Spring 缓存注解解析器 - SpringCacheAnnotationParser
  * Spring 缓存管理器 - CacheManager
  * Spring 缓存接口 - Cache
  * Spring 缓存代理配置 - ProxyCachingConfiguration
  * Spring 缓存 PointcutAdvisor 实现 - BeanFactoryCacheOperationSourceAdvisor
  * Spring 缓存 MethodInterceptor 实现 - CacheInterceptor


### 112 | Spring AOP在Spring本地调度（Scheduling）

* 核心 API
  * Spring 异步 @Enable 模块驱动 - @EnableAsync
  * Spring 异步注解 - @Async
  * Spring 异步配置器 - AsyncConfigurer
  * Spring 异步代理配置 - ProxyAsyncConfiguration
  * Spring 异步 PointcutAdvisor 实现 - AsyncAnnotationAdvisor
  * Spring 异步 MethodInterceptor 实现 - AnnotationAsyncExecutionInterceptor

### 113 | 面试题精选


沙雕面试题 - 请举例说明 Spring AOP 在 Spring
Framework 特性运用？

答：
* Spring 事件（ Events）
* Spring 事务（ Transaction）
* Spring 缓存（ Caching）
* Spring 本地调度（ Scheduling）
* Spring 远程（ Remoting）

996 面试题 - 请解释 Spring 事务传播的原理？

劝退面试题 - 请总结 Spring AOP 与 IoC 功能整合的设计模式？
答：
* 实现 Advice 或 MethodInterceptor
* 实现 PointcutAdvisor
* 实现 Spring AOP 代理配置类
* （ 可选） 实现注解和注解元信息的解析以及处理
* （ 可选） 实现 XML 与其元信息的解析以及处理


### 114 | 结束语



