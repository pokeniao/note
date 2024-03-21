---
日期: 2024-03-21
tags:
  - 基本语法
  - 常用指令
---
# 获得雪花算法
```java
Snowflake snowflake = IdUtil.getSnowflake(1, 1);  
String id = snowflake.nextIdStr();
```