---
title: Python 修改 pip 镜像源
date: 2015-02-09 19:17:20
tags: [Python]
---

使用 Python 的童鞋免不了需要 `pip` 来安装第三方依赖。但由于官方源在国外，下载很慢或者直接连接不上的情况时有发生。所以使用一个靠谱的镜像源就很有必要了。

这里推荐使用豆瓣的镜像源，[https://pypi.doubanio.com/simple/](https://pypi.doubanio.com/simple/)。

### 还没有安装 pip？

``` bash
# 下载安装文件
wget https://bootstrap.pypa.io/get-pip.py
# 执行安装
sudo python get-pip.py
```

### pip 源修改

修改源十分简单，只需配置用户目录下的 `.pip/pip.conf` 文件即可。步骤如下

``` bash
cd ~
mkdir .pip
cd .pip
touch pip.conf
```

接着在 `pip.conf` 写入以下内容：

```
[global]
index-url = https://pypi.doubanio.com/simple/
```

之后使用 `pip` 命令就会直接从指定的源安装了。

上面使用的是豆瓣源，也可以使用阿里云源：

```
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/

[install]
trusted-host = mirrors.aliyun.com
```
