---
author:
- LTSlw
tags:
- android
date: 2024-02-21
lastmod: 2024-02-21
---

# 第1话 安装Android Studio

`Android Studio`是Android官方推出的IDE，用于Android开发，被广泛使用。绝大部分工作都可以在里面完成，比如编写代码、设计UI、构建应用、模拟不同的设备调试

## 配置要求

不同的平台的配置要求略有不同，总结一下

最低配置：

- 8GB RAM
- 8GB DISK
- 1280*800的屏幕
- 不太旧的cpu和操作系统

推荐配置：

- 16GB RAM
- 16GB SSD
- 1920*1080的屏幕

只看最低配置的话，其实要求不高，电脑配置虽然越高越好，但不必为此焦虑。详细的配置要求可以看[文档](https://developer.android.com/studio/install)

## 安装

官方的[文档](https://developer.android.com/studio/install)已经非常简单了，可以说是已经做到了无脑安装，推荐至少将文档看一遍

### Arch

下面介绍一个Arch Linux使用包管理器安装Android Studio的方法。Android Studio不是真正意义上的自由软件，因此不在官方源中，但可以在[AUR](https://aur.archlinux.org/packages/android-studio)中找到它

#### 启用multilib源

`Android SDK`依赖32位库，所以需要先启用`multilib`源，可以编辑`/etc/pacman.conf`

```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

#### 安装本体和依赖

``` shell
yay -S android-studio android-sdk-cmdline-tools-latest-dummy android-sdk-build-tools-dummy android-sdk-platform-tools-dummy android-platform-dummy android-emulator-dummy
```

使用dummy包是允许`SDK Manager`管理SDK的同时安装好依赖，避免Pacman和SDK Manager同时插手SDK的管理，造成混乱

#### 设置网络

安装之后，即可启动Android Studio，此时会尝试联网，如果联网失败会有设置proxy的弹窗。填写完proxy之后建议测试连接，大量的组件要从`dl.google.com`下载，网络环境很重要

#### 安装组件

其实dummy包还帮我们做了添加`PATH`的工作，但它默认SDK存放在`/opt/android-sdk`，Android Studio默认将SDK存放在`~/Android/Sdk`，如果希望利用上自动配置的`PATH`，可以遵循以下步骤：

1. mkdir /opt/android-sdk
2. chmod 777 /opt/android-sdk
3. `Install Type`可以选择`Custom`，在下一页`SDK Components Setup`中把`Android SDK Location`改为`/opt/android-sdk`

![Components](./imgs/01_01_components.png)

#### 完成安装

接下来你需要同意许可协议并等待下载结束

[参考 Arch Wiki](https://wiki.archlinux.org/title/Android#Android_Studio)
