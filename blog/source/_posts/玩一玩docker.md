---
title: 玩一玩docker
date: 2017-05-08 20:47:23
categories: 搞点事情
tags: [docker,centos7,2048]
---

``` shell
Docker是一个开源的应用容器引擎，基于 Go 语言 并遵从Apache2.0协议开源。

Docker可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，
然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,
更重要的是容器性能开销极低。

Docker 使用客户端-服务器 (C/S) 架构模式。
Docker 客户端会与 Docker 守护进程进行通信。
Docker 守护进程会处理复杂繁重的任务，例如建立、运行、发布你的 Docker 容器。
Docker 客户端和守护进程可以运行在同一个系统上，
当然你也可以使用 Docker 客户端去连接一个远程的 Docker 守护进程。
Docker 客户端和守护进程之间通过 socket 或者 RESTful API 进行通信。

- Docker 镜像是 Docker 容器运行时的只读模板，每一个镜像由一系列的层 (layers) 组成。
  Docker 使用 UnionFS 来将这些层联合到单独的镜像中。

- Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。

- Docker 容器和文件夹很类似，一个Docker容器包含了所有的某个应用运行所需要的环境。


```

## 1. centos安装docker

1. 安装yum-utils，它提供yum-config-manager实用程序：

  sudo yum install -y yum-utils

2. 使用以下命令设置稳定版本库：

  ```shell
  sudo yum-config-manager \
      --add-repo \
      https://docs.docker.com/v1.13/engine/installation/linux/repo_files/centos/docker.repo
  ```
3. 更新yum包索引。

  sudo yum makecache fast

4. 安装特定版本

    yum list docker-engine.x86_64  --showduplicates |sort -r

   -例如安装17.05.0.ce版本

    sudo yum -y install docker-engine-17.05.0.ce-1.el7.centos

5. 启动服务

   sudo systemctl start docker

   systemctl enable docker

---

## 2. 好玩的docker image

### docker运行2048游戏

- 命令： docker run -d -p 8989:80 alexwhen/docker-2048

![2048](https://raw.githubusercontent.com/Scofieldsu/Image_hosting/master/blog/2048.png)

### docker运行gitlab

- 命令：

  ```
  docker run -d -h gitlab-p 9999:22-p 8081:80-p 8443:443-v /docker/gitlab/config:/etc/gitlab -v /docker/gitlab/logs:/var/log/gitlab -v /docker/gitlab/data:/var/opt/gitlab --restart always --name gitlab gitlab/gitlab-ce:latest

  ```

![gitlab](https://github.com/Scofieldsu/Image_hosting/blob/master/blog/gitlab.png?raw=true)

### docker运行rancher

>Rancher是一个容器管理平台，专为在生产中部署容器的组织而构建。Rancher使您可以轻松地在任何地方运行Kubernetes.

- 命令： docker run -d --restart=unless-stopped -p 8989:80 -p 443:443 rancher/rancher:stable

![rancher-1](https://github.com/Scofieldsu/Image_hosting/blob/master/blog/rancher-1.png?raw=true)
![rancher-2](https://github.com/Scofieldsu/Image_hosting/blob/master/blog/rancher-2.png?raw=true)
![rancher-3](https://github.com/Scofieldsu/Image_hosting/blob/master/blog/rancher-3.png?raw=true)

---

### 3. docker 命令


### 4. dockerfile
