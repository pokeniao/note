---
日期: 2024-03-19
tags:
  - 问题错题
  - bug
---

# github
## push问题
### 修改用户名后问题
- [x] 解决 ✅ 2024-03-19
github修改username后出现,无法提交问题：
```
! [remote rejected] master -> master (failure)
```
**解决方法：** 删除库.git文件，出现创建init

### 无法提交问题：
- [x] 解决 ✅ 2024-03-19
```
! [remote rejected] master -> master (push declined due to repository rule violations)
```
**原因：** github的校验到文件中带有token等。
**解决方法：** 删掉token
- [x] 解决 ✅ 2024-03-19
```
! [remote rejected] master -> master (fetch first)
```
**原因：** 发生了冲突
**解决方法：** [[git#分支冲突|分支冲突解决]]
