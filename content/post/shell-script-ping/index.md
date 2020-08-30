---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Shell Script Ping"
subtitle: ""
summary: ""
authors: []
tags: [shell,]
categories: []
date: 2020-08-31T00:08:10+08:00
lastmod: 2020-08-31T00:08:10+08:00
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

## 探测10.10.10.0/24 网络主机存活脚本

```sh
#!/bin/bash
for i in {1..5}
do
    ping -c 2 172.17.0.$i > /dev/null && echo 172.17.0.$i is up &
done
wait
echo END
```

[参考1](https://www.infvie.com/sexuality-skills/shell-multi-process.html)  

[参考2](https://stackoverflow.com/questions/2791069/how-to-use-parallel-execution-in-a-shell-script)