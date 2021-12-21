# Spring AOP

## Spring AOP设计目标

Spring AOP事实上有三部分组成

* 一个是通过Java动态代理
* 一个是通过像字节码提升
* 通过Aspect整合

JDK动态代理实现-基于接口代理
CGLIB动态代理实现-基于类代理(字节码提升)
AspectJ适配实现


### AopProxy

它通过getProxy方法去返回或新建一个new一个object

这里有两个重载方法,一个是带ClassLoader,一个是不带ClassLoader,带ClassLoader就是什么就相当于说指定ClassLoader下面的一个类，然后产生一个代理对象。
没有带它就利用当前线程所关联的应用上下文ClassLoader。

当判断目标对象，接口JDK动态代理，如果是一个类就变成了CGLIB的一个字节码提升。

Aspect整合

### 为什么 Proxy.newProxyInstance 会生成新的字节码

JDK

生产代码实现了传递进去的接口，继承Proxy API，传递进去InvocationHandler实现，相当于动态代理自己创建。

性能损耗一般

### 为什么 Java 动态代理无法满足 AOP 的需要？

类可以用字节码提升的手段做这个事情。运行是创建新的class。

两个内部依赖的框架

CGLIB Enhancer API
ASM 底层操作

性能损耗更大

## 问: Spring AOP和AspectJ AOP存在哪些区别?

答:
* AspectJ是AOP完整实现，Spring AOP则是部分实现
* Spring AOP比AspectJ使用更简单
* Spring AOP整合AspectJ注解与Spring IoC容器↑
* Spring AOP仅支持基于代理模式的AOP
* Spring AOP仅支持方法级别的Pointcuts


## AspectJ

如果在一个aspect里面，around通常来说是在before之前。

如果在不同aspect里面，根据Ordered的情况来决定。

每一次的pointcut，它是筛选出一个JoinPoint，一个JoinPoint对应的是一个方法的拦截执行，方法拦截执行里面有around/before/after动作。


