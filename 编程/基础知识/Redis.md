---
日期: 2024-03-24
tags:
  - 快速开始
  - 基本语法
  - NoSQL
---
# 分布式锁
```java
@Autowired  
private RedissonClient redissonClient;
```

```java
String key = "CarcareServices::" + servicesId;  
	//获得锁->锁用一个服务的扣减  
	RLock lock = redissonClient.getLock(key);  
	try {  
	boolean b = lock.tryLock(2, TimeUnit.SECONDS);  
		if(b){}  
	} catch (InterruptedException e) {  
		throw new RuntimeException(e);  
	}finally {  
		lock.unlock();  
	}
```