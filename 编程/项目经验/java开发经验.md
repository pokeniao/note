---
日期: 2024-03-21
tags:
  - 常用指令
aliases: []
---
# 复制类
```java
BeanUtils.copyProperties(复制对象,目标对象);
```

# 金钱操作
使用`BigDecimal`进行金额计算
1. 创建一个 new BigDecimal(`数值`);

| 方法       | 作用  | 例子                  |
| -------- | --- | ------------------- |
| add      | 加   | num1.add(num2)      |
| subtract | 减   | num1.subtract(num2) |
| multiple | 乘   | num1.multiple(num2) |
| divide   | 除   | num1.divide(num2)   |
