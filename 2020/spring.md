# Spring

## BeanFactory与FactoryBean？

BeanFactory 是IOC底层容器

FactoryBean是创建Bean的一种方式，帮助实现复杂的初始化逻辑

## 重点

* Spring 应用上下文生命周期

* Spring Bean 生命周期

* Spring Bean 容器

* Spring 事件/监听机制

* Spring 工厂加载机制

* Spring Aware

* Spring Envionmnet 抽象

* Spirng 接口

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


