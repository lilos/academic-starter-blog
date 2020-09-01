---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Clear Memory Cache in Linux"
subtitle: ""
summary: "clear memory cache"
authors: []
tags: [linux, mem]
categories: []
date: 2020-09-01T18:44:21+08:00
lastmod: 2020-09-01T18:44:21+08:00
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

```
摘自：https://www.kernel.org/doc/Documentation/sysctl/vm.txt
drop_caches

Writing to this will cause the kernel to drop clean caches, as well as
reclaimable slab objects like dentries and inodes.  Once dropped, their
memory becomes free.

To free pagecache:
	echo 1 > /proc/sys/vm/drop_caches
To free reclaimable slab objects (includes dentries and inodes):
	echo 2 > /proc/sys/vm/drop_caches
To free slab objects and pagecache:
	echo 3 > /proc/sys/vm/drop_caches
```

## 操作

```
free && sync && echo 3 > /proc/sys/vm/drop_caches && free

相关：
1、dropcache不会清理脏页，只会清理干净的页，所以如果你想清理所有的页的话，是需要在drop前先sync的。
2、flush和fsycn都可以用来刷脏页，只是fsync可以更加具体一些：比如只刷data或者只刷metadata。而且都可以针对pagecache。sync也会刷脏页，它会刷整个系统的脏页，而不是针对具体某个文件。
3、echo 2 会去尝试释放所有可以回收的slab，但是它释放inode的过程中也会释放inode的page cache
4、echo 1 则只是释放page cache，而不去释放slab，而且在释放pagecache的过程中也不会去考虑inode的情况，也就是说echo 2 中有些不会释放的pagecache在这种方式里会被释放。
摘自：https://time.geekbang.org/column/article/278222

```

## 相关概念

* 脏页：当内存数据页和磁盘数据页上的内容不一致时，我们称这个内存页为脏页
* 干净页：内存数据写入磁盘后，内存页上的数据和磁盘页上的数据就一致了，我们称这个内存页为干净页。[摘抄](https://www.jianshu.com/p/6ffb01aa7717)
* 匿名页(anon)：如进程堆、栈、数据段使用的页、匿名mmap共享内存时使用的页、shmem共享内存时使用的页等,如果要交换,需要交换到虚拟内存-swapfile或者linux的swap硬盘分区。
* 文件页(file)：有文件背景的页面,如代码段,要交换的话,可以直接和硬盘对应的文件进行交换。 [摘抄](https://www.jianshu.com/p/7ab51b8a6368)

### Page Cache

```sh
$ cat /proc/meminfo
...
Buffers:            1224 kB
Cached:           111472 kB
SwapCached:        36364 kB
Active:          6224232 kB
Inactive:         979432 kB
Active(anon):    6173036 kB
Inactive(anon):   927932 kB
Active(file):      51196 kB
Inactive(file):    51500 kB
...
Shmem:             10000 kB
...
SReclaimable:      43532 kB
...

指标具体含义：
1、https://www.kernel.org/doc/Documentation/filesystems/proc.rst
2、https://access.redhat.com/solutions/406773
3、https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/s2-proc-meminfo

$ free -k
              total        used        free      shared  buff/cache   available
Mem:        7926580     7277960      492392       10000      156228      430680
Swap:       8224764      380748     7844016
buff/cache = Buffers + Cached + SReclaimable
```

> Buffers + Cached + SwapCached = Active(file) + Inactive(file) + Shmem + SwapCached

那么等式两边的内容就是我们平时说的 **Page Cache**

在 Page Cache 中，Active(file)+Inactive(file) 是 File-backed page（与文件对应的内存页），是你最需要关注的部分。因为你平时用的 mmap() 内存映射方式和 buffered I/O 来消耗的内存就属于这部分，最重要的是，这部分在真实的生产环境上也最容易产生问题

### reclaimable slab objects (includes dentries and inodes)

* dentry：目录项，directory entry的缩写。[摘抄](https://bean-li.github.io/vfs-inode-dentry/)
* inode：索引节点
* slab：slub分配器管理小块内存的分配，小于一页

## 参考

[[1] https://unix.stackexchange.com/questions/87908/how-do-you-empty-the-buffers-and-cache-on-a-linux-system?noredirect=1&lq=1](https://unix.stackexchange.com/questions/87908/how-do-you-empty-the-buffers-and-cache-on-a-linux-system?noredirect=1&lq=1)

[[2] https://time.geekbang.org/column/article/273892](https://time.geekbang.org/column/article/273892)

[[3] https://time.geekbang.org/column/article/96103](https://time.geekbang.org/column/article/96103)

[[4] https://stackoverflow.com/questions/15470560/what-to-choose-between-slab-and-slub-allocator-in-linux-kernel](https://stackoverflow.com/questions/15470560/what-to-choose-between-slab-and-slub-allocator-in-linux-kernel)

[[5] http://cenalulu.github.io/linux/numa/](http://cenalulu.github.io/linux/numa/)

