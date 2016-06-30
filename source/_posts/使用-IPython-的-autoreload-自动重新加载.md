---
title: 使用 IPython 的 autoreload 自动重新加载
date: 2015-06-30 18:23:57
tags: [IPython, Python]
---

[IPython](http://ipython.org/) 是极好用的 Python 交互 shell。

先来看一个使用场景，运行 IPython：

``` Python
In [1]: from a.b imort c
In [2]: c()
hello world  # c 函数的功能 打印 hello world
# 这时修改了 c 函数，在 'hello world' 后面加一个 '!'
In [3]: c()
hello world  # 会发现并不是修改后的结果
```

通常做法是重启 shell，重新 import，这样当然可以，但我们可以优雅的使用 IPython 的 autoreload 来处理：

``` Python
In [1]: from a.b imort c
In [2]: c()
hello world  # c 函数的功能 打印 hello world
# 这时修改了 c 函数，在 'hello world' 后面加一个 '!'
In [3]: %load_ext autoreload
In [4]: %autoreload 2
In [5]: c()
hello world!  # 自动重新加载了
```

`%load_ext autoreload` + `%autoreload 2`，两步轻松实现自动加载，是不是很爽？

参考文档：
[http://ipython.readthedocs.io/en/stable/config/extensions/autoreload.html](http://ipython.readthedocs.io/en/stable/config/extensions/autoreload.html)
