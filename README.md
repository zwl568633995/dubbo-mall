# 做程序员不易，熬夜coding更不易，给个小星星Strar吧

# dubbo-mall
基于dubbo的下单扣减库存的通用电商业务逻辑，同时保证分布式数据一致性

电商的下单扣减库存，取消恢复库存。这一看似简单的逻辑背后的数据一致性，微服务治理，高可用的保证还是十分复杂的！
先简述下本框架所使用的业务架构:
### Dubbo+Zookeeper+Apollo+Redis+Rabbitmq+Springboot+Maven+Mysql（是不是很分布式的一套框架！但是整合在一起，各司其职，各尽所能才是复杂的，就像TeamLeader需要管理好Follows一样！）
相关接口地址配置：
zookeeper:127.0.0.1:2181 127.0.0.1:2182 127.0.0.1:2181
redis:127.0.0.1:6379
rabbitmq:127.0.0.1:5672
apollo/eureka:127.0.0.1:8080

## Dubbo
   高性能的RPC框架，注册中心基于Zookeeper，本系统采用了3个ZK的集群，保证高可用！
   采用Dubbo作为RPC框架还是其高性能所吸引，底层的通信框架采用的netty，性能绝壁好！
   切记，采用Dubbo最为RPC框架，所有的诸如domain,dto实体都需要继承Serializable接口，实现序列化！
## Zookeeper
   本Dubbo框架采用的注册中心是Zookeeper，上述也说到了，采用了3个zk保证高可用！在真实项目中，至少也需要5台吧！
   在本系统中，zk仅作为注册中心注册服务url。
## Apollo
   通用配置中心，暂未用上，业务集成肯定需要的！
   携程的Apollo框架自带的注册中心是Euraka,建议源码改为Zookeeper，因为本项目首先注册中心用的ZK,再者上述也说到了zk的通信框架采用的也是netty，追求性能极    致！
## Redis
   项目因为复杂度不是很高，暂时配置中心和redis使用不是很多。
   本项目用的分布式ID生成用到了redis，本框架提供了2中分布式id生成的方式：一是通用的SnowFlake(雪花算法64位)，二是Redis自增id(真实电商项目不建议用自增    id作为订单号，容易看出订单量)
## Rabbitmq
   消息队列承载业务流！本框架用到的主要是延迟队列，规定时间内订单未付款，扔到延迟队列消费，取消锁住的库存！
