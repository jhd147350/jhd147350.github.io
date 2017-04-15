---
title: Hexo搭建github博客绑定顶级域名和www子域名
date: 2017-04-07 17:56:27
tags: 
- jhdTag
categories: 
- jhdcate
comment: true
---

#Hexo搭建github博客绑定顶级域名和www子域名
我想将 jhd147350.github.io 和 www.jhd147350.space & jhd147350.space 绑定在一起。
##1. 在你博客目录source下 新建一个文件 CNAME (没有后缀)
内容如下：

> jhd147350.space
> www.jhd147350.space

##2. 部署
hexo的部署是强制更新github仓库的代码，所以不要在github仓库中新建CNAME，要在你博客目录source下建立，
```
//依次执行
hexo g
hexo d
```
##3. 解析你的域名
>我的是在新网注册的，其他网站注册解析域名的方法可能有不同  

A记录解析如下：
![这里写图片描述](http://img.blog.csdn.net/20170407174642005?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjQ1MDU0ODU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

顶级域名 **错误** A记录如下：
![这里写图片描述](http://img.blog.csdn.net/20170407175007181?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjQ1MDU0ODU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

>**我将通配符 * 加了进来， 我以为 *.jhd147350.space 就能代表顶级域名呢**
>在这坑了半天。

##4. 成果
>jhd147350.space
>jhd147350.github.io
>www.jhd147350.space
>都能成功访问到自己博客