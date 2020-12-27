## 注册中心

### Spring Cloud Eureka

#### 特点

* Spring Cloud背书
  * 推荐服务发现方案
* CAP理论
  * AP模型，数据最终致
* 简单易用
  * 开箱即用，控制台管理
  
* 内存限制
  * 客户端上报完整注册信息，造成服务端内存浪费
* 单一调度更新
  * 客户端简单轮训更新， 增加服务器压力
* 集群伸缩性限制
  * 广播式复制模型，增加服务器压力

### Spring Cloud Zookeeper

* 成熟协调系统
  * Dubbo、Spring Cloud等适配方案
* CAP理论
  * CP模型，ZAB算法，强数据一致性

* 维护成本
  * 客户端、Session 状态、网络故障
* 伸缩性限制
  * 内存、GC,连接

### Spring Cloud Consul

* 通用方案
  * 适用于Service Mesh、Java生态
* CAP理论
  * AP Raft+ Gossip 数据最终一致

* 可靠性无法保证
  * 未经过大规模验证
* 非Java生态
  * 维护和问题排查困难

### Alibaba Nacos Discovery

|技术选型|CAP模型|适用规模(建议)|控制台管理|社区活跃|
|:--:|:--:|:--:|:--:|:--:|
|Eureka|AP|< 30K|支持|低|
|Zookepper|CP|< 20K|不支持|中|
|Consul|AP|< 5K|支持.|高|
|Nacos|AP|100K +|支持|靠大家啦|

使用
* 下载注册中心
* 启动注册中心
* 增加三方依赖
* 外部化配置
* 激活服务发现
* 检验服务发现

Nacos服务器
https:/github.com/alibaba/nacos/releases
命令行启动
sh startup.sh -m standalone
org.springframework.cloud 
spring-cloud-tarter-alibaba-nacos-discovery
application.properties
spring.loud.nacos.discovery.server-addr-127.0.0.1.8848 
@EnableDiscoveryClient
SpringApplication.run 
已注册实例
http://127.0.0.1:8848/v1/ns/instances?serviceName=service-consumer


## Spring Cloud Commons 抽象原理

* 激活注册 @EnableDiscoveryClient
* 服务注册 ServiceRegistry、Registration
* 负载均衡 Ribbon Server、ServerList
* Actuator HealthIndicator、@Endpoint 

https://github.com/nacos-group/nacos-spring-project
https://github.com/nacos-group/nacos-spring-boot-project
https://github.com/spring-cloud-incubator/spring-cloud-alibaba


## Config

http://localhost:12345/application-default.properties
http://localhost:12345/app1-dev.properties

## Spring Cloud Context抽象配置相关

* Spring Environment

EnvironmentManager

* Bean动态刷新
@RefreshScope

* Spring应用上下文
RefreshScope
ContextRefresher
scope-refresh

* Spring Boot Actuator
EnvironmentEndpoint
WritableEnvironmentEndpoint
RefreshEndpoint


* Spring Cloud事件
EnvironmentChangeEvent
RefreshEvent


2.0 
management.endpoints.web.exposure.include = *
http://localhost:12345/actuator

http://127.0.0.1:8848/nacos/v1/cs/configs


http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos-config-exampleroperties&group=DEFAULT_GROUP

## Spring Cloud Alibaba Sentinel 

Spring Cloud服务熔断现状- Hystrix

* 熔断模式
  * 服务超时( Timeout )
  * 信号量( Semaphore )
* 编程模型
  * 面向接口( Interface )
  * 面向注解( Annotation )
* 策略规则
  * 自定义实现
  * 注解配置
  * 多数据源适配
* 控制台
  * Hystrix Dashboard
* 生态整合
  * JVM进程服务
  * RPC服务
  * Spring Cloud Stack等

### Alibaba Sentinel

* 隔离策略 信号量隔离
* 熔断降级策略 基于响应时间或失败比率
* 实时指标实现 滑动窗口
* 规则配置 支持多种数据源
* 扩展性 多个扩展点
* 基于注解的支持 支持
* 限流 基于QPS,支持基于调用关系的限流
* 流量整形 支持慢启动、匀速器模式
* 系缩负载保护 支持
* 控制台 开箱即用，可配置规则、查看秒级监控、机器发现等
* 常见框架的适配 Servlet、Spring Cloud、Dubbo、 gRPC等

### Sentinel是什么

随着微服务的流行，服务和服务之间的稳定性变得越来越重要。Sentinel是面向分布
式服务架构的轻量级流量控制框架，主要以流量为切入点，从流量控制、熔断降级、
系统负载保护等多个维度来帮助您保护服务的稳定性。

* 限流
* 流量整形
* 熔断降级
* 系统保护

流量控制有以下几个角度:
* 资源的调用关系，例如资源的调用链路，资源和资源之间的关系;
* 运行指标，例如QPS、线程池、系统负载等;
* 控制的效果，例如直接限流、冷启动、排队等。

## Spring Cloud Stream

* Destination Binders
* Destination Bindings
* Message 

source
Sink

Processor =Source + Sink


类比
@Function = @Supplier + @Consumer


## Spring Cloud Bus Alibaba
技术基础
* Spring Environment抽象
* Spring Event/Listener 机制
* Spring Annotation-Driven 
* Spring Boot Externalized Configuration 
* Spring Boot Actuator
* Spring Cloud Context抽象
* Spring Cloud Stream抽象


Spring Cloud Bus用轻量级消息代理连接分布式系统的节点。然后，该代理可以用于广播状态更改(例如配置更改)
或其他管理指令。一个关键的想法是，总线就像Spring Boot应用程序的分布式执行器，可以向外扩展。然而,
它也可以作为应用程序之间的通信通道。这个项目提供了AMQP broker或Kafka作为传输的启动器。

分布式更新