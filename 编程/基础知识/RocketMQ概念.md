---
日期: 2024-03-21
aliases:
  - 消息队列
  - MQ
tags:
  - 中间件
---
[[MQ消息队列]]
[基本概念 | RocketMQ (apache.org)](https://rocketmq.apache.org/zh/docs/introduction/02concepts)
# 主题Topic
消费者==消费的对应消息==
![[Pasted image 20240321231334.png]]
# 队列(Queue)
一个主题可以有多个队列
一个Queue只能被一个==消费者组==消费
![[Pasted image 20240321231605.png]]



# 消费者获取信息方式
**Push** :
**pull** :