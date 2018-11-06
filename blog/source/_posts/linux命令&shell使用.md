---
title: linux命令&shell使用
date: 2017-12-18 20:13:45
categories: 关于一些事儿
tags: [linux,shell]
---
## 1. nohup （no hang up）
- 当你在运行一个进程，想要让其后台运行，不占用当前终端，关闭终端或者合上电脑或者退出账号时程序仍然在运行。nohup 了解一下。

``` shell

nohup java -jar -server -Xms512m a.jar abc >> logs/nohup.log 2>&1 &


---命令详解
(1) 执行jar包，可以带上你需要的启动参数，例如以server模式运行，初始堆大小512m -server -Xms512m
(2) abc 为主程序接收的参数
(3)  >> logs/nohup.log  
      其中>>表示追加，如果改为 > 则每次启动都会覆盖原log文件。
      指定到特定路径下的文件，如果不指定，则默认输出到当前目录的nohup.out
(4) 2>&1 将错误信息重定向到标准输出
(5) & 作业被提交到后台运行，当前控制台没有被占用

---其他相关
(1) 执行python程序时需要加上-u参数（不使用python print 的缓冲）把print的内容输出到文件。
    例如： nohup python -u run.py >> logs/nohup.log 2>&1 &

(2) 可以使用jobs -l  查看当前 shell 终端的后台运行任务进程信息,根据进程pid 进行kill来退出任务。
(3) fg %n ,置为前端运行,然后ctrl + c 退出任务。其中%n 为job id
(4) bg %n 让进程n到后台运行
(5) 文件很大的话，nohup.out就会不停的增大，可以利用Linux下一个特殊的文件/dev/null来解决这个问题，
    这个文件就相当于一个黑洞,任何输出到这个文件的东西都将消失
      只保留输出错误信息 nohup command >/dev/null 2>log &
      所有信息都不要 nohup command >/dev/null 2>&1 &

 ```

##  2. awk 和xargs  

``` python

```
