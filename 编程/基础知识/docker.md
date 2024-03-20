---
日期: 2024-03-20
tags:
  - 快速开始
---
# 基本指令
[容器具体运行参数和镜像查看dockerhub](https://hub.docker.com/)
**镜像**
1. 查看镜像：docker images
2. 下载镜像：
	1. 从网络拉取 docker pull
	2. 加载压缩包镜像 docker load
3. 删除镜像：docker rmi `镜像`
**容器** 
1. 查看容器：docker ps （所有运行的容器）
> [!success]- 参数
> - **-a :** 显示所有的容器，包括未运行的。
2. 创建容器运行容器：docker run --name `起一个容器名` -p `宿主机端口号`:`容器端口号`  -v `宿主机目录`:`容器内部目录` -d `镜像名`
> [!Success]- 参数解释
>1. [[Pasted image 20240320205706.png|宿主机与容器端口的关系图]] 外部连接连接到`宿主机端口`
>2. `-d` 表示后台运行容器
>3. `-v` 挂载数据卷 直接`:容器内部目录` 则会默认在/var/lib/docker/volumes/下
1. 进入容器： docker exec -it `容器名` `进入容器执行的指令`
	1. 从容器中退出：exit
> [!success]- 参数解释
>1. `-it` 允许我们与容器交互
4. 容器运行状态
	1. 运行：docker start `容器名`
	2. 暂停：docker pause`容器`
	3. 停止：docker stop `容器`
	4. 查看日志 docker logs （查看运行日志）
5. 删除容器：docker rm `容器名`
**数据卷**
1. 查看数据卷
	1. 查看指定 docker volume inspect `数据卷名`
	2. 查看全部 docker volume ls
2. 创建数据卷 docker volume create `数据卷名`
3.  删除数据卷
	1. 删除未使用 : docker volume prune
	2. 删除一个或多个：docker volume rm