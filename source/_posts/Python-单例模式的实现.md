---
title: Python 单例模式的实现
date: 2015-08-20 18:42:17
tags: [python]
---


> 单例模式，也叫单子模式，是一种常用的软件设计模式。 在应用这个模式时，单例对象的类必须保证只有一个实例存在。 许多时候整个系统只需要拥有一个的全局对象，这样有利于我们协调系统整体的行为。(来自：维基百科)

本文主要介绍 Python 中实现单例模式的几种方法。

### 使用 __new__ 方法

``` Python
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            orig = super(Singleton, cls)
            _instance = orig.__new__(cls, *args, **kwargs)
            cls._instance = _instance
        return cls._instance

class MyClass(Singleton):
    a = 1
```

### 共享属性

``` Python
class Borg(object):
    _state = {}
    def __new__(cls, *args, **kw):
        ob = super(Borg, cls).__new__(cls, *args, **kw)
        ob.__dict__ = cls._state
        return ob

class MyClass2(Borg):
    a = 1
```

### 装饰器版本

``` Python
def singleton(cls):
    instances = {}
    def getinstance(*args, **kw):
        if cls not in instances:
            instances[cls] = cls(*args, **kw)
        return instances[cls]
    return getinstance

@singleton
class MyClass:
  ...
```

### import方法

``` Python
# mysingleton.py
class My_Singleton(object):
    def foo(self):
        pass

my_singleton = My_Singleton()

# to use
from mysingleton import my_singleton

my_singleton.foo()
```
