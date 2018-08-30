---
title: 玩一玩jenkins
date: 2017-06-08 20:47:23
categories: 皮一下
tags: [jenkins]
---

### 安装jenkins

> 准备工作 安装java环境

1. 配置yum源

 ```
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

2. 导入公钥

```
   sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

3. 安装jenkins

    yum install jenkins -y

4. 修改用户

   vi /etc/sysconfig/jenkins

5. 配置文件中加入java路径

    vim /etc/rc.d/init.d/jenkins

6. 启动
    systemctl start jenkins

7. 初次密码路径
    /var/lib/jenkins/secrets/initialAdminPassword


![jenkins](https://github.com/Scofieldsu/Image_hosting/blob/master/blog/jenkins.png?raw=true)

---

### jenkins使用参数构建任务
