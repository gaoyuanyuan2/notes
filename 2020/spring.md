# Spring

总结

## BeanFactory与FactoryBean？

BeanFactory 是IOC底层容器

FactoryBean是创建Bean的一种方式，帮助实现复杂的初始化逻辑

BeanFactory和FactoryBean,其中BeanFactory指的是IOC容器的编程抽象，比如

ApplicationContext, XmlBeanFactory 等，这些都是IOC容器的具体表现，需要使用什么样的容器由客户决定,但Spring为我们提供了丰富的选择。
FactoryBean 只是一个可以在IOC而容器中被管理的一个bean,是对各种处理过程和资源使用的抽象,FactoryBean在需要时产生另一个对象，而不返回
FactoryBean本身,我们可以把它看成是一个抽象工厂，对它的调用返回的是工厂“生产的产品”。所有的FactoryBean都实现特殊的
org.springframework.beans.factory.FactoryBean接口，当使用容器中FactoryBean的时候，
该容器不会返回FactoryBean本身,而是返回其生成的对象。Spring 包括了大部分的通用资源和服务访问抽象的FactoryBean的实现，
其中包括:对JNDI查询的处理，对代理对象的处理，对事务性代理的处理，对RMI代理的处理等，这些我们都可以看成是具体的工厂，
看成是Spring为我们建立好的工厂。也就是说Spring通过使用抽象工厂模式为我们准备了一系列工厂来生产一些特定的对象，
免除我们手工重复的工作，我们要使用时只需要在IOC容器里配置好就能很方便的使用了

## Spring IoC容器：BeanFactory和ApplicationContext谁才是Spring IoC容器？

1. ApplicationContext和BeanFactory之间的关系, 也知道了DefaultListableBeanFactory被组合到了

2. AnnotationConfigApplicationContext继承了GenericApplicationContext它的refreshBeanFactory()只是在无参构造函数中new 
DefaultListableBeanFactory
      
## ApplicationContext除了IoC容器角色，还提供了哪些特性

我们常说spring的核心就是IOC和AOP,但是BeanFactory和ApplicationContext才是真正的IOC容器，
ApplicationContext又提供了AOP的功能，那之前的说法是不是有点问题?

并不矛盾，BeanFactory 是Bean容器，它不提供企业特性，比如AOP、事务以及事件等，这些都被ApplicationContext支持。


## IoC 容器底层是BeanFactory（抽象工厂）

是的，Spring Bean 的维护和生命周期管理均在BeanFactory实现类中，绝大多数是指DefaultListableBeanFactory

## 双亲委派
 
BeanFactory的双亲委派和ClassLoader类似，和Bean冲突没有直接关系。
    
BeanFactoryUtils#beansOfTypelncludingAncestors仍旧是递归地查找指定类型的Bean集合，并且是在所有层次类查找，
只不过该方法会排除子BeanFactory已存在的Bean,这是一种就近原则的设计。

基本都是单一查找， 依赖查找可以在LB这种场景应用，但这个分层查找有啥用?

比如Spring MVC中，Biz 组件放在Root ApplicationContext,而Web组件放在DispatcherServlet的ApplicationContext,
后者是前者的子ApplicationContext,所以，子ApplicationContext可以读取父ApplicationContext



## Spring IoC 选 BeanFactory还是ApplicationContext

一般是ApplicationContext 

1.当前类不加@Configuration也能获取到bean,且当前类也会作为一个bean

 @Configuration注册并不是必须的，不过标注它之后Bean的类被CGLib提升。
 
2.beanFactory用的什么设计模式 

DefaultListableBeanFactory实现的设计模式有:
  
抽象工厂(BeanFactory 接口实现)

组合模式(组合AutowireCandidateResolver等实例)

单例模式(Bean Scope)

原型模式(Bean Scope)

模板模式(模板方法定义: AbstractBeanFactory)

适配器模式(适配BeanDefinitionRegistry接口)

策略模式(Bean实例化)

代理模式(ObjectProvider 代理依赖查找)


## IoC 容器底层是BeanFactory（抽象工厂）

是的，Spring Bean 的维护和生命周期管理均在BeanFactory实现类中，绝大多数是指DefaultListableBeanFactory

org.springframework.context.support.AbstractApplicationContext#prepareBeanFactory方法中，其中:

```java
//注册可以解析的自动装配；我们能直接在任何组件中自动注入

beanFactory.registerResolvableDependency(BeanFactory.class, beanFactory);

beanFactory.registerResolvableDependency(ResourceLoader.class, this);

beanFactory.registerResolvableDependency(ApplicationEventPublisher.class, this);

beanFactory.registerResolvableDependency(ApplicationContext.class, this);

```

以上代码明确地指定了BeanFactory 类型的对象是ApplicationContext#getBeanFactory()方法的内容，而非它自生。


2.为什么spring需要做这么一层代理实现呢， 直接用ApplicationContext继承某个BeanFactory,然后提供新的能力的式不好吗,是因为太耦合了吗
  
这样设计相对简单，将ApplicationContext作为Facade（外观）提供一个大而全的API 

3. 有点想委派，直接调用底层BeanFactory实现类的方法

## 重点

* Spring 应用上下文生命周期

* Spring Bean 生命周期

* Spring Bean 容器

* Spring 事件/监听机制

* Spring 工厂加载机制

* Spring Aware

* Spring Environment 抽象

* Spring 接口

## 设计模式

抽象工厂（BeanFactory接口实现）

组合模式（组合AutowireCandidateResolver）

单例模式（Bean Scope）

原型模式（Bean Scope）

模板模式（模板方法定义AbstractBeanFactory）

策略模式（Bean实例化）

## Spring 中的 bean 的作用域有哪些?

* singleton : 唯一 bean 实例，Spring 中的 bean 默认都是单例的。
* prototype : 每次请求都会创建一个新的 bean 实例。
* request : 每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效。
* session : 每一次HTTP请求都会产生一个新的 bean，该bean仅在当前 HTTP session 内有效。
* global-session： 全局session作用域，仅仅在基于portlet的web应用中才有意义，Spring5已经没有了。Portlet是能够生成语义代码(例如：HTML)片段的小型Java Web插件。它们基于portlet容器，可以像servlet一样处理HTTP请求。但是，与 servlet 不同，每个 portlet 都有不同的会话

## @Component 和 @Bean 的区别是什么？

1. 作用对象不同: @Component 注解作用于类，而@Bean注解作用于方法。

2. @Component通常是通过类路径扫描来自动侦测以及自动装配到Spring容器中（我们可以使用 @ComponentScan 注解定义要扫描的路径从中找出标识了需要装配的类自动装配到 Spring 的 bean 容器中）。@Bean 注解通常是我们在标有该注解的方法中定义产生这个 bean,@Bean告诉了Spring这是某个类的示例，当我需要用它的时候还给我。

3. @Bean 注解比 Component 注解的自定义性更强，而且很多地方我们只能通过 @Bean 注解来注册bean。
比如当我们引用第三方库中的类需要装配到 Spring容器时，则只能通过 @Bean来实现。

## @Transactional

在@Transactional注解中如果不配置rollbackFor属性,那么事物只会在遇到RuntimeException的时候才会回滚,加上rollbackFor=Exception.class,可以让事物在遇到非运行时异常时也回滚。

## JDBC

jpa 默认实现是hibernate


## 些常用操作

* 判断类是否存在
  * ClassUtils.isPresent()
* 判断Bean是否已定义
  * ListableBeanFactory.containsBeanDefinition()
  * ListableBeanFactory.getBeanNamesForType()
* 注册Bean定义.
  * BeanDefinitionRegistry.registerBeanDefinition()
  * GenericBeanDefinition
  * BeanFactory.registerSingleton()

