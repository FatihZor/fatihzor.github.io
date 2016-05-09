---
layout: post
title:  "Docker常用命令"
date:   2015-12-16 15:22:15
categories:  [Ruby]
tags:  [Docker]
---




###查看docker信息

首先通过下面命令检查Docker是否安装成功

	docker info
	docker version
	

###对image的操作(search,pull,images,rmi,history)
	
检索image
	
	docker search image_name

下载image
	
	docker pull image_name
	
列出镜像列表

	docker images
	
删除镜像

	docker rmi image_name
	
显示一个镜像历史

	docker history image_name
	

### 启动容器

	#列出正在运行的所有容器
	docker ps
	
	#列出所有的容器
	docker ps -a
	
	#列出最近一次启动的容器
	docker ps -l
	
###保存对容器的修改(commit)

	docker commit ID new_image_name
	
	
### 对容器的操作

	#删除所有的容器
	docker rm `docker ps -a -q`
	
	#删除单个容器
	docker rm Name/ID
	
	#停止、启动、杀死一个容器
	docker start Name/ID
	docker stop Name/ID
	docker kill Name/ID
	#从一个容器中获取日志
	docker logs Name/ID
	#重启一个正在运行的容器
	docker restart Name/ID
	#进入容器
	docker exec -it Name/ID /bin/bash
	
### 容器和主机之前的文件拷贝

	docker cp Name:/container_path to_path
	docker cp ID:/container_path to_path
	
### 在主机上重启docker服务

	service docker restart
	
### 保存和加载镜像

	docker save image_name -o file_path
	
	docker load -i file_path
	
	#机器a
	docker save image_name > /home/save.tar
	
	#使用scp将save.tar拷贝到机器b上，然后
	
	docker load < /home/save.tar
	
### 登录registry server （login）

	docker login
	
###发布image

	docker push new_image_name
	
### 根据Dockerfile构建出一个容器

	$docker build -t image_name Dockerfile_path
	
	
	
	
	
	
	
