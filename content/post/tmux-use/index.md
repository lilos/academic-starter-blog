---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Tmux Use"
subtitle: ""
summary: "tmux use"
authors: []
tags: [tools,]
categories: []
date: 2020-09-16T00:05:47+08:00
lastmod: 2020-09-16T00:05:47+08:00
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

## install 

* Mac

  brew install tmux

* Centos 7

  rpm -ivh  https://packages.endpoint.com/rhel/7/os/x86_64/tmux-2.9a-3.ep7.x86_64.rpm
  
  tmux -V

## config

```sh
% cat ~/.tmux.conf
set -g mouse on
```

## use

1. 窗格管理
   * Ctrl+b  "    : 划分左右两个窗格
   * Ctrl+b  %  : 划分上下两个窗格

2. 窗口管理

   * Ctrl+b  c  : 创建一个新窗口
   * Ctrl+b  w : 列出所有窗口，并选择

3. 会话管理

   * Ctrl+b  d : 分离当前会话
   * Ctrl+b $ ：重命名当前会话。
   * Ctrl+b  s : 列出所有会话，并选择

4. 命令

   * tmux new -s <session-name>

   * tmux ls
   * tmux attach -t {id}
   * tmux rename-session -t {id} <new-name>

## refer

[[1] Tmux 使用教程](http://www.ruanyifeng.com/blog/2019/10/tmux.html)

