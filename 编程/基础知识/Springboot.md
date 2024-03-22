---
日期: 2024-03-23
tags:
  - 快速开始
---
# 定时任务
## SpringTask(全局定时任务)
1. SpringApplication 加上@EnableScheduling
2. 创建一个全局定时任务组件
```java fold:定时任务每30秒执行
@Component  
public class Task {  
	@Scheduled(cron = "0/30 * * * * ?")  
	public void task() {  
	log.info("定时任务执行");  
	}  
}
```

