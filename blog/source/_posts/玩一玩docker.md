---
title: 玩一玩docker
date: 2017-05-08 20:47:23
categories: 皮一下
tags: [docker,centos7,2048]
---

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
