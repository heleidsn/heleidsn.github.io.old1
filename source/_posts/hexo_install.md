---
layout: '利用github+Hexo建立个人博客 Ubuntu版本'
title: post
date: 2020-08-30 00:30:57
tags:
---


今天查资料的时候发现,以前很多东西都没有进行保存,重复查起来又很费劲,于是再次想起了搭建博客来进行一些记录,一方面方便自己查询,另一方面也可以给其他提供一些帮助.

于是首先翻看了自己github账号上的上古博客,发现竟然是五年前的.五年了没有一点改进,真的是...

下面将Github+Hexo建站的一些过程记录一下...

## 安装Node.js

可以使用[nvm](https://github.com/nvm-sh/nvm)来进行安装

`$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash`

查看Node.js版本

`$ nvm ls-remote`

如果遇到返回`N/a`的情况重启命令行即可

安装Node.js

`$ nvm install 12.18.3`

## 安装Git

`$ sudo apt-get install git-core`

## 安装Hexo

`$ npm install -g hexo-cli`

## 创建工程

选择一个合适的位置创建工程

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

## 部署到github

https://hexo.io/docs/github-pages#One-command-deployment

Hexo提供了一键部署的方法:

1. 安装[hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)
2. 修改_config.yml

```
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
```

3. 执行`hexo clean && hexo deploy`
4. 在github中查看,或者直接在域名查看即可(PS:部署后大概一分钟左右即可看到网站的更新)


## 修改主题


## 参考

https://blog.kavoori.com/2014-10-13/installing-hexo-on-ubuntu.html
