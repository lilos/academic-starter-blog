---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Interview Questions for 2020"
subtitle: ""
summary: "2020 面试回顾"
authors: []
tags: []
categories: []
date: 2020-08-26T20:38:17+08:00
lastmod: 2020-08-26T20:38:17+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## 基础层

1. Linux系统优化
2. TCP三次握手和四次挥手介绍
3. 系统卡顿或CPU高占用处理思路
4. 对于一个web服务器来说，应该调整哪些Linux内核参数，并说明他们的含义

## 中间层

1. mysql主从同步原理介绍
2. mysql环状三主高可用架构介绍
3. mysql优化
4. redis优化
5. LVS dr/nat 原理介绍
6. apache有几种工作模式，分别简述两种工作模式及其优缺点？
7. nginx配置文件结构、负载均衡算法、常用模块
8. nginx高可用方案
9. postgres高可用方案
10. nginx处理跨域问题和proxy_pass后带路径
11. mysql备份和恢复，以test库为例

## firewalld

1. iptables几表几链
2. 禁止来自 10.0.0.188 ip 地址访问 80 端口的请求
3. 如何将本地80端口的请求转发到8080端口，当前主机IP为10.0.1.10？
4. firewalld介绍 几个区

## git

1. git工作流

## shell

1. 写一个脚本（shell、python都可以），实现nginx日志按天分割，并将前一天的日志进行压缩，总共保留10天的备份

2. 写一个并发执行的脚本，完成并发获取20台服务器的20:00:01到20:10:01的nginx日志。服务器列表:/data/iplist ,日志路径：/data/logs/nginx/access.log

3. 用shell统计ip访问情况，要求分析nginx访问日志，找出访问数量前10位的IP数，以下nginx日志结构

   ```
   195.54.160.21 - - [26/Aug/2020:21:06:38 +0800] "GET /index.php?s=/Index/\x5Cthink\x5Capp/invokefunction&function=call_user_func_array&vars[0]=md5&vars[1][]=HelloThinkPHP HTTP/1.1" 
   404 571 "-" 
   "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36"
   
       #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
       #                  '$status $body_bytes_sent "$http_referer" '
       #                  '"$http_user_agent" "$http_x_forwarded_for"';
   ```

4. 编写shell脚本将/usr/local/test目录下大于100K的文件转移到/tmp目录下

5. shell字符串处理

## python

1. 有没有一个工具可以帮助查找python的bug和进行静态的代码分析？
2. 深拷贝和浅拷贝，赋值、切片呢？

  ```python
  >>> a=[1,2,[1,2]]
  >>> a
  [1, 2, [1, 2]]
  >>> b=a
  >>> import copy
  >>> c=copy.copy(a)
  >>> d=copy.deepcopy(a)
  >>> a[2].append(5)
  >>> a
  [1, 2, [1, 2, 5]]
  >>> b
  [1, 2, [1, 2, 5]]
  >>> c
  [1, 2, [1, 2, 5]]
  >>> d
  [1, 2, [1, 2]]
  >>> a.append(3)
  >>> a
  [1, 2, [1, 2, 5], 3]
  >>> b
  [1, 2, [1, 2, 5], 3]
  >>> c
  [1, 2, [1, 2, 5]]
  >>> d
  [1, 2, [1, 2]]
  ```

赋值：打标签，同一对象

切片：浅拷贝

浅拷贝，如果容器里面的项是引用，拷贝的就是引用，此引用指向相同的对象  
深拷贝，如果容器里面的项是引用，拷贝的是引用所指向的对象、即创建新对象（若此对象是一个容器，里面的项是引用，递归上述操作）[Python中深拷贝和浅拷贝有什么具体的区别吗? - 小张的回答 - 知乎](https://www.zhihu.com/question/326409605/answer/699059739)

## Kubernetes

1. pod理解  [为什么我们需要Pod？](https://time.geekbang.org/column/article/40092) (真的，能讲出来或者实践才能真正理解相关设计)
2. docker理解，和虚拟机的区别

## docker

1. docker copy/add 区别

2. docker 配置文件介绍

3. 编写 dockerfile 文件

4. kill docker 进程会关闭吗

   