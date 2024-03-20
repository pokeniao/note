---
日期: 
tags:
  - 问题错题
---
# 函数例题
## 通过数据库来生成，一个六位数的随机验证码
```sql
Select lpad(round(rand()\*1000000),6,'0');
```


# 子查询和连接
## update多行数据关联
1. 题目：我要修改carcare_services中的Type_id字段，条件是carcare_services的Type_name=carcare_types的name
```sql
UPDATE carcare_services
JOIN carcare_type on carcare_services.Services_Type =carcare_type.Type_NAME
SET carcare_services.services_type_id = carcare_type.id;
```
解题思路：既然要用到2个表，我们在==引入的时候就关联上2个表==，而不是在where中
