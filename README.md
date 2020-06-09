# dubbo-mall
基于dubbo的下单扣减库存的通用电商业务逻辑，同时保证分布式数据一致性

电商的下单扣减库存，取消恢复库存。这一看似简单的逻辑背后的数据一致性，微服务治理，高可用的保证还是十分复杂的！
先简述下本框架所使用的业务架构:
Dubbo+Zookeeper+Apollo+Redis+Rabbitmq+Springboot+Maven+Mysql（是不是很分布式的一套框架！但是整合在一起，各司其职，各尽所能才是复杂的，就像TeamLeader需要管理好Follows一样！）
## Dubbo
## Zookeeper
## Apollo
## Redis
## Rabbitmq
