---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Docker Network"
subtitle: ""
summary: "docker network"
authors: []
tags: [docker,]
categories: []
date: 2020-09-01T11:16:06+08:00
lastmod: 2020-09-01T11:16:06+08:00
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

>docker -v
>Docker version 19.03.12, build 48a66213fe

## man docker-run

    --network=type
       Set the Network mode for the container. Supported values are:
    Default is bridge.
| Value                 | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| none                  | No networking in the container.                              |
| bridge                | Connect the container to the default Docker bridge via veth interfaces. |
| host                  | Use the host's network stack inside the container.           |
| container:<u>name</u> | <u>id</u>                                                    |
| <u>network-name</u>   | <u>network-id</u>                                            |

## networking using the bridge network:

[https://docs.docker.com/network/network-tutorial-standalone/](https://docs.docker.com/network/network-tutorial-standalone/)

* [Use the default bridge network](https://docs.docker.com/network/network-tutorial-standalone/#use-the-default-bridge-network) demonstrates how to use the default `bridge` network that Docker sets up for you automatically. This network is not the best choice for production systems.
* [Use user-defined bridge networks](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks) shows how to create and use your own custom bridge networks, to connect containers running on the same Docker host. This is recommended for standalone containers running in production.

## networking using the host network:

[https://docs.docker.com/network/network-tutorial-host/](https://docs.docker.com/network/network-tutorial-host/)

