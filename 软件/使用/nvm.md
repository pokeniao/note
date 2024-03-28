---
tags:
  - 软件使用
日期: 2024-03-28
---
[window下安装并使用nvm_window安装nvm-CSDN博客](https://blog.csdn.net/HuangsTing/article/details/113857145)
# 安装

1. 去github [下载最新的 nvm](https://github.com/coreybutler/nvm-windows/releases) 找到 `nvm-setup.zip` 点击下载

2. 配置镜像
```
nvm npm_mirror https://npmmirror.com/mirrors/npm/
nvm node_mirror https://npmmirror.com/mirrors/node/
```

# 使用指令
1. 查看网络可以安装的版本`nvm list available` 
2. 安装`nvm install 14.14.0`
3. 使用`nvm use 14.14.0`
4. 查看已安装 `nvm list`
5. 卸载指定版本 `nvm uninstall`
