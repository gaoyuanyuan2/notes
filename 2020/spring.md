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

代理模式（ObjectProvider代理依赖查找）