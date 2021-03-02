# SpringBoot + k8s 项目学习

## 微服务

1.分而治之
2.单一职责
3.关注分离

### Dubbo、Spring Cloud和K8s横向比对

||Dubbo|Spring Cloud|K8s|
|:--:|:--:|:--:|:--:|
|服务发现和LB|ZK/Nacos + Client|Eureka + Ribbon|Service|
|API网关|NA|Zuul|Ingress|
|配置管理|Diamond/Nacos|Spring Cloud Config|ConfigMaps/Secrets|
|容错限流|Sentinel|Hystrix|HealthCheck/Probe/ServiceMesh|
|日志监控|ELK|ELK|EFK|
|Metrics监控|Dubbo Admin/ Monitor| Actuator/MicroMeter + Prometheus|Heapster+Prometheus|
|调用链监控|NA|SpringCloud Sleuth/ zipkin|Jaeger/Zipkin|

### Dubbo、Spring Cloud和K8s横向比对

||Dubbo|Spring Cloud|K8s|
|:--:|:--:|:--:|:--:|
|应用打包|Jar/War|Uber Jar/War|Docker Image/Helm|
|服务框架|Dubbo RPC|Spring(Boot) REST|框架无关|
|发布和调度|NA|NA|Scheduler|
|自动伸缩和自愈|NA|NA|Scheduler/AutoScaler|
|进程隔离|NA|NA|Docker/Pod|
|环境管理|NA|NA|Namespace/Authorization|
|资源配额|NA|NA|CPU/Mem Limit, Namespace Quotas|
|流量治理|ZK + Client|NA|ServiceMesh|


### 优劣比对

||Dubbo|Spring Cloud|K8s|
|:--:|:--:|:--:|:--:|
|亮点|阿里背书 成熟稳定 RPC高性能 流量治理|Netflix/Pivotal背书 社区活跃 开发体验好 抽象组件化好|谷歌背书 平台抽象 全面覆盖微服务关注点(发布) 语言栈无关 社区活跃|
|不足|耦合性高 JVM only|JVM only 运行耗资源|偏DevOps和运维 重量复杂 技术门槛高|

## 网关生产扩展点

* 限流熔断
* 动态路由和负载均衡
* 基于Path的路由
  * api.xxx.com/pathx
* 截获器链
* 日志采集和Metrics 埋点
* 响应流优化

*** 主流开源网关概览

||支持公司|实现语言|亮点|不足|
|:--:|:--:|:--:|:--:|
|Nginx(2004)|Nginx Inc|C/Lua|高性能，成熟稳定|门槛高，偏运维，可编程弱|
|Kong (2014)|Kong Inc|OpenResty/Lua|高性能，可编程API|门槛较高|
|Zuul1(2012)|Netflix/ Pivotal|Java|成熟 简单门槛低|性能一般，可编程一般|
|Spring Cloud Gateway(2016)|Pivotal|Java|异步，配置灵活|早期产品|
|Envoy(2016)|Lyft|C++|高性能，可编程API/ServiceMesh集成|门槛较高|
|Traefik(2015)|Containous|Golang|云原生，可编程API/对接各种服务发现|生产案例不多|

