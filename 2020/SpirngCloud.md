# Spring Cloud

## Spring Cloud Commons

1. Spring Cloud Context 应用上下文相关，

spring cloud 应用中创建一个 bootstrap context，她是作为了主应用的 parent context ；主要负责从外部资源（分布式配置）
加载配置以及在解码本地的配置文件。

application context 和 bootstrap context 共享了相同Environment. 默认情况下，bootstrap properties(从配置中心加载的属性) 
有更高的优先级，所以它们不能被本地的配置所覆盖。

bootstrap context使用了和主应用的 context 不同的配置方式，使用的是 bootstrap.yml 而不是 application.yml，
这主要是为了保证两个context的配置可以很好的分离；


2. Spring Cloud Commons

抽象

## Spring Cloud GateWay

底层是netty