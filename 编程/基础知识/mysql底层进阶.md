---
日期: 2024-03-18
tags:
  - SQL
  - 底层原理
  - 基本概念
---

# [[mysql]]的体系结构
- 连接层
	-和客户端进行连接服务，包括授权认证等
- 服务层
	-大多数核心服务，sql接口，优化，缓存。跨存储引擎的功能实现，如：过程，函数
- 引擎层（更具不同引擎有所不同）
	-负责数据的存储提取,由具体的存储引擎决定
- 存储层
	-存储数据在文件系统，并于存储引擎交互
![[Pasted image 20240318201553.png]]

# 存储引擎
描述：存储引擎是存储数据，建立索引，更新/查询数据等技术实现。存储引擎是基于表的而不是基于库的。
### Innodb
特点：
	1. [[mysql#^8ff1f1|DML]]操作遵循[[mysql面试题#3.数据库事务的特性（ACID）|ACID]]模型，支持事务
	2. 行级锁
	3. 支持外键
# 索引
