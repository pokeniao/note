---
日期: 2024-03-17
tags:
  - 快速开始
---
# 基础指令使用

1. 构建本地仓库： git init
2. 1. 查看上传版本的信息：
	- git log
	- git reflog (精简的)
2. 回退版本： git reset --hard `版本id`
3. 查看当前的状态：git status
4. 分支
	1. 查看分支 git branch -v
	2. 创建分支 git branch `分支名`
	3. 切换分支 
		- git checkout `分支名`
		- git checkout -b `分支名` （没有创建并跳转，有跳转）
	4. 合并分支 git merge `分支名`
	5. 删除分支 
		- git branch -d `分支名`（需要检查）
		- git branch -D `分支名`（强制删除）

- **暂存区**
	1. 添加到暂存区： git add `.`
	2. 从暂存区和工作区中移除：git rm `.删除内容`
	3. 从暂存区中移除：git rm --cached `.删除内容`
	4. *暂存区替换工作区（危险）：* git checkout `.`
- **本地仓库**
	1. 获取本地仓库到暂存区：git reset HEAD
	2. 提交到本地仓库：git commit -m `描述信息`
- **远程库**
	- ***添加远程库***
	1. 添加远程库: git remote add `定义仓库名可以为gitee或githup（一般默认origin）` `仓库地址`[^仓库地址为]
	2. 查看绑定远程库：git remote show 或 git remote -v
	- ***操作远程库***
	1. 从远程库抓取到本地：git fetch `远程仓库名` `分支名` 如果不指定远程名和分支，则抓取所有		1. 从远程库抓取并合并到本地：git pull `远程仓库名` `分支名` 
	2. 推送到远程：git push -u `远程仓库名gitee或githup(一般默认origin)` `分支` 
		(-u上传并结合）
		强制推送：git push -u `远程仓库名gitee或githup(一般默认origin)` `分支`  --force
	3. 克隆：git clone `仓库路径` `本地目录`

[^仓库地址为]: http https://gitee.com/a1625229957/car-care.git 或ssh方式 git@gitee.com:a1625229957/note.git。http方式需要登入，ssh不需要登入，但要绑定ssh [[#关联远程仓库账号]]
# 分支冲突
原因：上传到远程时，`merge`合并分支时同一个文件位置（行）有2中不同的更改，git不能判断，需要我们手动解决。

解决：在远程仓库下冲突
1. 先提交当前`commit `，然后`pull`下后会开启一个（master|Merging）
> [!NOTE]- 提示我们错误，要手动处理冲突的文件
> ``` 
From github.com:1625229957/note
 branch            master     -> FETCH_HEAD
Auto-merging 笔记/.obsidian/workspace.json
Auto-merging 笔记/编程/通用学习/git.md
CONFLICT (content): Merge conflict in 笔记/编程/通用学习/git.md
Automatic merge failed; fix conflicts and then commit the result.
> ```

2. 打开文件，然后找到标记了冲突的部分，它通常会以`<<<<<<< HEAD`  `这里是pull内容` `==== `   `本地内容` `>>>>>>>>>>>>>>>>字符串` ，我们进行修改。修改完后提交。
3. 最后推送
# 关联远程仓库账号
## github与gitee
1. 配置本地用户信息（电脑配置一次即可）：
```
git config --global user.name "pokeniao"
git config --global user.email "1625229957@qq.com"
```

2. SSH关联
	1.通过 `ssh-keygen -t rsa` 获取SSH公钥, 注意：如果存在会覆盖
		通过 `cat ~/.ssh/id_rsa.pub` 查看
	2.复制ssh到gitee或github上关联
	3.通过 `ssh -T git@gitee.com` 或 `ssh -T git@github.com` 查看是否成功关联
## 远程提交忽略 
.gitignore
 \*/`文件名` ： 表示任意名为`文件名`的文件夹忽略
 `文件`： 表示忽略根目录下的`文件`



# Git工作流程图
![[Pasted image 20240317205948.jpg]]