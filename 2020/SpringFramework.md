# Spring Framework （小马哥）

## 第一章：Spring Framework总览 (12讲)

01 | 课程介绍

02 | 内容综述

1.特性

按需分配

胶水：API和或者规范整合在一起

2.使用API

Spring 3 对Java 5 的支持

Spring 5 对Java 8 的支持

Java: XML、反射、动态代理

JavaEE: Servlet、Jsp、Jpa、Jms

3.自己的实现

* 面向对象（OOP）：多态，接口对应语义


* 切面编程：jdk动态代理、ASM、CGLIB、AspectJ 类的提升

* 面向元编程

配置元信息：配置类，配置属性在XML或者.properties文件，会影响运行时的一些状态，比如影响依赖注入的方式

注解

属性配置：占位符、外部化配置

不是面向程序来编程，在程序的基础上在进行元数据的一些处理

* 面向模块编程 

Maven Artifacts

OSGI Bundles

Java 9 Automatic Modules

Spring @Enable* 注解

* 面向函数编程 

Lambda

Reactive

03 | 课前准备：学习三件套（工具、代码与大脑）

04 | 特性总览：核心特性、数据存储、Web技术、框架整合与测试

05 | Spring版本特性：Spring各个版本引入了哪些新特性？

06 | Spring模块化设计：Spring功能特性如何在不同模块中组织？

07 | Java语言特性运用：各种Java语法特性是怎样被Spring各种版本巧妙运用的？

08 | JDK API实践：Spring怎样取舍Java I/O、集合、反射、动态代理等API的使用？

09 | Java EE API整合：为什么Spring要与“笨重”的Java EE共舞？

10 | Spring编程模型：Spring实现了哪些编程模型？

11 | Spring核心价值：我们能从Spring Framework中学到哪些经验和教训呢？

12 | 面试题精选


## 第二章：重新认识IoC (9讲)

13 | IoC发展简介：你可能对IoC有些误会？

控制反转（Inversion of Control，缩写为IoC），是面向对象编程中的一种设计原则，可以用来降低程序代码之间的耦合度。其中最常见的方式叫做依赖注入（Dependency Injection，简称DI），还有一种方式叫“依赖查找”（Dependency Lookup）。通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体将其所依赖的对象的引用传递给它。也可以说，依赖被注入到对象中。

IoC实际遵循的是DIP依赖倒置原则，上层模块不应该依赖于低层模块，二者应该通过抽象来依赖。Ioc把程序上层对下层的依赖转移到了第三方容器进行管理装配.


14 | IoC主要实现策略：面试官总问IoC和DI的区别，他真的理解吗？

15 | IoC容器的职责：IoC除了依赖注入，还涵盖哪些职责呢？

16 | 除了Spring，还有其它的IOC容器实现吗？

17 | 传统IoC容器实现：JavaBeans也是IoC容器吗？

Ioc 中的一个重要的应用，其实就是java beans

spring 与bean的关系：继承，依赖 引用。

其实提到IOC可以说是ioc容器，spring通过IOC容器来管理所有的java 对象及其相互间的依赖关系。

spring 通过IOC容器来管理依赖关系，ioc解决了各个对象之间不需要直接关联。开发者只需维护相对独立的各个对象代码即可。

IoC是一个过程，即对象定义及其依赖关系，其他与之配合的对象只能通过构造函数、工厂方法参数、从工厂方法构造或返回或setter的属性来定义依赖关系。然后IoC容器在创建bean时会注入这些依赖项。此过程在职责上是反转的，即先把原来代码中需要实现的对象创建、依赖的代码反转给容器来实现和管理，故称为控制反转。

所以，由上得出 spring创建bean来注入这些依赖项。spring来管理依赖关系，然后创建出来的容器就是bean了。


18 | 轻量级IoC容器：如何界定IoC容器的“轻重”？

19 | 依赖查找 VS. 依赖注入：为什么Spring总会强调后者，而选择性忽视前者？

依赖注入是一个程序设计模式和架构模型，也称控制反转。

在技术上来说依赖注入是一个控制反转的特殊事项，但依赖注入还指一个对象应用另外一个对象来提供一个它没有的功能。

如把一个数据库连接以参数的形式传到一个对象的结构方法里，而不是在那个对象内部自行创建一个连接。

控制反转的实现类型：依赖注入（Dependency Injection，DI）和依赖查找（Dependency Lookup）。

其中依赖注入应用较为广泛，spring就是采用此方式来实现控制反转的。


20 | 构造器注入 VS. Setter 注入：为什么Spring官方文档的解读会与作者的初心出现偏差？

21 | 面试题精选

## 第三章：Spring IoC容器概述 (9讲)

22 | Spring IoC依赖查找：依赖注入还不够吗？依赖查找存在的价值几何？

23 | Spring IoC依赖注入：Spring提供了哪些依赖注入模式和类型呢？

24 | Spring IoC依赖来源：依赖注入和查找的对象来自于哪里？

25 | Spring IoC配置元信息：Spring IoC有哪些配置元信息？它们的进化过程是怎样的？

26 | Spring IoC容器：BeanFactory和ApplicationContext谁才是Spring IoC容器？

27 | Spring应用上下文：ApplicationContext除了IoC容器角色，还提供哪些特性？

28 | 使用Spring IoC容器：选BeanFactory还是ApplicationContext？

29 | Spring IoC容器生命周期：IoC容器启停过程中发生了什么？

30 | 面试题精选

## 第四章：Spring Bean基础 (11讲)

1. 如何注册一个Spring Bean?
  
通过BeanDefinition和外部单体对象来注册

31 | 定义Bean：什么是BeanDefinition？

32 | BeanDefinition元信息：除了Bean名称和类名，还有哪些Bean元信息值得关注？

33 | 命名Spring Bean：id和name属性命名Bean，哪个更好？

34 | Spring Bean的别名：为什么命名Bean还需要别名？

35 | 注册Spring Bean：如何将BeanDefinition注册到IoC容器？

36 | 实例化Spring Bean：Bean实例化的姿势有多少种？

37 | 初始化Spring Bean：Bean初始化有哪些方式？

38 | 延迟初始化Spring Bean：延迟初始化的Bean会影响依赖注入吗？

39 | 销毁Spring Bean： 销毁Bean的基本操作有哪些？

40 | 回收Spring Bean：Spring IoC容器管理的Bean能够被垃圾回收吗？

41 | 面试题精选

## 第五章：Spring IoC依赖查找（Dependency Lookup） (9讲)

42 | 依赖查找的今世前生：Spring IoC容器从Java标准中学到了什么？

43 | 单一类型依赖查找：如何查找已知名称或类型的Bean对象？

44 | 集合类型依赖查找：如何查找已知类型多个Bean集合？

45 | 层次性依赖查找：依赖查找也有双亲委派？

46 | 延迟依赖查找：非延迟初始化Bean也能实现延迟查找？

47 | 安全依赖查找

48 | 内建可查找的依赖：哪些Spring IoC容器内建依赖可供查找？

49 | 依赖查找中的经典异常：Bean找不到？Bean不是唯一的？Bean创建失败？

50 | 面试题精选

## 第六章：Spring IoC依赖注入（Dependency Injection） (20讲)

DI和IoC区别？

IoC是一种设计原则，DI是IoC的一种实现方式（IoC不是Spring特有）

1. 有一点：“设置属性autowire candidate为false”，太明白是什么意思?

autowire-candidate属性是设置当前Bean是否为其他Bean autowiring候选者

2. 可以讲解下setter注入的原理吗,为什么注入顺序是不确定的，不是从上往下执行代码嘛?
  
并不是，由于Java反射API所返回的public方法热顺序并非定义顺序，所以无法控制先后情况。你可以自行尝试!

3. 构造器参数不会选择默认构造器，否则没有入口让Bean注入。通常spring Framework会尽可能地选择能够构造器参数注入的构造器。

4. 静态字段该怎么注入呢?
  
通常通过实例方法注入，然后再通过该方法注入到静态资源，还有一种比较常见， 通过ApplicationContextAware或BeanFactorIyAware来操作

5. 方法注入和Setter注入有什么不同?
  
Setter 注入是通过Java Beans来实现的，而方法注入则是直接通过Java反射来做的。当然底层都是Java反射~ 

6. 当任意Spring Bean实现类实现了BeanFactoryAware 接口时，在Bean生命周期回调时，会被容器调用setBeanFactory方法~

7. @Bean的方式通常属于半自动方式，许多关联Bean需要手动关联

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

51 | 依赖注入的模式和类型：Spring提供了哪些依赖注入的模式和类型？

52 | 自动绑定（Autowiring）：为什么Spring会引入Autowiring？

53 | 自动绑定（Autowiring）模式：各种自动绑定模式的使用场景是什么？

54 | 自动绑定（Autowiring）限制和不足：如何理解和挖掘官方文档中深层次的含义？

55 | Setter方法依赖注入：Setter注入的原理是什么？

56 | 构造器依赖注入：官方为什么推荐使用构造器注入？

57 | 字段注入：为什么Spring官方文档没有单独列举这种注入方式？

58 | 方法注入：方法注入是@Autowired专利吗？

不是

59 | 接口回调注入：回调注入的使用场景和限制有哪些？

60 | 依赖注入类型选择：各种依赖注入有什么样的使用场景？

61 | 基础类型注入：String和Java原生类型也能注入Bean的属性，它们算依赖注入吗？

62 | 集合类型注入：注入Collection和Map类型的依赖区别？还支持哪些集合类型？

63 | 限定注入：如何限定Bean名称注入？如何实现Bean逻辑分组注入？

64 | 延迟依赖注入：如何实现延迟执行依赖注入？与延迟依赖查找是类似的吗？

65 | 依赖处理过程：依赖处理时会发生什么？其中与依赖查找的差异在哪？

66 | @Autowired注入：@Autowired注入的规则和原理有哪些？

67 | JSR-330 @Inject注入：@Inject与@Autowired的注入原理有怎样的联系？

68 | Java通用注解注入原理：Spring是如何实现@Resource和@EJB等注解注入的？

69 | 自定义依赖注入注解：如何最简化实现自定义依赖注入注解？

70 | 面试题精选

## 第七章：Spring IoC依赖来源（Dependency Sources） (8讲)

71 | 依赖查找的来源：除容器内建和自定义Spring Bean之外，还有其他来源提供依赖查找吗？

72 | 依赖注入的来源：难道依赖注入的来源与依赖查找的不同吗？

73 | Spring容器管理和游离对象：为什么会有管理对象和游离对象？

74 | Spring Bean Definition作为依赖来源：Spring Bean的来源

75 | 单例对象作为依赖来源：单体对象与普通Spring Bean存在哪些差异？

76 | 非Spring容器管理对象作为依赖来源：如何理解ResolvableDependency？

77 | 外部化配置作为依赖来源：@Value是如何将外部化配置注入Spring Bean的？

78 | 面试题精选

## 第八章：Spring Bean作用域（Scopes） (9讲)

79 | Spring Bean作用域：为什么Spring Bean需要多种作用域？

80 | "singleton" Bean作用域：单例Bean在当前Spring应用真是唯一的吗？

不是

81 | "prototype" Bean作用域：原型Bean在哪些场景下会创建新的实例？

82 | "request" Bean作用域：request Bean会在每次HTTP请求创建新的实例吗？

83 | "session" Bean作用域：session Bean在Spring MVC场景下存在哪些局限性？

84 | "application" Bean作用域：application Bean是否真的有必要？

没太大必要

85 | 自定义Bean作用域：设计Bean作用域应该注意哪些原则？

86 | 课外资料：Spring Cloud RefreshScope是如何控制Bean的动态刷新？

87 | 面试题精选

## 第九章：Spring Bean生命周期（Bean Lifecycle） (18讲)

88 | Spring Bean 元信息配置阶段：BeanDefinition配置与扩展

89 | Spring Bean 元信息解析阶段：BeanDefinition的解析

90 | Spring Bean 注册阶段：BeanDefinition与单体Bean注册

91 | Spring BeanDefinition合并阶段：BeanDefinition合并过程是怎样出现的？

92 | Spring Bean Class加载阶段：Bean ClassLoader能够被替换吗?

93 | Spring Bean实例化前阶段：Bean的实例化能否被绕开？

94 | Spring Bean实例化阶段：Bean实例是通过Java反射创建吗？

95 | Spring Bean实例化后阶段：Bean实例化后是否一定被是使用吗？

96 | Spring Bean属性赋值前阶段：配置后的PropertyValues还有机会修改吗？

有

```java
public abstract class InstantiationAwareBeanPostProcessorAdapter implements SmartInstantiationAwareBeanPostProcessor {
    public PropertyValues postProcessProperties(PropertyValues pvs, Object bean, String beanName) throws BeansException {
        return null;
    }
}
```

97 | Aware接口回调阶段：众多Aware接口回调的顺序是安排的？

98 | Spring Bean初始化前阶段：BeanPostProcessor

99 | Spring Bean初始化阶段：@PostConstruct、InitializingBean以及自定义方法

100 | Spring Bean初始化后阶段：BeanPostProcessor

101 | Spring Bean初始化完成阶段：SmartInitializingSingleton

102 | Spring Bean销毁前阶段：DestructionAwareBeanPostProcessor用在怎样的场景?

103 | Spring Bean销毁阶段：@PreDestroy、DisposableBean以及自定义方法

104 | Spring Bean垃圾收集（GC）：何时需要GC Spring Bean？

105 | 面试题精选

## 第十章：Spring配置元信息（Configuration Metadata） (17讲)

106 | Spring配置元信息：Spring存在哪些配置元信息？它们分别用在什么场景？

107 | Spring Bean配置元信息：BeanDefinition

108 | Spring Bean属性元信息：PropertyValues

109 | Spring容器配置元信息

110 | 基于XML资源装载Spring Bean配置元信息

111 | 基于Properties资源装载Spring Bean配置元信息：为什么Spring官方不推荐？

112 | 基于Java注解装载Spring Bean配置元信息

113 | Spring Bean配置元信息底层实现之XML资源

114 | Spring Bean配置元信息底层实现之Properties资源

115 | Spring Bean配置元信息底层实现之Java注解

116 | 基于XML资源装载Spring IoC容器配置元信息

117 | 基于Java注解装载Spring IoC容器配置元信息

118 | 基于Extensible XML authoring 扩展Spring XML元素

119 | Extensible XML authoring扩展原理

120 | 基于Properties资源装载外部化配置

121 | 基于Yaml资源装载外部化配置

122 | 面试题

第十一章：Spring资源管理（Resources） (11讲)

123 | 引入动机：为什么Spring不使用Java标准资源管理，而选择重新发明轮子？

124 | Java标准资源管理：Java URL资源管理存在哪些潜规则？

125 | Spring资源接口：Resource接口有哪些语义？它是否“借鉴”了SUN的实现呢？

126 | Spring内建Resource实现：Spring框架提供了多少种内建的Resource实现呢？

127 | Spring Resource接口扩展：Resource能否支持写入以及字符集编码？

128 | Spring资源加载器：为什么说Spring应用上下文也是一种Spring资源加载器？

129 | Spring通配路径资源加载器：如何理解路径通配Ant模式？

130 | Spring通配路径模式扩展：如何扩展路径匹配的规则？

131 | 依赖注入Spring Resource：如何在XML和Java注解场景注入Resource对象？

132 | 依赖注入ResourceLoader：除了ResourceLoaderAware回调注入，还有哪些注入方法？

133 | 面试题精选

## 第十二章：Spring国际化（i18n） (5讲)

134 | Spring国际化使用场景

135 | Spring国际化接口：MessageSource不是技术的创造者，只是技术的搬运工？

136 | 层次性MessageSource：双亲委派不是ClassLoader的专利吗？

137 | Java国际化标准实现：ResourceBundle潜规则多？

138 | Java文本格式化：MessageFormat脱离Spring场景，能力更强大？