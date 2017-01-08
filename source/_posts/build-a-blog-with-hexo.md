---
title: 用Hexo + Github搭建静态博客
date: 2017-01-06 11:28:36
tags: Hexo 
---

# 先絮叨絮叨
本来我是在新浪的SAE上搭了个Wordpress来写blog，因为当时还在新浪微博上班，用内部员工邮箱验证的话，每月有15000云豆足够使用，但是自打从微博离职以后有一阵没再管过我那个blog了。也就是在那个时候，SAE改变了策略，不再送云豆了，随后又对欠费的空间进行了清理，于是乎我那几年写的技术帖就伴随着我的blog一起消失掉了，也是怪可惜的。

从微博离职后的两年中我不断学习了一些新东西，但是一直没有记录下来，很多知识又逐渐遗忘了，于是想还是写点什么吧，毕竟好记性不如烂笔头。于是利用Hexo和Github Pages重新搭了个blog，并记录一下过程。

# 正文开始
## 安装Hexo
Hexo和Wordpress不同，Hexo不是一个blog系统，而是一个静态博客框架，或者说是静态网站生成器。我们使用Wordpress的时候，需要一套php+mysql+apache/nginx环境来运行Wordpress，而Hexo不需要，它只需要Node即可，我们平时用Markdown来写文章，然后通过Hexo转成静态的HTML页面。本文假设你已安装了Node。

首先把hexo安装到global，这样你在任何位置都可以运行hexo命令

```
$ sudo npm install hexo -g
```

Hexo就安装好了，值得一提的是，如果你在墙内使用npm非常慢的话，可以试试先运行下面的命令，更换到国内镜像：

```
$ sudo npm config set registry https://registry.npm.taobao.org
```

### 试运行Hexo
安装好后，我们可以试运行一下Hexo
```
$ hexo init myblog
```
这会在当前目录下生成一个myblog目录，里面有blog所需要的全部代码了，接着我们让他先跑起来试试。
```
$ cd myblog
$ hexo serve
```
根据提示，访问http://localhost:4000/ 就可以看到正常的页面了。

## 创建Github Pages
Github Pages是Github提供的静态页面服务，适合用作个人或者项目主页，作为全国最大的程序员同性交友社区，Github的服务质量还是可靠的，当然除了被墙掉以外。

要申请Github Pages服务非常简单，只要创建一个username.github.io命名的Repository就行了，比如我的Github用户名是sandysong，那么我的Repository名就是sandysong.github.io。

{% asset_img create-github-pages.png [创建Github Pages] %}

### 创建Hexo分支
Github Pages默认将master分支的代码用作静态页面服务，我们这里创建一个Hexo分支，用来存放我们blog的源文件，而只将生成的静态文件发布到master。
```
$ cd myblog
$ git init
$ git branch hexo
$ git checkout hexo
```
然后我们还需要安装一个Hexo插件：hexo-deployer-git
```
$ npm install hexo-deployer-git --save
```
接下来修改一下Hexo的配置文件，也就是myblog/_config.yml文件，告诉Hexo如何发布代码
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/sandysong/sandysong.github.io
  branch: master
```
完成这些事情之后，我们将代码提交：
```
$ git add -A
$ git commit -m 'init'
$ git push origin hexo
```
### 编辑文章并发布
如果要创建一篇文章，可运行
```
$ hexo new title-of-your-blog
```
这会在source/_posts/下创建一个"title-of-your-blog.md"文件，用我们喜欢的markdown编辑器完成这个文件内容的编辑后，我们可以生成并发布我们的文章了。
```
$ hexo g
$ hexo d
```
生成的静态文件会自动发布到master分支，之后我们访问：https://sandysong.github.io，就能看到我们刚写的blog了。

