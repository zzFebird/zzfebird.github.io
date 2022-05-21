---
title: GitHub Pages + Hexo 搭建个人博客
date: 2022-05-05 21:04:25
tags:
---

## 安装 Git 和 Node.js
Git: https://git-scm.com/downloads
Node.js: https://nodejs.org/en/
<!--more-->
全部默认安装即可。

## 连接GitHub
打开 Git Bash，设置 GitHub 用户：
```
git config --global user.name "zzFebird"
git config --global user.email "zengzipeng2012@163.com"
```
创建 SSH 密匙：
```
ssh-keygen -t rsa -C "zengzipeng2012@163.com"
```
一路回车，在 .ssh 目录下会生成密钥。  
进入 GitHub 设置，将 id_rsa.pub 的内容添加至 SSH Keys，测试连接：
```
ssh -T git@github.com
```
若提示 `Are you sure you want to continue connecting (yes/no/[fingerprint])?`  
输入 `yes`， .ssh 目录下会生成 known_hosts  
提示 `You've successfully authenticated` 则连接成功

## 创建仓库
创建 GitHub 仓库（略），创建本地仓库（空目录），进入本地仓库，初始化并下载必要组件：
```
hexo init
npm install
npm install hexo-deployer-git --save
```
修改 _config.yml 的 Deployment 部分：
``` 
deploy:
  type: git
  repo: https://github.com/zzFebird/zzfebird.github.io.git
  branch: main
```
修改本地博客文件，生成页面并部署：
```
hexo clean
hexo g
hexo d
```
刚部署完需要等待几分钟才能生效，可以通过 `hexo s` 预览本地网页。

## 修改主题
进入 hexo 官网 https://hexo.io/themes/ 选择主题，以 next 为例  
npm 方式：
```
npm install hexo-theme-next
```
git 方式：
```
git clone https://github.com/next-theme/hexo-theme-next themes/next
```
修改 _config.yml：
```
theme: next
```

## 编写博客
删除 source/_posts 目录下的 md 示例文件，通过`hexo new`创建新的 md 文件，编辑并部署即可。

## 显示摘要
在需要截断的地方加入 `<!--more-->`
