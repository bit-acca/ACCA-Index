---
author:
- LTSlw
tags:
- mid
- hugo
- blog
- web
- server
date: 2024-03-06
lastmod: 2024-03-06
---

# 认识hugo

## hugo简介

[`hugo`](https://gohugo.io/)是一个开源的静态网站生成器，使用go语言编写。它允许你设置自己的主题，然后用markdown编写页面内容，hugo就可以直接生成html页面。静态网站意味着没有后台的数据库和服务软件，虽然限制了一些功能，但也带来了很多好处

- 静态页面节省资源，构建和访问都非常快
- 省去直接编写html带来的麻烦
- 主题和内容分离，可以分别维护
- 可以直接托管到github pages等平台，无需自己支付服务器费用

虽然页面是静态的，但hugo也允许你在页面中引入javascript代码，实现交互

## 前置技术

- markdown
- git（推荐）
- go mod（推荐）

## 安装hugo

受益于go语言，hugo只有一个单独的可执行文件

hugo有两个版本`standard`和`extended`，extended版本额外包含webp和scss支持，都是很有用的功能，推荐直接使用extended版本

### Linux

#### Arch

``` shell
pacman -S hugo
```

#### Debian

``` shell
apt install hugo
```

### Windows

在[Github Release](https://github.com/gohugoio/hugo/releases/latest)下载Windows版本，下载extended版本

下载解压之后，将其目录添加到`PATH`

### MacOS

``` shell
brew install hugo
```

### 检查安装

``` shell
hugo version
```
