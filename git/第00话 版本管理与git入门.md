---
author:
- LTSlw
- dedfaf
tags:
- basic
- getting-start
- git
date: 2023-10-13
lastmod: 2024-02-28
---

# 版本控制与git入门

你是一名普通的计算魔法学学生，你最近接到了一个奇怪的白袍子小萝莉的任务：帮助她编写一本关于计算魔法的入门书籍

今天的课程结束后，你来到你们工作组的教室，然后那几个混蛋让你从你们群里114514个文件还水了半小时的破烂里找到你要处理的事情和文件，在⑨个小时后你找到了你要干的事，整理好了项目文档，然后你妹妹就催你快点去回家便利店买最新魔法禁书目录了...

扯远了...( ﾟ∀。)，这一章我们来介绍开发过程中进行版本管理的方法 - `git`

## 什么是版本控制

`版本控制`是开发过程中用于记录开发过程，协调工作的办法

在通常的开发流程中，项目在不断的修改过程中必然会产生很多版本，也就不可避免出现这些情况：

- 新版本出现问题，需要回滚到旧版本
- 多人合作，每个人都对项目进行了不同程度的修改，需要合并在一起
- 有人在代码里留下了低级错误，需要抓到这个人，并在第一时间嘲笑他（雾
- ……

每个版本都复制粘贴一份必然是低效而混乱的，此时就需要`版本控制系统`（`VCS`）帮助你们记录版本改动，管理代码修改历史

## 比较各种VCS

### 库模式

`库模式`表示源码库各个副本之间的关系。分为`集中式版本管理系统`（`CVCS`）和`分布式版本管理系统`（`DVCS`）两种

CVCS是基于一台集中管理的主服务器，所有人都直接在这台服务器上进行操作。CVCS的优势在于，每个人的工作都是同步进行的，甚至可以实时观看别人在干什么或者同步编辑。CVCS也同时易于管理权限，与操作系统类似，按照用户与文件授予不同权限即可。但其缺点也显而易见，首先CVCS要求开发人员必须保证可以在开发始终连接到中心服务器，限制了开发环境，其次服务器的宕机时也必然会使开发陷入停滞

而DVCS中，每个客户端都会和服务器主机一样拥有完整的代码仓库，参与人在本地进行编辑后提交至主机的仓库中。DVCS的利弊基本与CVCS相反，不同开发者的各自在自己的计算机上完成开发，最后找个可以连接到服务器的时间提交即可，也不必担心服务器宕机，甚至理论上无需服务器也能完成版本控制。但是，不同开发人员互相不能实时看到其他人的修改，就要处理不同人修改造成的冲突，处理起来比较复杂

### 并发模式

`并发模式`表示如何管理工作副本的变化，主要也有两种：`合并`和`锁定`

合并模式允许不同的开发者自由编辑，有时更改可以直接合并（比如追加），有时则会产生`冲突`，在开发者提交时，VCS会报告可能的冲突，然后由其本人或项目管理者选择哪些更改被合并（也称作处理冲突）。**分布式版本控制几乎都是合并的并发模式**。它的好处在于开发者可以各自按照自己的思路修改项目，但也造成处理冲突有时会比较麻烦

锁定模式是让文件在一定的时间内仅对特定的一个（或几个）开发者开放编辑，而其他人在此期间则不能对该文件编辑。它的利弊基本也和合并式相反，不用处理冲突，但如果多人同时修改项目就需要事先协调好

### 是不是开源自由软件，使用费用，是否积极维护

这其实是评判软件的一般标准，此处便不细说。

一般来说开源，意味着使用者有权审查、编辑自己使用的软件。使用费用则是要根据自身需求在技术支持和价格之间进行权衡。积极维护的软件在未来有机会修复漏洞和bug

### 我该选哪个VCS

由于VCS在项目中几乎是必备的，历史上有形形色色的软件被开发出来，也可以看看[Wikipedia - 版本控制软件比较](https://zh.wikipedia.org/zh-hans/%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E8%BD%AF%E4%BB%B6%E6%AF%94%E8%BE%83)，里面包括具体的各种软件，本部分在编写时也参考了里面的内容

## git是什么

[`git`](https://git-scm.com/)是本系列教程推荐的版本控制系统，诞生于linux开发过程中，它是一个分布式，采用合并模式的开源自由免费软件（许可证：GNU GPLv2），可以说是现在最流行的版本控制系统，只要你肯搜索，庞大的用户群体便是最好的技术支持。你也许之前听说过github，gitlab或gitee这类代码托管平台，他们就是基于git运行的版本控制平台，茵蒂克丝会在以后介绍这类平台的使用方法

## 使用git的准备工作

### 一些资料

- [Pro Git](https://git-scm.com/book/zh/v2)，git自己出的书，在CC BY-NC-SA 3.0协议下分享，本文也有很多内容引用自这本书，如果你愿意去读的话，就完全没必要去看下面的内容了
- [Git cheat sheet](https://education.github.com/git-cheat-sheet-education.pdf)，包含一些常用命令，如果有命令想不起来，可以首先看看这个，基本可以找到，链接里是Github制作的版本，实际上也有其他组织制作的版本，都叫这个名字，不喜欢的话可以搜一搜其他的

*需要注意的一点是，这些资料都可用，但不是最新，git现在已经把`checkout`命令做了拆分，虽然git一直保持了兼容性，所有的命令还都可用，但是`checkout`有时候有一些危险性，笔者建议优先使用和学习`switch`和`restore`命令，本文也优先使用非`checkout`的版本*

### 安装git

#### Linux

绝大部分发行版的包管理器里都内置了git，可以参照[官方文档](https://git-scm.com/download/linux)，不用包管理器也可以手动安装（此处不展开说）

##### Debian

``` shell
apt install git
apt install git-all # with all sub-packages
```

##### Arch

``` shell
pacman -S git
```

#### Windows

Windows上的git实际使用的是[`Git for Windows`](https://gitforwindows.org/)项目，但也可以从git官网[下载](https://git-scm.com/download/win)到

限于篇幅，就不附截图了，跟着安装向导走即可，可以辅助运用翻译软件，按照自己需要调整配置

**推荐配置（基于默认配置）：**  
`Windwos Terminal`（win11 默认）用户勾选`(NEW!) Add a Git Bash Profile to Windows Terminal`（Select Components页面）  
在Choosing the default editor used by Git页面，选择常用代码编辑器（例如：VSCode）

也可以使用`Chocolatey`一类的管理器安装，也不展开

#### MacOS

*由于笔者没有Mac，此部分是未经验证的*

可以使用安装包安装，[下载](https://sourceforge.net/projects/git-osx-installer/)

也可以使用homebrew等工具安装，详见[文档](https://git-scm.com/download/mac)

### 配置git

配置git可以使用命令git config来进行，首先要进入命令行，如Linux下的terminal，Windows下的cmd等

下面的命令中很多都有`--global`参数，表明这是全局设置，去掉它并在仓库目录下运行则作为当前仓库的设置

一般来说，我们有一个比较通用的全局设置，可以减少对单独仓库的配置

#### 获取帮助

除了查看在官网的[文档](https://git-scm.com/docs)，直接从命令行里获取帮助可能更方便

``` shell
git -h             # 获取git简要帮助，-h表示--help
git <command> -h   # 获取git指定命令的简要帮助
git help <command> # 获取指定命令的详细帮助
git help -g        # 获取git内置向导，-g表示--guides，是的，git内部已经自带了一套教程
```

#### 用户配置

``` shell
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

将上面的用户名和邮箱修改为自己的并运行

#### 文本编辑器

``` shell
git config --global core.editor code
```

也可以指定启动参数和完整路径，但要将整个命令用引号扩起来，例如：

``` shell
git config --global core.editor "nano -w"
```

#### 显示Unicode路径（显示中文）

路径中非Ascii字符默认会以八进制显示，有时会导致不显示想要显示的字符，这是为了兼容不同的shell。如果你的shell支持显示utf-8字符，可以手动配置

``` shell
git config --global core.quotepath false
```

#### 查看当前配置

列出所有配置

``` shell
git config --list
```

查看指定配置

``` shell
git config <key>
```

其中`<key>`可以是上面的`user.name`，`core.editor`等

### 有关git的概念

#### 基本概念

- `仓库`（`repository`）：被git管理的一个文件夹（`.git`），不要手动修改，是git最重要的部分
- `工作区`（`working directory`）：从仓库中提取出来的某个特定版本，这是我们直接修改的部分
- `暂存区`（`staging area`，索引）：实际是一个文件，在`.git`中
- `分支`（`branch`）：将开发从某个版本分离，与其他分支独立，每个仓库有一个`主分支`（`default branch`），一般命名为`master`或`main`
- `标签`（`tag`）：标签是给特定的版本起一个好名字，常用版本号命名，与分支不同，标签打在特定的提交上，后续的更改不影响之前的标签
- `提交`（`commit`）：把已修改和已暂存的保存在数据库中成为已提交状态
- `推送`（`push`）：把本地的更改同步到远程仓库
- `拉取`（`pull`）：把远程仓库的更改同步到本地

#### 文件的状态

所有文件只有两种状态，`未跟踪`（`untracked`）和`已跟踪`（`tracked`），已跟踪又分为3种，`已修改`（`modified`）、`已暂存`（`staged`）和`已提交`（`committed`）

- 未跟踪：未被纳入版本控制
- 已跟踪：被纳入了版本控制
- 已修改：修改了文件，但还没保存到数据库中
- 已暂存：表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中
- 已提交：数据已经安全地保存在本地数据库中

![文件的状态变化周期*（图源《Pro Git》 CC BY-NC-SA 3.0）*](imgs/00_00_lifecycle.png)

git的一般工作流程：

1. 在工作区中修改文件
2. 将你想要下次提交的改选择性地暂存，这样只会将更改的部分添加到暂存区
3. 提交更新，找到暂存区的文件，将快照永久性存储到 Git 目录

## 使用git

### 仓库

#### 本地初始化仓库

先把当前目录切换到工作目录（`cd`命令），下面的命令会在`./work_directory`下创建一个`.git`文件夹，但工作目录里的文件还是未被跟踪的

``` shell
cd ./work_directory
git init
```

#### 克隆仓库

``` shell
git clone https://github.com/bit-acca/ACCA-Index.git
```

#### 查看远程仓库

``` shell
git remote
```

#### 添加远程仓库

``` shell
git remote add <remote> <url>
```

例如：

``` shell
git remote add github https://github.com/example/example.git
git remote add gitlab https://gitlab.com/example/example.git
```

#### 重命名远程仓库

``` shell
git remote rename <remote_from> <remote_to>
```

#### 移除远程仓库

``` shell
git remote rm <remote>
```

#### 从远程仓库拉取

``` shell
git pull <remote>  # 常用，会自动fetch并merge，需要设置追踪分支，但一般是自动的
git fetch <remote> # 从远程仓库拉取所有数据，fetch只会拉取数据，并不会完成合并等操作
```

#### 查看远程仓库

``` shell
git remote show <remote> # 
```

### 文件

#### 跟踪文件/暂存文件

跟踪文件和暂存文件都使用`git add`命令，每次修改文件都需要重新运行`git add`命令把文件加入暂存区，才能把最新的修改提交

``` shell
git add README.md # 跟踪并暂存指定文件
git add .         # 跟踪并暂存当前目录下所有文件，即全部跟踪并暂存
```

#### 移除文件（取消跟踪文件）

``` shell
git rm README.md
```

#### 移动文件

git仓库中的文件如果需要重命名或移动，可以在git中执行

``` shell
git mv file_from file_to
```

`mv`命令等价于先`rm`后`add`

#### 检查文件状态

``` shell
git status
git status -s # -s表示--short，得到更加简洁的输出
```

#### 忽略文件

不需要纳入git管理的文件可以写进`.gitignore`文件，由于其接受一套类似正则表达式的语法，稍微有一些麻烦，一般来讲如果路径是确定的，直接填写相对工作目录的路径即可，一般要写表达式也不会太麻烦，下面给出一些例子：

``` gitignore
# 这是我的.gitignore # '#'以后的部分作为注释，被git忽略
trash.txt           # 忽略trash.txt
*.o                 # 忽略所有.o文件
!acca.o             # 但保留acca.o
```

git允许多个`.gitignore`文件

很多时候也可以用现成的[模板](https://github.com/github/gitignore)


#### 忽略修改

``` shell
git restore .          # 恢复工作区的所有文件到上一次提交
git checkout --        # checkout版本，和上面的命令等价
git restore <file>     # 只把<file>恢复到上一次提交
git checkout -- <file> # checkout版本，和上面的命令等价
```

`git checkout`会忽略所有的修改，**这个操作是不可逆的，使用时务必确认没有需要保留的修改**

#### 查看修改

```
git diff          # 显示所有暂存和未暂存文件的修改
git diff --staged # 仅查看已暂存文件的修改
```

**注意，`git diff`命令只显示未暂存的更改，而不是自上次提交的更改**

### 提交

#### 提交更新

``` shell
git commit           # git会启动默认编辑器，请在里面输入这次提交的描述并保存 
git commit -m ‘desc’ # 在-m参数后面直接编写描述，不进入编辑器
git commit -a        # 不需要git add，直接提交所有已经追踪的文件（不建议）
```

在输入`git commit`后，你需要对你这次commit写一个简单的介绍（Commit Message），默认编辑器会以注释的形式显示所有你做出的改动，你可以通过取消注释的方式列举你改动的文件(但一般不在Commit Message里列举具体改动了哪个文件，简单说一下自己添加修改了哪些内容即可)。

对每次Commit，Commit Message是必填的，如果在编辑器中没有写任何不是注释的字符，那么git会取消这次commit，*就当什么都没有发生*

#### 撤销提交

``` shell
git commit --amend
```
这条命令可以用于修改上一次提交，实际上是用第二次提交代替第一次，可看示例

``` shell
git commit -m 'initial commit'
git add forgotten_file
git commit --amend
```

#### 查看历史

``` shell
git log
git log -p     # -p表示--patch，显示提交的差异
git log --stat # 显示提交的统计信息
```

### 标签

#### 列出标签

``` shell
git tag
```

#### 创建标签

git支持两种标签：轻量标签（lightweight）与附注标签（annotated）

``` shell
git tag <tag>              # 创建名为<tag>的轻量标签
gti tag <tag> <commit>     # 在提交<commit>上创建名为<tag>的轻量标签
git tag <tag> -a           # 创建名为<tag>的附注标签，git会启动默认编辑器，请在里面输入附注并保存
git tag <tag> -a -m 'anno' # 创建名为<tag>的附注标签，在-m参数后面直接编写附注，不进入编辑器
```

#### 查看标签

``` shell
git show <tag>
```

#### 删除标签

``` shell
git tag -d <tag>
```

#### 检出标签

``` shell
git switch -d <tag>
git checkout <tag> # 和上面的命令等价，但可以看出，switch要求显地示使用-d参数，更加安全
```

可以检出标签后简单调整测试，并把更改提交到仓库，但提交会处在`分离头指针`（`detached HEAD`）状态，提交不属于任何分子，只能用提交哈希访问。如果要在某个标签上提交修改，建议先创建一个新分支，可以使用下面的命令：

``` shell
git switch -c <branch> <tag>
git checkout -b <branch> <tag> # checkout版本，和上面的命令等价
```

### 分支

#### 列出分支

``` shell
git branch
git branch --[no-]merged # 查看已经合并或尚未合并到当前分支的分支
```

#### 创建分支

``` shell
git branch <branch>
git switch -c <branch>   # 创建并切换到<branch>，-c表示--create
git checkout -b <branch> # checkout版本，和上面的命令等价
```

#### 切换分支

``` shell
git switch <branch>
git checkout <branch> # checkout版本，和上面的命令等价
```

#### 删除分支

``` shell
git branch -d <branch>
```

#### 合并分支

``` shell
git switch <branch_to>
git merge <branch_from>
```

执行了以上命令之后，如果报错中有`CONFLICT`字样，说明不能自动合并，产生了冲突，那么如何处理冲突呢？

首先执行`git status`查看产生冲突的文件和具体冲突的位置，之后进入有冲突的文件中，git会把冲突的位置用`<<<<<<<`、`=======`、`>>>>>>>`标出，手动修改后用`git add`、`git commit`提交更改

还可以使用`git mergetool`在gui中处理冲突，手动修改后也要提交更改，实际使用区别不大，所以也就不展开说了

#### 远程分支

远程分支用`<remote>/<branch>`命名，本地分支的改变不影响远程分支，可以使用`git fetch`与远程仓库同步

#### 推送到远程分支

``` shell
git push <remote> <branch> # 把<branch>的更改推送到<remote>
```

#### 跟踪远程分支

``` shell
git switch -c <branch> <remote>/<branch>
git switch --track <remote>/<branch>       # 和上面的命令等价，要求<branch>没有被占用
git switch <branch>                        # 和上面的命令等价，要求<branch>没有被占用
git checkout -b <branch> <remote>/<branch> # checkout版本，和上面的命令等价
git checkout --track <remote>/<branch>     # checkout版本，和上面的命令等价
git checkout <remote>/<branch>             # checkout版本，和上面的命令等价

git -u <remote>/<branch>                   # 设置已有的本地分支跟踪一个远程分支，-u表示--set-upstream-to

git branch -vv                                    # 查看跟踪远程分支
```

跟踪的分支才可以使用`git pull`

#### 删除远程分支

``` shell
git push <remote> --delete <branch>
```

## GUI

如果你觉得命令太复杂，git也自带了两个gui

``` shell
gitk
git gui
```

你的系统可能需要事先安装依赖

**Debian**

``` shell
apt install git-gui gitk
```

**Arch**

``` shell
pacman -S tk
```

git也有很多第三方的gui封装，例如[Gittyup](https://murmele.github.io/Gittyup/)

[官网](https://git-scm.com/downloads/guis/)里也列出了很多gui客户端，可以选择自己喜欢的使用
