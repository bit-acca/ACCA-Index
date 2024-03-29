---
author:
- LTSlw
- dedfaf
tags:
- basic
- getting-start
- markdown
date: 2023-09-16
lastmod: 2024-02-28
---

# markdown基础

这是计协教程的第0话，梦开始的地方。在我们学习真正的计算魔法语言前，我们先来学习一种计算魔法的解释载体 - `markdown`

markdown由John Gruber在2004年创建。其中在语法上有很大一部分是跟Aaron Swartz共同合作的

关于更多markdown的历史，可以查阅茵蒂克丝的好伙伴 - [wikipedia · markdown](https://zh.wikipedia.org/zh-hk/Markdown)

[John Gruber的博客](https://daringfireball.net/)

## 为什么用markdown

markdown是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档，这本书就是用茵蒂克丝用markdown语言写成的

选择markdown是因为它足够简单，编辑时可以在注重内容的同时兼顾排版

现在markdown已经被广泛地使用，尤其是在计算魔法领域，当你想给你的项目添加一份说明，想快速编辑一份页面或者pdf，或者只是单纯的想写一些东西给同学看，那么markdown将会是你最好用的工具。markdown也被许多平台支持。因此茵蒂克丝认为在学习计算魔法前，学习如何使用markdown是很有必要的

使用计算机应该是大学生的必备技能了吧，大家不妨也锻炼一下打字速度，这样在课上你甚至可以用markdown写出一份相当工整的笔记，轻松实现无纸化办公

## 目前适用的markdown标准

markdown文件的后缀是`.md`或`.markdown`，在实际使用中通常是`.md`

如果你们知道html是什么，markdown其实是html的简化版，markdown是通过自己的语法将文字转换为html内容，因此markdown的规范化是一个历史遗留问题

从2012年开始，包括Jeff Atwood和John MacFarlane在内的一群人启动了标准化工作

2014年9月，格鲁伯反对在这一工作中继续使用markdown这个名字，其被更名为[CommonMark](https://commonmark.org/)，发布了规范、参考实现和测试套件的几个版本，并在2018年宣布最终的1.0规范和测试套件

目前比较通用的规范是GitHub发布的基于CommonMark的`GitHub Flavored Markdown`（`GFM`）的正式规范，是CommonMark的严格超集。在本章下面阅读编写markdown的部分茵蒂克丝也会以该规范为主讲解

[CommonMark](https://commonmark.org/)

[GitHub Flavored Markdown](https://github.github.com/gfm/)

*关于更多markdown的规范，以及markdown规范化的历史请参阅wiki酱*

## 如何阅读，编写markdown

如果你只想要一个markdown编辑器的话同样有许多选择

作为学习计算魔法的学生，茵蒂克丝非常推荐你使用免费开源插件多多的VSCode！

装完即用的markdown软件和不需要安装的网页版markdown，茵蒂克丝也会各推荐一个

### VSCode

如果只有阅读的需要可以跳过编辑部分

#### VSCode阅读markdown

1. 用VSCode打开markdown文件
2. 使用快捷键`Ctrl+K`，`V`浏览（先按`Ctrl+K`后按`V`）

![预览按钮](imgs/00_00_preview_button.png)你也可以直接在VSCode界面的右上角找这个预览按钮

你也可以自定义markdown预览的各种样式和主题，这些内容将在[VSCode编辑markdown](#vscode编辑markdown)中介绍

#### VSCode编辑markdown

如果你已经入门了计算机开发，茵蒂克丝强烈建议你使用VSCode作为markdown编辑器，可以将开发和文档编辑集成在一起

其实VSCode本身就自带一定程度的markdown支持，比如：预览，跳转，链接验证等等

目前VSCode原生支持的规范是CommonMark原版，并不完全支持GFM中的格式（表情，待办表等），如果VSCode的原生功能不能满足你，或者你想在VSCode中编写阅览GitHub格式的markdown，可以在VSCode中安装下方的插件

[GitHub Markdown Preview 插件](https://marketplace.visualstudio.com/items?itemName=bierner.github-markdown-preview)

[VSCode 官方文档 - Markdown and Visual Studio Code](https://code.visualstudio.com/Docs/languages/markdown)

### Joplin

[Joplin](https://joplinapp.org/)是一款开源的markdown笔记软件，在官网下载安装即可使用，支持的markdown特性相当丰富

有全平台支持，无论是linux，windows，macos还是android，ios都有对应的软件可以用，可以做到全平台操作逻辑统一

有自己独特的浏览器插件，可以做到截图记笔记之类的

搜索，tag一类的功能完备

支持导出html/pdf

可以和Onedrive之类的平台，并且有自己的Joplin Cloud，实现云同步

除了Joplin Cloud，都是免费的

### StackEdit

[StackEdit](https://stackedit.io/)同样是一款开源软件，只需要浏览器即可运行

具有pwa支持，于是可以做到近似原生app的体验，性能开销小的同时，支持markdown特性丰富

可以连接到云平台，实现同步

部分功能需要付费，但可以self-host

## markdown的格式

接下来我们来学习如何编写markdown

markdown经历了一系列的标准修订之后有了多种多样的语法，但是实际上平时遇到的并不多，本文也只是挑选一部分常用的作为大家的入门

如果需要深入了解，可以看看下面这些

[Markdown Guide](https://www.markdownguide.org)

### 换行和分段

如果想在markdown中实现换行可以在行末空两格，对应html中的`<br>`

两行文字之间空一行表示分段，在html中会产生两个`<p>`

### 标题

markdown用`#`的数量表示几级标题，最高六级，这对应了html中的`<h1>`到`<h6>`

像编写html一样，不要将`#`用于更改文字大小，它被用于表示文章的层级结构

一般来说，如果写一篇文章，首先需要一个大标题，然后按照部分写小标题，再用更小的标题来说明每个部分（可以参照本篇文章）

另外标题也可以作为锚点，可以实现文章各部分的跳转，[试试这个：跳转至 markdown的格式](#markdown的格式)

以下是关于标题格式的一些约定俗成，一般是这么写的，不过不用过于在意这些规则

- 要有大标题
- 一般来说，标题等级是层层递进的，一级标题下面是二级标题，不会出现跨级标题
- 如果标题层数过多，可以考虑用其他的并列格式实现。*有一种说法是为了文章的可读性，一般只用到4级标题，需要按照使用情况具体分析*
- 如果标题重名，跳转链接内可以选择跳转哪个标题，因此不必太过担心标题重名的问题

### 代码

两个`` ` ``之间的文字被视作代码，对应html中的`<code>`

### 代码块

`` ``` ``用于标示代码块，并且同时可以在第一行末尾标注语言，会影响到代码高亮，例如：

```` markdown
``` cpp
int main() {
    return 0;
}
```
````

### 链接

链接的基本格式：`[说明](https://fwlink)`，对应html中的`<a>`

说明不一定是文字，一些markdown格式可以嵌套进说明，参考[第01话 markdown进阶 - 嵌套](第01话%20markdown进阶.md#嵌套)

### 图片

图片的基本格式就是在链接前面加上叹号：`![说明](https://imgurl)`，对应html中的`<img>`

同理，也可以直接写本地目录下的链接

## 小结

以上是对Markdown的一个非常初始的介绍，目的仅仅是为了让同学们了解这个工具（也是为了同学们能看到这份教程）

欲学习更多markdown的技术，成为markdown能力者，请跟随茵蒂克丝进入[Markdown进阶](第01话%20markdown进阶.md)
