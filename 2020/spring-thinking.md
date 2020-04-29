# Spring Boot 编程思想

IoC是一种设计原则，DI是IoC的一种实现方式（IoC不是Spring特有）

## IoC 容器底层是BeanFactory（抽象工厂）

是的，Spring Bean 的维护和生命周期管理均在BeanFactory实现类中，绝大多数是指DefaultListableBeanFactory

## Spring IoC容器：BeanFactory和ApplicationContext谁才是Spring IoC容器？

1. ApplicationContext和BeanFactory之间的关系, 也知道了DefaultListableBeanFactory被组合到了
AbstractRefreshableApplicationContext,但并没有回答一个问题: 
UserRepository中的BeanFactory beanFactory属性为什么通过autowired= "byType” ，
注入的是DefaultListableBeanFactory,而不是
ClassPathXmlApplicationContext?既然他们两者属于BeanFactory接口, 
按type注入, 为什么不是ClassPathXmlApplicationContext? 是框架哪里设置的吗?


org.springframework.context.support.AbstractApplicationContext#prepareBeanFactory方法中，其中:

```java

beanFactory.registerResolvableDependency(BeanFactory.class, beanFactory);

beanFactory.registerResolvableDependency(ResourceLoader.class, this);

beanFactory.registerResolvableDependency(ApplicationEventPublisher.class, this);

beanFactory.registerResolvableDependency(ApplicationContext.class, this);

```

以上代码明确地指定了BeanFactory 类型的对象是ApplicationContext#getBeanFactory()方法的内容，而非它自生。


2.为什么spring需要做这么一层代理实现呢， 直接用ApplicationContext继承某个BeanFactory,然后提供新的能力的式不好吗,是因为太耦合了吗
  
这样设计相对简单，将ApplicationContext作为Facade（外观）提供一个大而全的API 


3. 有点想委派，直接调用底层BeanFactory实现类的方法

## ApplicationContext除了IoC容器角色，还提供了哪些特性

我们常说spring的核心就是IOC和AOP,但是BeanFactory和ApplicationContext才是真正的IOC容器，
ApplicationContext又提供了AOP的功能，那之前的说法是不是有点问题?

并不矛盾，BeanFactory 是Bean容器，它不提供企业特性，比如AOP、事务以及事件等，这些都被ApplicationContext支持。

## Spring IoC 选 BeanFactory还是ApplicationContext

一般是ApplicationContext 

1.当前类不加@Configuration也能获取到bean,粗当前类也会作为-个bean

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

## BeanFactory与FactoryBean?
   
BeanFactory是loC底层容器，ApplicationContext是在BeanFactory基础上扩展，组合了DefaultListableBeanFactory
   
FactoryBean是创建Bean的一种方式，帮助实现复杂的初始化逻辑

## AnnotationConfigApplicationContext

1. AnnotationConfigApplicationContext继承了GenicApplicationontext它的refreshBeanFactory()只是在无参构造函数中new 
DefaultListableBeanFactory(),并没有注册bean定义相关的步骤,不是此类ApplicationContext不要注册bean定义?
      
AnnotationConfigApplicationContext不需要加载外部配置化的BeanDefinition,比如
   
ClassPathXmlApplicationContext继承了AbstractRefreshableConfigApplicationContext 在
   
refreshBeanFactory()方法会调用loadBeanDefinitions()方法，在AbstractXmlApplicationContext的实现作用下，加载XML配置元素。
 
 ## 双亲委派
 
BeanFactory的双亲委派和ClassLoader类似，和Bean冲突没有直接关系。
    
BeanFactoryUtils#beansOfTypelncludingAncestors仍旧是递归地查找指定类型的Bean集合，并且是在所有层次类查找，
只不过该方法会排除子BeanFactory已存在的Bean,这是一种就近原则的设计。

基本都是单一查找， 依赖查找可以在LB这种场景应用，但这个分层查找有啥用?

比如Spring MVC中，Biz 组件放在Root ApplicationContext,而Web组件放在DispatcherServlet的ApplicationContext,
后者是前者的子ApplicationContext,所以，子ApplicationContext可以读取父ApplicationContext

## ClassPathXmlApplicationContext

在够早ClassPathXmlApplicationContext需要指定XML文件的位置，为什么Spring还要提供无参的构造方法

通过构造器传递XML配置文件默认会自动启动上下文，默认构造器则不会，按照需要设置配置文件，并启动

## 如何注册一个Spring Bean?
   
通过BeanDefinition和外部单体对象来注册

## 注入

1. 有一点"设置属性autowire candidate为false”，太明白是什么意思?

autowire-candidate属性是设置当前Bean是否为其他Bean autowiring候选者

2. 可以讲解下setter注入的原理吗,为什么注入顺序是不确定的，不是从上往下执行代码嘛?
  
并不是，由于Java反射API所返回的public方法热顺序并非定义顺序，所以无法控制先后情况。你可以自行尝试!

3. 构造器参数不会选择默认构造器，否则没有入口让Bean注入。通常spring Framework会尽可能地选择能够构造器参数注入的构造器。

4.静态字段该怎么注入呢?
  
通常通过实例方法注入，然后再通过该方法注入到静态资源，还有一种比较常见， 通过ApplicationContextAware或BeanFactorIyAware来操作

5. 方法注入和Setter注入有什么不同?
   
 Setter 注入是通过Java Beans来实现的，而方法注入则是直接通过Java反射来做的。当然底层都是Java反射~ 
 
6. 当任意Spring Bean实现类实现了BeanFactoryAware 接口时，在Bean生命周期回调时，会被容器调用setBeanFactory方法~

7.  @Bean的方式通常属于半自动方式，许多关联Bean需要手动关联

```java
public class T{
    @Bean //Lite 模式
    //@Configuration Full 模式 CGLIB 提升 CGLib 新类 extends XXX
    @Autowired
    
    public UserRepository userRepository(Collection<User> users, BeanFactory beanFactory){
    
        UserRepository userRepository = new UserRepository();
    
        // auto-wiring = by-type
        
        userRepository.setUsers(users);
        
        userRepository.setBeanFactory(beanFactory);
        
        return userRepository;
    
    }
}

```

## IoC容器

1. Ioc发展简介

控制反转（Inversion of Control，缩写为IoC），是面向对象编程中的一种设计原则，可以用来降低程序代码之间的耦合度。其中最常见的方式叫做依赖注入（Dependency Injection，简称DI），还有一种方式叫“依赖查找”（Dependency Lookup）。通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体将其所依赖的对象的引用传递给它。也可以说，依赖被注入到对象中。

IoC实际遵循的是DIP依赖倒置原则，上层模块不应该依赖于低层模块，二者应该通过抽象来依赖。Ioc把程序上层对下层的依赖转移到了第三方容器进行管理装配.

2. java beans 也是Ioc?

Ioc 中的一个重要的应用，其实就是java beans

spring 与bean的关系：继承，依赖 引用。

其实提到IOC可以说是ioc容器，spring通过IOC容器来管理所有的java 对象及其相互间的依赖关系。

3.依赖注入（Dependency Injection，DI）和控制反转的关系？

依赖注入是一个程序设计模式和架构模型，也称控制反转。

在技术上来说依赖注入是一个控制反转的特殊事项，但依赖注入还指一个对象应用另外一个对象来提供一个它没有的功能。

如把一个数据库连接以参数的形式传到一个对象的结构方法里，而不是在那个对象内部自行创建一个连接。

控制反转的实现类型：依赖注入（Dependency Injection，DI）和依赖查找（Dependency Lookup）。

其中依赖注入应用较为广泛，spring就是采用此方式来实现控制反转的。





