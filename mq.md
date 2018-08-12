## MQ
![对比](https://github.com/gaoyuanyuan2/notes/blob/master/img/3.png) 
### 1、好处
解耦、、安全可靠、异步、顺序保证、横向扩展。
### 2、RabbitMQ
![fanout](https://github.com/gaoyuanyuan2/notes/blob/master/img/4.png) 
### 3、Kafka
 1.集成Kafka
  <br>Kafka使用group.id分组消费者
  配置消息者参数group.id相同时对消息进行负载处理
  配置服务器partitions参数,控制同一个group.id下的consumer数量
  小于partitions
  Kafka只保证同一个partition下的消息是有序的

