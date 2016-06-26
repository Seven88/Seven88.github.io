---
title: 【译】为什么Python中没有Switch/Case语句
date: 2015-09-05 18:13:40
tags: [翻译, Python]
---

**英文出处：[pydanny.com](http://www.pydanny.com/why-doesnt-python-have-switch-case.html)**
**校稿：[伯乐在线 - 唐尤华](http://www.jobbole.com/members/tangyouhua)**

不同于我用过的其它编程语言，Python 没有 switch / case 语句。为了实现它，我们可以使用字典映射：

``` python
def numbers_to_strings(argument):
    switcher = {
        0: "zero",
        1: "one",
        2: "two",
    }
    return switcher.get(argument, "nothing")
```

这段代码在 JavaScript 中相当于：

``` javascript
function(argument){
    switch(argument) {
        case 0:
            return "zero";
        case 1:
            return "one";
        case 2:
            return "two";
        default:
            return "nothing";
    };
};
```

Python 代码通常比处理 case 的标准方法更为简短，也可以说它更难理解。当我初次使用 Python 时，感觉很奇怪并且心烦意乱。而随着时间的推移，在 switch 中使用字典的 key 来做标识符变得越来越习以为常。

<!-- more -->

### 函数的字典映射

在 Python 中字典映射也可以包含函数或者 lambda 表达式：

``` python
def zero():
    return "zero"

def one():
    return "one"

def numbers_to_functions_to_strings(argument):
    switcher = {
        0: zero,
        1: one,
        2: lambda: "two",
    }
    # Get the function from switcher dictionary
    func = switcher.get(argument, lambda: "nothing")
    # Execute the function
    return func()
```

虽然 zero 和 one 中的代码很简单，但是很多 Python 程序使用这样的字典映射来调度复杂的流程。

### 类的调度方法

如果在一个类中，不确定要使用哪种方法，可以用一个调度方法在运行的时候来确定。

``` python
class Switcher(object):
    def numbers_to_methods_to_strings(self, argument):
        """Dispatch method"""
        # prefix the method_name with 'number_' because method names
        # cannot begin with an integer.
        method_name = 'number_' + str(argument)
        # Get the method from 'self'. Default to a lambda.
        method = getattr(self, method_name, lambda: "nothing")
        # Call the method as we return it
        return method()

    def number_0(self):
        return "zero"

    def number_1(self):
        return "one"

    def number_2(self):
        return "two"
```

很灵活，对吧？

### 官方说明

[官方的解释](https://docs.python.org/2/faq/design.html#why-isn-t-there-a-switch-or-case-statement-in-python)说，
> 用`if... elif... elif... else`序列很容易来实现 switch / case 语句。

而且可以使用函数字典映射和类的调度方法。

可以说官方的说明并没有解释什么，只是给出了解决方案。换句话说，没有回答为什么。我认为其实官方真正想说的是：“Python 不需要 switch / case 语句”。

### 真的是这样吗？

是的。但是还有别的原因。我听牛人说过，在代码中 switch/case 语句真的很难调试。

就我个人而言，我发现当运行到大量嵌套的用作代码分支映射的字典里，上述说法就站不住脚了。想想吧，一个超过100条语句的嵌套字典，和一个嵌套100个以上 case 的 switch/case 代码块一样，都是难以调试的。

### 字典映射运行更快？

Python 没有 case 语句，使用其它语言的衡量标准是没有意义的，因为在某种语言中运行更快并不意味着在另一种语言中也一样。让我们继续。

### Python 实现方法的显著优点

有时候我会遇到 Python 的实现方法比 switch/case 语句更好用的情况，例如在运行的时候，需要从映射里添加或者删除一些潜在的选项。每当这时，多年来使用字典映射和调度方法的实践让我受益匪浅。现在我觉得，我再也无法回到依赖 switch/case 语句的日子了。

### 结束语

Python 迫使我积累了很多映射的实践经验，对我来说是塞翁失马，焉知非福。没有 switch/case 语句可用的约束，促使我想到了可能不会用来开发的方法和主意。

有意或无意中，Python 没有 switch/case 语句已成为一种社会建构，并让我成为一个更优秀的程序员。

综上所述，所以我认为这种意外的社会构建解释比官方的“用这个来代替”的说明要好得多。
