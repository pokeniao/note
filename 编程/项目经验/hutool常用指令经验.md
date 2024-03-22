---
日期: 2024-03-21
tags:
  - 常用指令
  - 开发经验
---
# 获得雪花算法
```java
Snowflake snowflake = IdUtil.getSnowflake(1, 1);  
String id = snowflake.nextIdStr();
```