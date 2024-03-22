---
日期: 2024-03-21
tags:
  - 开发经验
aliases:
  - 后端开发
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
**==推荐使用LocalDateTime==** ，LocalDate、LocalTime,他们都是不可变的需要通过调用方法返回新的对象类似String
1. **获得当前时间**
LocalDateTime currentTime = LocalDateTime.now();
```java fold:获得其他详细
    public static void main(String[] args) {
    	// 当前时间
        LocalDateTime nowDateTime = LocalDateTime.now();
        System.out.println("今天是：" + nowDateTime);
        System.out.println("年：" + nowDateTime.getYear());
        System.out.println("月：" + nowDateTime.getMonthValue());
        System.out.println("日：" + nowDateTime.getDayOfMonth());
        System.out.println("时：" + nowDateTime.getHour());
        System.out.println("分：" + nowDateTime.getMinute());
        System.out.println("秒：" + nowDateTime.getSecond());
        System.out.println("纳秒：" + nowDateTime.getNano());
        System.out.println("当年的第" + nowDateTime.getDayOfYear() + "天");
        System.out.println("星期（单词）" + nowDateTime.getDayOfWeek());
        System.out.println("星期（数字）" + nowDateTime.getDayOfWeek().getValue());
        System.out.println("月份（单词）" + nowDateTime.getMonth());
        System.out.println("月份（数字）" + nowDateTime.getMonth().getValue());
    }
-------获取LocalDate或LocalTime
    public static void main(String[] args) {
        LocalDateTime nowTime = LocalDateTime.now();
        LocalDate localDate = nowTime.toLocalDate();
        LocalTime localTime = nowTime.toLocalTime();
        System.out.println("nowTime: " + nowTime);//2024-03-07T16:01:07.551
        System.out.println("localDate: " + localDate);//2024-03-07
        System.out.println("localTime: " + localTime);//16:01:07.551
    }

```
2. **时间加减**/**对象操作**
	- 加：LocalDateTime newTime = currentTime.plusMinutes(15);
	- 减：LocalDateTime pastTime = currentTime.minusMinutes(15);
3. **比较时间**
>==当前时间==大于==过去时间==15分钟 **或** ==过去时间==大于==当前时间==15分钟： currentTime.isAfter(pastTime.plusMinutes(15)）

| 方法                                                   | 说明             |
| ---------------------------------------------------- | -------------- |
| withYear,...,withHour,withMinute,withSecond,withNano | 修改时间，返回对象      |
| plusHour,plusMinutes,plusSeconds,plusNanos           | 加时间，返回对象       |
| minusHour,minusMinutes,minusSeconds,minusNanos       | 减时间，返回对象       |
| equals,isBefore,isAfter                              | 判断时间，是否相等或在前或后 |

1. **输出格式** `DateTimeFormatter.ofPattern`
>LocalDateTime newTime = LocalDateTime.now();
>DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
  String formattedTime = newTime.format(formatter);

5. **格式转换**
*Date转LocalDateTime*:
>LocalDateTime createDateTime = LocalDateTime.ofInstant(ticket.getCreateDate().toInstant(), ZoneId.systemDefault());

> [!Tip]- 解释
> Instant 时间戳: 它可以精确到纳秒级别，并且不依赖于时区。



# json转数组
Gson gson = new Gson();  
HashMap hashMap = gson.fromJson(response.getBody(), HashMap.class);