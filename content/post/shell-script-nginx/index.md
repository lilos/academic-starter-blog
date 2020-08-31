---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Shell Script Nginx"
subtitle: ""
summary: "Shell Script Nginx"
authors: []
tags: [shell,nginx]
categories: []
date: 2020-08-31T22:13:29+08:00
lastmod: 2020-08-31T22:13:29+08:00
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

## 日志切割

[摘抄：](https://time.geekbang.org/course/detail/100020301-65071)

```sh
#!/bin/bash
#Rotate the nginx logs
LOGS_PATH=/usr/local/openrestry/nginx/logs/history
CUR_LOGS_PATH=/usr/local/openrestry/nginx/log
YESTERDAY=$(date -d "yesterday" +%Y-%m-%d)
mv ${CUR_LOGS_PATH}/access.log ${LOGS_PATH}/access_${YESTERDAY}.log
mv ${CUR_LOGS_PATH}/error.log ${LOGS_PATH}/erros_${YESTERDAY}.log
## 向 Nginx 主进程发送 USR1 信号。USR1 信号是重新打开日志文件
kill -USR1 $(cat /usr/local/openresty/nginx/logs/nginx.pid)
```

## 面试题

> 1：写一个脚本（shell、python都可以），实现nginx日志按天分割，并将前一天的日志进行压缩，总共保留10天的备份

```sh
#!/bin/bash
#Rotate the nginx logs
LOGS_PATH=/usr/local/openrestry/nginx/logs/history
CUR_LOGS_PATH=/usr/local/openrestry/nginx/log
YESTERDAY=$(date -d "yesterday" +%Y-%m-%d)
mv ${CUR_LOGS_PATH}/access.log ${LOGS_PATH}/access_${YESTERDAY}.log
mv ${CUR_LOGS_PATH}/error.log ${LOGS_PATH}/erros_${YESTERDAY}.log
## 向 Nginx 主进程发送 USR1 信号。USR1 信号是重新打开日志文件
kill -USR1 $(cat /usr/local/openresty/nginx/logs/nginx.pid)

tar -czf ${LOGS_PATH}/access_${YESTERDAY}.log.tar.gz ${LOGS_PATH}/access_${YESTERDAY}.log --remove-files
tar -czf ${LOGS_PATH}/erros_${YESTERDAY}.log.tar.gz  ${LOGS_PATH}/erros_${YESTERDAY}.log --remove-files

find ${LOGS_PATH} -mtime +10 -name "*.log.tar.gz" -exec mv {} /tmp \;
```

> 2：写一个并发执行的脚本，完成并发获取20台服务器的20:00:01到20:10:01的nginx日志。服务器列表:/data/iplist ,日志路径：/data/logs/nginx/access.log

```sh
#!/bin/bash
IPLIST=/data/iplist
LOG_PATH=/data/logs/nginx/access.log
LOCAL_PATH=/data/logs

while read line
do
    #echo $line
    scp root@${line}:${LOG_PAT}  ${LOCAL_PATH}/${line}_access.log && sed -n '/31\/Aug\/2020:20:00:01/,/31\/Aug\/2020:20:10:01/p' ${line}_access.log &
done < ${IPLIST}
```

