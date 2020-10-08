---
layout: 
title: hexo 常用命令
date: 2020-09-01 17:34:40
tags: hexo
---

## 常用命令
- 新建博客： `hexo n XX` 等于 `hexo new XX`
- 生成文件： `hexo g` 等于 `hexo generate`
- 启动本地服务器：`hexo s` 等于 `hexo server`
- 部署：`hexo d` 等于 `hexo deploy`

## 修改主题

- 查看主题：https://hexo.io/themes/
- 下载（以pure为例）：
  - `git clone https://github.com/cofess/hexo-theme-pure.git themes/pure`
- 设置：　Modify the value of `theme`: in `_config.yml`

## 安装插件

- 字数统计: `npm install hexo-wordcount --save`