---
tags:
  - 软件使用
日期: 2024-03-29
---

# 安装node用nvm或直接网页安装
在 [Node官网](https://nodejs.org/zh-cn/) 上，下载对应的安装包
# 默认安装模块位置
若不进行环境变量配置，那么在使用命令安装 `node.js全局模块` （如：npm install -g vue）时，会默认安装到C盘的路径 (`C:\Users\hua\AppData\Roaming\npm`) 中
- 因此，需要配置 **全局安装模块 `node_global`** 以及 **缓存目录 `node_cache`** 的环境变量；