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

### 主流开源网关概览

||支持公司|实现语言|亮点|不足|
|:--:|:--:|:--:|:--:|
|Nginx(2004)|Nginx Inc|C/Lua|高性能，成熟稳定|门槛高，偏运维，可编程弱|
|Kong (2014)|Kong Inc|OpenResty/Lua|高性能，可编程API|门槛较高|
|Zuul1(2012)|Netflix/ Pivotal|Java|成熟 简单门槛低|性能一般，可编程一般|
|Spring Cloud Gateway(2016)|Pivotal|Java|异步，配置灵活|早期产品|
|Envoy(2016)|Lyft|C++|高性能，可编程API/ServiceMesh集成|门槛较高|
|Traefik(2015)|Containous|Golang|云原生，可编程API/对接各种服务发现|生产案例不多|


### jwt
|优势 |不足|
|:--:|:--:|
|紧凑轻量对AuthServer简化AuthServer实现 |压力小无状态和吊销无法两全传输开销|


## 测试

|分类|功能|
|:--:|:--:|
|单元测试|确保类、模块功能正确|
|集成测试|确保组件间接口、交互和链路正确|
|组件测试|确保微服务作为独立整体，接口功能正确|
|契约测试|确保服务提供方和消费方都遵循契约规范|
|端到端测试|确保整个应用满足用户需求|
|探索测试|手工探索学习系统功能，改进自动化测试|

## 配置中心

### Apollo VS Spring Cloud Config VS K8s ConfigMap

|对比项|Apollo|Spring Cloud Config|K8s ConfigMaps|
|:--:|:--:|:--:|:--:|
|配置界面|统一界面管理不同环境和集群配置|无，通过git操作|Cli或Dashboard|
|配置存储|DB|Git|Etcd |
|配置生效时间|实时推送+应用配合|近实时+应用配合|近实时+应用配合|
|动态配置|支持，实时推送|复杂+Mq|支持发布更新|
|版本管理|UI支持发布历史和回滚|无，通过git操作|无，需自己管理|
|灰度发布|支持|不支持|支持灰度发布|
|授权/审计/审核|UI操作，修改和发布权限分离|需通过git仓库设置|K8s平台部分支持|
|实例配置监控|可见哪些客户端配置生效|不支持|可查询容器环境变量|
|客户端支持|原生Java/.Net,提供API,支持Sprinq标注|Spring应用+标注支持|语言无关|

* Apollo动态配置
  * https://github.com/ctripcorp/apollo-use-cases
* SpringCloud集中配置
  * https://github.com/sqshq/piggymetrics/tree/master/config


## 调用链监控

### CAT VS Zipkin VS Skywalking
|对比项|CAT |Zipkin |Apache Skywalking|
|:--:|:--:|:--:|:--:|
|调用链可视化|有|有|有|
|聚合报表|非常丰富|少|较丰富|
|服务依赖图|简单|简单|好|
|埋点方式|侵入|侵入|非侵入，运行期字节码增强|
|VM指标监控|好|无|有|
|告警支持|有|无|有|
|多语言支持|Java/ .Net|丰富|Java/.Net/NodeJS/PHP自动|Go手动|
|存储机制|Mysql(报表),本地文件/HDFS (调用链)| 可选 in memory, mysql, ES(生产)，Cassandra(生产)|H2, ES(生产)|
|社区支持|主要在国内，点评/美团| 文档丰富，国外主流| Apache支持，国内社区好|
| 国内案例| 点评、携程、陆金所、拍拍贷| 京东、阿里定制不开源| 华为，小米，当当，微众银行|
| APM| Yes| No| Yes|
| 祖先源头| eBay CAL| Google Dapper| Google Dapper|
| 同类产品| 暂无| Uber Jaeger, Spring Cloud Sleuth| Naver Pinpoint|
| Github Stars(2019.6)| 9.6k| 11.2k| 9.2k|
| 亮点| 企业生产级，报表丰富| 社区社区生态好| 非侵入，Apache背书|
| 不足| 用户体验一般，社区一般| APM报表能力弱| 时间不长，文档一般，仅限中文社区|


## 云原生(Cloud Native)应用定义

基于微服务原理而开发的应用，以容器方式打包。在运行时,容器由运行于云基础设施之.上的平台进行调度。应用开发采用持续交付和DevOps实践。
