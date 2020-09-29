---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Curl Use"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-09-23T10:49:03+08:00
lastmod: 2020-09-23T10:49:03+08:00
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

## curl

## 1. -X

```
curl -X GET http://example.com
```

## 2. -H

```
-H 'Content-Type: application/json'
-H "Token:$HEADER_TOKEN" 
-H "Timestamp:$TIMESTAMP"
```

## 3. -F, --form

```
curl -X POST  -F name=lilos http://example.com
# 默认 -H 'Content-Type: multipart/form-data'
```

## 4. -d

```
curl -X POST -d 'name=lilos&alias=lil' http://example.com

-H 'Content-Type: application/json' -d '
{
    "name": "lilos",
    'alias' "lll"
}'


```



