---
title: hexo多台电脑同步
date: 2020-10-08 17:13:41
tags: hexo
---

hexo在github pages中只上传了编译好的静态文件，如果需要在多台设备间进行同步写作，需要将源文件同时进同步。

方法：创建新的分支并设置为默认分支，用于保存源文件。

参考： 
使用hexo，如果换了电脑怎么更新博客？ - 直上云霄的回答 - 知乎
https://www.zhihu.com/question/21193762/answer/489124966

https://duran.im/2018/05/24/mastering-hexo/

## windows下重新安装hexo环境
- git clone
- 安装Node.js
  - https://nodejs.org/en/
- 安装hexo
  - `npm install -g hexo-cli`
- 初始化工作区
  - `npm install --force`