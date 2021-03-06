---
title: GitHub Pages + hexo搭建博客
date: 2017-03-26 14:40:36
tags:
---

本文介绍通过[GitHub Pages](https://pages.github.com/) + [hexo](https://hexo.io/zh-cn/) 搭建个人博客


### 准备工作
+ [注册github账户](https://github.com/join)
	+ 使用 GitHub Pages 服务托管博客
+ [安装node](https://nodejs.org/en/)
	+ hexo基于 node 进行生成
+ [安装Git](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
	+ 提交代码、blog代码进行版本控制

### 创建gitHub库
+ 命令行创建

 ```bash
 $ curl -u "userName" https://api.github.com/user/repos -d '{"name":"'blogName'"}'
 ```

	userName 为你github用户名

	blogName 你需要创建github库名字

这个库创建重要用于网站源代码的管理

+ [网页创建](https://github.com/new)

### 安装hexo
hexo基于node进行生成，请确保是否安装 node 环境

```bash
$ npm i -g hexo-cli                      // 安装hexo模块
```
### 本地初始化博客
依次输入以下命令

```bash
$ cd ~/Desktop/ && mkdir blog && cd blog // 创建本地博客目录
$ hexo init                              // 初始化博客
```
### 添加并关联远程仓库

```bash
$ git init
$ git remote add git@github.com:getjll/blog.git
```

### 创建getjll.github.io仓库

用于部署生成的静态页面

```bash
 $ curl -u "userName" https://api.github.com/user/repos -d '{"name":"'getjll.github.io'"}'
```
### 添加部署脚本

```bash
$ mkdir deploy.sh && open deplay.sh
```
向 deploy.sh添加如下代码

```bash
hexo clean
hexo g
cd public
git init
git add -A
git commit -m 'update site'
git push -f git@github.com:getjll/getjll.github.io.git master // 这里替换成自己的分支
```
打开package.json文件向 scripts 添加如下字段

```json
  "scripts": {
    "d": "sh ./deploy.sh"
  },
```

部署命令

```bash
$ npm run d
```

### [自定义域名](https://help.github.com/articles/setting-up-a-custom-subdomain/)

```
$ echo getjll.com source/CNAME  getjll.com替换成你自己申请并解析的域名
```
hexo会将source的文件自动拷贝到生成目录
