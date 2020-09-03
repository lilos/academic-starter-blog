---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Hugo Use"
subtitle: ""
summary: "hugo use"
authors: []
tags: [Hugo, Academic, 备案]
categories: []
date: 2020-08-26T20:26:15+08:00
lastmod: 2020-08-26T20:26:15+08:00
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

## Create blog post

```
cd ~/github/academic-starter-blog
hugo new --kind post post/hugo-use

hugo server
```

## hugo Academic添加ICP备案号

```
config/_default/config.toml:

# Enter a copyright notice to display in the site footer.
# To display a copyright symbol, type `&copy;`. For current year, type `{year}`.
copyright = "&copy; {year} | [京ICP备2020034512号-1](https://beian.miit.gov.cn/)"
```

## 腾讯云全站加速网络+netlify发布配置

1. netlify 配置

   [Domain settings] -> [Domain management] -> [Add domain alias] 

   {{< figure src="netlify_config.png" title="netlify 配置" >}}

2. 腾讯云全站加速配置(已备案)

   {{< figure src="ecdn_add.png" title="ECDN 添加域名" >}}

3. 腾讯云免费[SSL证书](https://console.cloud.tencent.com/ssl)申请+ECDN配置HTTPS

4. 腾讯云DNS解析配置

   {{< figure src="cns.png" title="DNSPod 解析" >}}

5. 结果

   ```
   jong@mac ~ % host www.lilos.cn
   www.lilos.cn is an alias for www.lilos.cn.dsa.dnsv1.com.
   www.lilos.cn.dsa.dnsv1.com is an alias for jnt1nygp.dsa.dispatch.spcdntip.com.
   jnt1nygp.dsa.dispatch.spcdntip.com has address 117.131.201.103
   
   jong@mac ~ % host lilos.cn
   lilos.cn is an alias for www.lilos.cn.
   www.lilos.cn is an alias for www.lilos.cn.dsa.dnsv1.com.
   www.lilos.cn.dsa.dnsv1.com is an alias for jnt1nygp.dsa.dispatch.spcdntip.com.
   jnt1nygp.dsa.dispatch.spcdntip.com has address 117.131.201.103
   ```

   {{< figure src="pre.png" title="加速前" >}}
   {{< figure src="post.png" title="加速后" >}}

   



## 参考

* [[1] sourcethemes.com](https://sourcethemes.com/academic/docs/managing-content/#create-a-blog-post)
* [[2] gohugo.io](https://gohugo.io/documentation/)

* [[3] www.netlify.com](https://www.netlify.com/)