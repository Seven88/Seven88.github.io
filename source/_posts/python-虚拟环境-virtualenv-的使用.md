---
title: python 虚拟环境 virtualenv 的使用
date: 2015-01-29 12:06:16
tags: [Python]
---

## 什么是 virtualenv？

官方说明：

> virtualenv is a tool to create isolated Python environments.

## 为什么要用虚拟环境？

Python 开发环境中，经常会有库依赖、版本以及系统权限等问题，比如不同项目使用的 Django 版本不同，如果直接使用系统环境，项目将无法同时运行。使用虚拟环境就可以解决这个问题。

## 如何使用？

使用 `pip` 安装即可：

``` bash
sudo pip install virtualenv
```

具体可参考[官方文档](https://pip.pypa.io/en/latest/installing.html) 。

本文推荐另一个更为好用的工具 `virtualenvwrapper`，它对 `virtualenv` 进行了一些非常方便使用的包装。

<!-- more -->

使用 `pip` 安装：

``` bash
sudo pip install virtualenvwrapper
```

安装后即可使用了，常用命令如下：

### mkvirtualenv

``` bash
mkvirtualenv envname
```

创建一个名为 envname 的虚拟环境，并自动切换到该环境。

创建后的环境已自动安装 `pip`，之后在环境中可直接安装需要的依赖，如 `pip install flask`。

### workon


``` bash
workon envname
```

切换到名为 envname 的虚拟环境。

### deactivate


``` bash
deactivate
```

退出当前虚拟环境，使用系统环境。


### setvirtualenvproject


``` bash
setvirtualenvproject
```

指定所在目录为当前虚拟环境的默认目录，当下次切换到该环境中，自动进入该目录。

### rmvirtualenv

``` bash
rmvirtualenv envname
```

删除名为 envname 的虚拟环境。
