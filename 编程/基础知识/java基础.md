---
日期: 2024-03-23
tags:
  - 基本语法
  - 快速开始
  - 基本概念
  - 常用指令
---
# 多线程
## 快速开始
1. 创建一个线程
	1. class继承Thread类，重写run 方法，通过new这个类.start()运行线程
	```java fold:run
	class Cat extends Thread{
		@Override
		public void run(){}
	}
	new Cat().start();
	```
	2. class实现Runnable接口，实现run方法，new Thread(class)
## 线程的使用
