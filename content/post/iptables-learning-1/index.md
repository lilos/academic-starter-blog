---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Iptables Learning 1"
subtitle: ""
summary: "Iptables Learning"
authors: []
tags: [iptables,firewalld]
categories: []
date: 2020-08-26T21:31:25+08:00
lastmod: 2020-08-26T21:31:25+08:00
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

> 1、如何将本地80端口的请求转发到8080端口，当前主机IP为172.17.0.5？

```
iptables -t nat -A PREROUTING -d 172.17.0.5 -p tcp --dport 8084 -j REDIRECT --to-ports 80
or:
iptables -t nat -A PREROUTING -d 172.17.0.5 -p tcp --dport 8084 -j DNAT --to-destination :80
```

[参考](https://unix.stackexchange.com/questions/144497/in-iptables-what-is-the-difference-between-targets-dnat-and-redirect)

