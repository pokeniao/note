---
日期: 2024-03-21
aliases:
  - 消息队列
tags:
  - 中间件
  - 快速开始
---
下载zip包到linux安装
```
$ unzip rocketmq-all-5.2.0-source-release.zip  
$ cd rocketmq-all-5.2.0-source-release/
```
[RocketMQ · 官方网站 | RocketMQ (apache.org)](https://rocketmq.apache.org/zh/)

64位操作系统，推荐 Linux/Unix/macOS
使用环境： jdk8+
# 配置
1. 运行内存占用空间：`rocketmqe\bin\runbroker.sh` 
```sh
# JAVA_OPT="${JAVA_OPT} -server -Xms8g -Xmx8g"
JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx256m"
```
2. windows只能jdk8: `bin/runserver.cmd` 和``bin/runbroker.cmd` 添加在最上面
```
set JAVA_HOME=C:\Users\admin\.jdks\corretto-1.8.0_382\jre 
set PATH=%JAVA_HOME%\bin;%PATH%
```
# 启动MQ
## linux
```
# 在 RocketMQ 的 bin 目录下执行
nohup sh mqnamesrv &
nohup sh mqbroker -n localhost:9876 &
```

> [!Success]- 成功反馈
> 我们可以在namesrv.log 中看到 **'The Name Server boot success..'，** 表示NameServer 已成功启动。

## window
1. 启动
>第一步：进入到bin目录
start mqnamesrv.cmd
或者 双击 mqnamesrv.cmd
第二步：start mqbroker.cmd





# 使用MQ
1. 导入依赖
```xml
<dependency>  
<groupId>org.apache.rocketmq</groupId>  
<artifactId>rocketmq-spring-boot-starter</artifactId>  
<version>2.3.0</version>  
</dependency>
```
2. 配置application.yml
```java
rocketmq:  
	name-server: http://localhost:9876  
  # Producer 生产者
  producer:
    group: my-group  # 指定发送者组名
    send-message-timeout: 3000 
    # 发送消息超时时间，单位：毫秒。默认为 3000 。
    compress-message-body-threshold: 4096 
    # 消息压缩阀值，当消息体的大小超过该阀值后，进行消息压缩。默认为 4 * 1024B
    max-message-size: 4194304
     # 消息体的最大允许大小。。默认为 4 * 1024 * 1024B
    retry-times-when-send-failed: 2 
    # 同步发送消息时，失败重试次数。默认为 2 次。
    retry-times-when-send-async-failed: 2
     # 异步发送消息时，失败重试次数。默认为 2 次。
    retry-next-server: false
     # 发送消息给 Broker 时，如果发送失败，是否重试另外一台 Broker 。默认为 false
```

## 发送者
**普通消息:**
无返回值，只负责发送消息⽽不等待服务器回应且没有回调函数触发
rocketMQTemplate.convertAndSend(`主题` ,`消息`)

延迟级别从1到18分别对应了1s 5s 10s 30s 1m 2m 3m 4m 5m 6m 7m 8m 9m 10m 20m 30m 1h 2h
**同步消息**:
同步消息有返回值SendResult，等到消息发送成功后才算结束。
		**定时任务**
		`rocketMQTemplate.syncSend(String destination, Message<?> message, long timeout, int delayLevel)中的delayLevel参数设置了延迟的级别。`
**异步消息**
	异步消息无返回值，需要传入回调类。无需等待消息是否发送成功。

```java fold:代码
@Resource  
private RocketMQTemplate rocketMQTemplate;
/**
     * 普通字符串消息
     */
    public void sendMessage() {
        String json = "普通消息";
        rocketMQTemplate.convertAndSend("sendMessage", json);
    }

    /**
     * 同步消息
     */
    public void syncSend() {
        String json = "同步消息";
        SendResult sendMessage = rocketMQTemplate.syncSend("sendMessage", json);
        System.out.println(sendMessage);
    }

    /**
     * 异步消息
     */
    public void asyncSend() {
        String json = "异步消息";
        SendCallback callback = new SendCallback() {
            @Override
            public void onSuccess(SendResult sendResult) {
                System.out.println("123");
            }

            @Override
            public void onException(Throwable throwable) {
                System.out.println("456");
            }
        };
        rocketMQTemplate.asyncSend("sendMessage", json, callback);
    }

    /**
     * 单向消息
     */
    public void onewaySend() {
        String json = "单向消息";
        rocketMQTemplate.sendOneWay("sendMessage", json);
    }
    /**
     * 同步消息定时
     */
	public void syncSendDelay(String topic, Object message, long timeout, int delayLevel) 
	{ 
	rocketMQTemplate.syncSend(
	topic, MessageBuilder.withPayload(message).build(), 
	timeout, delayLevel);
	}
	/**
	*异步延迟消息
	*/
	public void asyncSendDelay(String topic, Object message, long timeout, int delayLevel) 
	{ 
	rocketMQTemplate.asyncSend(topic, MessageBuilder.withPayload(message).build(), 
	new SendCallback() { 
		@Override public void onSuccess(SendResult sendResult) 
		{ log.info("异步发送延时消息成功"); }
		 @Override public void onException(Throwable throwable) 
		 { log.error("异步发送延时消息发生异常"); } 
	 }, 
	 timeout, delayLevel); 
	}

  
  
```

## 接收者
```java
@Service  
@RocketMQMessageListener(consumerGroup = "分组名",topic = "主题名")  
public class AlipayPayConsumer implements RocketMQListener<MessageExt> {  
  
@Override  
public void onMessage(MessageExt messageExt) {  
//接受消息  
byte[] body = messageExt.getBody();  
String s = new String(body);
}  
}
```
