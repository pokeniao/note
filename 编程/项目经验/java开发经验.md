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
# 时间
1. **获得当前时间**
LocalDateTime currentTime = LocalDateTime.now();
2. **时间加减**
	- 加：LocalDateTime newTime = currentTime.plusMinutes(15);
	- 减：LocalDateTime pastTime = currentTime.minusMinutes(15);
3. **输出格式**
>DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
  String formattedTime = newTime.format(formatter);
4. **比较时间**
>==当前时间==大于==过去时间==15分钟 **或** ==过去时间==大于==当前时间==15分钟： currentTime.isAfter(pastTime.plusMinutes(15)）
5. 格式转换
*Date转LocalDateTime*:
>LocalDateTime createDateTime = LocalDateTime.ofInstant(ticket.getCreateDate().toInstant(), ZoneId.systemDefault());


# json转数组
Gson gson = new Gson();  
HashMap hashMap = gson.fromJson(response.getBody(), HashMap.class);