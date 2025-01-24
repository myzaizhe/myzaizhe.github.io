### 1. Docker 基础命令

#### 查看 Docker 版本

```bash
docker version
```

该命令会显示 Docker 客户端和服务端的版本信息。



#### 查看 Docker 系统信息

```bash
docker info
```

用于查看 Docker 系统的详细信息，如容器数量、镜像数量、存储驱动等。

#### 获取帮助信息

```bash
docker --help
docker <命令> --help
```

第一个命令是获取 Docker 整体的帮助信息，第二个是获取特定命令的详细帮助。



### 2. 镜像操作命令

#### 拉取镜像

```bash
docker pull <镜像名称>:<标签>
```

例如 `docker pull nginx:latest` 用于拉取最新版本的 Nginx 镜像。



#### 列出本地镜像

```bash
docker images
```

会显示本地已有的 Docker 镜像列表，包括镜像名称、标签、镜像 ID 等信息。



#### 构建镜像

```bash
docker build -t <镜像名称>:<标签> <构建上下文路径>
```

例如 `docker build -t myapp:1.0 .` 会在当前目录下根据 `Dockerfile` 构建一个名为 `myapp` 版本为 `1.0` 的镜像。



#### 删除本地镜像

```bash
docker rmi <镜像 ID 或镜像名称:标签>
```

可一次删除多个镜像，如 `docker rmi nginx:latest myapp:1.0`。



#### 保存镜像到文件

```bash
docker save -o <保存文件名> <镜像名称:标签>
```

如 `docker save -o nginx_image.tar nginx:latest` 将 Nginx 镜像保存为 `nginx_image.tar` 文件。



#### 从文件加载镜像

```bash
docker load -i <保存文件名>
```

例如 `docker load -i nginx_image.tar` 会将保存的 Nginx 镜像加载到本地。



#### 推送镜像到 Docker Hub

```bash
docker push <镜像名称:标签>
```

在推送前需要先登录 Docker Hub，使用 `docker login` 命令登录。



### 3. 容器操作命令

#### 创建并运行容器

```bash
docker run [选项] <镜像名称:标签> [命令] [参数]
```

常见选项：

- `-d`：后台运行容器。
- `-p <主机端口>:<容器端口>`：端口映射。
- `-v <主机目录>:<容器目录>`：挂载卷。
- `--name <容器名称>`：指定容器名称。

例如 `docker run -d -p 80:80 --name mynginx nginx:latest` 会在后台运行一个名为 `mynginx` 的 Nginx 容器，并将主机的 80 端口映射到容器的 80 端口。



#### 列出运行中的容器

```bash
docker ps
```

若要列出所有容器（包括停止的），使用 `docker ps -a`。



#### 停止容器

```bash
docker stop <容器 ID 或容器名称>
```

例如 `docker stop mynginx` 会停止名为 `mynginx` 的容器。



#### 启动已停止的容器

```bash
docker start <容器 ID 或容器名称>
```



#### 重启容器

```bash
docker restart <容器 ID 或容器名称>
```



#### 删除容器

```bash
docker rm <容器 ID 或容器名称>
```

若要删除正在运行的容器，可使用 `docker rm -f <容器 ID 或容器名称>`。



#### 进入容器

```bash
docker exec -it <容器 ID 或容器名称> <命令>
```

例如 `docker exec -it mynginx bash` 会以交互模式进入 `mynginx` 容器并启动 `bash` 终端。



#### 查看容器日志

```bash
docker logs <容器 ID 或容器名称>
```

添加 `-f` 选项可实时查看日志，如 `docker logs -f mynginx`。



#### 查看容器详细信息

```bash
docker inspect <容器 ID 或容器名称>
```

会输出容器的详细配置信息，如网络配置、挂载信息等。



### 4. 网络操作命令

#### 列出 Docker 网络

```bash
docker network ls
```



#### 创建网络

```bash
docker network create [选项] <网络名称>
```

例如 `docker network create mynetwork` 创建一个名为 `mynetwork` 的网络。



#### 删除网络

```bash
docker network rm <网络名称>
```



#### 连接容器到网络

```bash
docker network connect <网络名称> <容器 ID 或容器名称>
```



#### 断开容器与网络的连接

```bash
docker network disconnect <网络名称> <容器 ID 或容器名称>
```



### 5. 卷操作命令

#### 列出 Docker 卷

```bash
docker volume ls
```



#### 创建卷

```bash
docker volume create <卷名称>
```



#### 删除卷

```bash
docker volume rm <卷名称>
```



#### 查看卷详细信息

```bash
docker volume inspect <卷名称>
```



### 6. Docker Compose 相关命令

#### 启动服务

```bash
docker-compose up [-d]
```

`-d` 选项表示在后台运行服务。



#### 停止服务

```bash
docker-compose down
```

该命令会停止并删除由 `docker-compose.yml` 文件定义的服务、网络和容器。



#### 查看服务状态

```bash
docker-compose ps
```



#### 构建或重建服务镜像

```bash
docker-compose build
```



### 7. Docker Swarm 相关命令（用于集群管理）

#### 初始化 Swarm 集群

```bash
docker swarm init
```



#### 加入 Swarm 集群

```bash
docker swarm join --token <令牌> <管理节点 IP>:<端口>
```



#### 离开 Swarm 集群

```bash
docker swarm leave
```



#### 创建服务

```bash
docker service create [选项] <镜像名称:标签> [命令] [参数]
```

例如 `docker service create --name myservice -p 80:80 nginx:latest` 创建一个名为 `myservice` 的 Nginx 服务。



#### 列出服务

```bash
docker service ls
```



#### 删除服务

```bash
docker service rm <服务名称>
```