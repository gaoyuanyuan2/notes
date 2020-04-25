# Spring 简化开发

* 轻量级

零配置编程、API使用简单

* 面向Bean

只需要编写非常普通的Bean

* 松耦合

充分利用AOP思想，一个切面就是一个规则，先拆分后组装

**定义**

面向切面编程，即AOP,是一种编程思想， 允许程序员对横切关注点或横切典型的职责分界线的行为(例如日志和事务管理)进行模块化。
AOP的核心构造是方面，它将那些影响多个类的行为封装到可重用的模块中。

* 万能胶
与主流框架无缝集成

* 设计模式
将Java中经典的设计模式运用得淋漓尽致


## 说明

注入：默认按类型，也可以指定名称

IOC容器：装java bean （Web容器：装servlet）


定位、加载、注册

Beans

Core

Context

## AOP的功能完全集成到了Spring 事务管理、日志和其他各种特性的上下文中

* Authentication权限认证

* Logging日志

* TransactionManager事务

* Lazy Loading懒加载

* Context Process 上下文处理

* Error Handler错误跟踪(异常捕获机制)

* Cache缓存

## 常见模式

* 代理模式

* 工厂模式: 1、隐藏复杂的逻辑过程，只关心结果。简单工厂、工厂方法、抽象工厂

* 单例模式: 1、保证从系统启动到系统停止，全过程只会产生一个实例。

* 委派模式: 1、类似于中介的功能(委托机制) ; 2、只有被委托人的引用。要和代理模式区分开来

* 策略模式: 1、过程不同，但结果一样。

* 原型模式: 1、过程相同，但结果不一样。或者叫模板模式(提高开发效率)


|设计模式 | 应用场景(特点) Design Patterns|一句话归纳|
|:--:|:--:|:--:|
|代理模式 Proxy | 1、两个参与角色:执行者(代理人)、被代理人 <br>2、对于被代理人来说， 这件事情是一定要做的，但是我自己又不想做或者没有时间做，找代理。<br>3、代理人必须需要获取到被代理的人个人资料(持有被代理人的引用)。|办事要求人，所以找代理|
|工厂模式 Factory|  1、对调用者隐藏复杂的逻辑处理过程，调用者只关心执行结果。 2、对于工厂来说要对结果负责，保证生产出符合规范的产品。| 只对结果负责， 不要三无产品。| 
|单例模式 Singleton|1、保证从系统启动到系统终止，全过程只会产生一个实例。 <br>2、当我们在应用中遇到功能性冲突的时候，需要使用单例模式。 |保证独一无二|
|委派模式  Delegate|1、两个参与角色，委托人和被委托人。 <br>2、委托人和被委托人在权利上完全平等(即实现同一个接口)<br>3、委托人持有被委托人的引用。<br>4、不关心过程，只关心结果。 |干活是你的(普通员工)，功劳是我的(项目经理)。|
|策略模式 Strategy| 1、执行最终结果一样。 <br>2、执行过程和执行逻辑不一样。| 我行我素，达到目的就行| 
|原型模式 Prototype| 1、首先有一个原型。  <br>2、数据内容相同，但对象实例不同(完全两个不同的内存地址) |拔一根猴毛，吹出千万个|
|模板模式 Template|1、执行流程固定，但中间有些步骤有细微差别。<br>2、可实现批量生产。|流程标准化，原料自己加|


## 事务

通过解析配置文件，得到TransactionDefinition代理 (实际上就是AOP中的MethodInterceptor 方法)

就可以在满足条件的方法调用之前和调用之后加一些东西

PlatformTransactionManger中的方法getTransaction()  调用了TransactionSynchronizationManager类的getResource()

从ThreadLocal里面取值，Map<Key:DataSource ,Value:ConnectionHolder> (相当于获取一个连接对象Connection);

##  延迟查找

```java
public class VelocityLayoutAutoConfiguration{
    
    private VelocityConfigurer velocityConfigurer;
    
    private ObjectProvider<VelocityConfigurer> velocityConfigurerObjectProvider; //延迟依赖查找
    
    @Lazy
    private VeloeityConfigurer laziedVelocityConfigurer; // Lazy（代理）对象会被字节码提升延迟依赖注入
    
    public VelocityLayoutAutoConfiguration(VelocityConfiguree velocityConfigurer) { //可能过早初始化VelocityConfigurer
      this .velocityConfigurer = velocityConfigurer;
     }
    
    public VelocityLayoutAutoConfiguration(ObjectProvider<VelocityConfigurer> velocityConfigurer) {
        this.velocityConfigurerobjectProvider = velocityConfigurer;
    
    }
    
    @PostConstruct
    public void process() {
        velocityConfigurerobjectProvider.getIfAvailable(); //才发生Bean初始化
    }
}
```

## 底层是BeanFactory?

Spring Bean的维护和生命周期管理均在BeanFactory实现类中，绝多大数是指DefaultLlistableBeanFactory





