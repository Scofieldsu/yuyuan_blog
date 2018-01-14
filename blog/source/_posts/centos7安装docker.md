---
title: centos7 安装docker1.26
date: 2017-05-08 20:47:23
categories: devops
tags: [docker,centos7]
---

1. 安装yum-utils，它提供yum-config-manager实用程序：

sudo yum install -y yum-utils

2. 使用以下命令设置稳定版本库：

sudo yum-config-manager \
    --add-repo \
    https://docs.docker.com/v1.13/engine/installation/linux/repo_files/centos/docker.repo

3. 更新yum包索引。

sudo yum makecache fast

4. 安装特定版本

yum list docker-engine.x86_64  --showduplicates |sort -r

sudo yum -y install docker-engine-1.12.6-1.el7.centos

5. 启动服务
sudo systemctl start docker

systemctl enable docker
