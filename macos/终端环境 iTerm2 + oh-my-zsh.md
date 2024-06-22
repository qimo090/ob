---
created: 2024-06-21T22:43
updated: 2024-06-22T11:27
url: https://www.poloxue.com/posts/2023-10-16-zsh-themes-and-plugins
---
## 为什么使用 zsh ？

Zsh，全称Z Shell，是一种功能强大的UNIX shell（命令行解释器），也是一种脚本语言。Zsh是Bourne Shell（sh）的扩展，结合了Bourne Shell、Korn Shell（ksh）和C Shell（csh）的功能，并增加了许多独特的特性。

## 安装

对于不同系统，zsh 的安装命令，如下所示：

Debian

```shell file:Debian
apt install zsh
```

Centos

```shell file:Centos
yum install -y zsh
```

Arch Linux

```shell file:"Arch Linus"
pacman -S zsh
```

Fedora

```shell title:Fedora
dnf install zsh
```

MacOS

对于 macOS 系统的用户，MacOS 的默认 shell 从 2019 开始以前替换为 zsh，该步骤可省略。可阅读：[What is Zsh? Should You Use it?](https://linuxhandbook.com/why-zsh/#:~:text=Zsh%20is%20more%20powerful%20and,more%20advanced%20features%20shipped%20in.) 其中有介绍为什么 2019 macOS 将默认的 shell 从 bash 切换到 zsh。

我看下来，主要原因就是版权问题啦。

如果你是个老古董，还是用 MacOS 2019 之前的系统，可通过如下命令安装：

```shell
brew install zsh
```

安装完成后，将 zsh 设置为默认 shell，命令如下所示：

```ts
chsh -s /bin/zsh
```

通过如下命令检查下是否成功。

```shell
echo $SHELL
zsh
```

## oh-my-zsh

[oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh) 是用于管理 zsh 配置的轻量级框架，具有开箱即用的特点，而且它提供了大量内置插件。

## 安装

通过 curl 命令

```shell file:curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

通过 wget 命令

```shell title:wget
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## 内置插件

重点来了，接下来我们一起来看看 zsh 的效率神器 - 插件能力吧。

我先给大家推荐 7 款常用的插件，其中 5 个是 oh-my-zsh 的内置插件。考虑内容不宜太长，下期会再推荐 6 个插件。

oh-my-zsh 提供的所有内置插件，都可以在仓库 [ohmyzsh/ohmyzsh/plugins](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins) 中找到，每个插件都有相应的介绍文档。

本教程将要介绍的 5 个 oh-my-zsh 内置插件，如下所示：

- [git](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git)，Git 插件，其实就是提供一些常用的 git 命令别名。
- [web-search](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/web-search)，命令行打开搜索引擎，已支持大部分搜索引擎；
- [jsontools](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/jsontools)，用于格式化 json 数据；
- [z](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/z)，基于历史访问目录的快速跳转；
- [vi-mode](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/vi-mode)，使用 vi 模式编辑命令行；
