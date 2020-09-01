---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Python Shallow Copy and Deep Copy"
subtitle: ""
summary: "python copy"
authors: []
tags: [python,]
categories: []
date: 2020-09-01T10:50:25+08:00
lastmod: 2020-09-01T10:50:25+08:00
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

> Python 深拷贝和浅拷贝理解，赋值、切片呢？

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

* 赋值：打标签，同一对象  

* 切片：浅拷贝  

* 浅拷贝，如果容器里面的项是引用，拷贝的就是引用，此引用指向相同的对象  

* 深拷贝，如果容器里面的项是引用，拷贝的是引用所指向的对象、即创建新对象（若此对象是一个容器，里面的项是引用，递归上述操作） [Python中深拷贝和浅拷贝有什么具体的区别吗? - 小张的回答 - 知乎](https://www.zhihu.com/question/326409605/answer/699059739)

