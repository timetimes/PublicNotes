# Docker

虚拟机——Docker——沙盒
技术：VirtualBox、Hyper-V、WSL2

 Docker安装[Windows](https://docs.docker.com/desktop/setup/install/windows-install/)：
 下载安装选项默认即可
 根据报错提示在命令行输入`wsl --update`，安装适用于 Linux 的 Windows 子系统

 `docker info` 查看docker是否正常安装

 `docker ps`查看正在运行的所有容器
 `docker ps -a` 查看设备上所有容器
`docker stop 容器id或名字` 停止容器
kill
`docker start 容器id或名字` 运行容器
`docker rm 容器id或名字`删除容器

 `docker pull 镜像作者/镜像名字` 从Docker Hub下载
` docker load < xxx.tar` tar文件 `docker save 镜像id > xxx.tar` 
 dockerfile
` docker commit 容器id 镜像名字` 把容器保存成镜像
` docker image ls` 列出镜像
` docker rmi` 删除镜像

`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]` 运行镜像成容器（如果本地没有会自动docker pull 镜像）（可以运行`hello-world`镜像测试）
部分 OPTIONS 说明，
-a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项，
-d: 后台运行容器，并返回容器 ID ；
-P: 随机端口映射，容器内部端口随机映射到主机的端口
-P. 指定端口映射，格式为：主机（宿主）端口：容器端口
--name= nginx-lb '为容器指定一个名称
--volume ， -v: 绑定一个卷

`docker exec -t 容器id或名字 bash` 进入容器
 
 docker volume 
 docker-compose up 
 docker-compose down

 由于某种原因在国内无法访问Docker Hub，需要改用Docker Hub 镜像。
 Linux修改 `/etc/docker/daemon.json`文件；windows在图形界面-设置-Docker Engine中修改（或者修改`daemon.json文件`），在大括号内加上：

 ```
    "registry-mirrors": [
		"镜像地址1",
		"镜像地址2"
    ],
```
修改daemon.json文件出错可能导致stopped，需要`cd "C:\Program Files\Docker\Docker"`跳转到Docker Desktop安装路径，运行命令`.\DockerCli.exe -SwitchDaemon`
