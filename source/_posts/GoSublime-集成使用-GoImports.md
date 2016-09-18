---
title: GoSublime 集成使用 GoImports
date: 2016-09-18 16:04:09
tags: [Go, Sublime Text]
---

```
imported and not used: 'fmt'
# 或者
undefined: fmt in fmt.Sprintf
```

是否厌倦了编译 `Go` 文件时看到类似以上的错误信息？让 `GoImports` 来拯救你！

由于笔者偏爱 `SublimeText`，这里主要介绍怎样在 `SublimeText` 中使用 `GoImports`。

1. 确认 `$GOPATH/bin` 在 `$PATH` 中。
2. go get -u golang.org/x/tools/cmd/goimports，安装 `GoImports`。
3. 安装 [GoSublime](https://github.com/DisposaBoy/GoSublime)。
4. 编辑 `GoSublime.sublime-settings`，添加 `"fmt_cmd": ["goimports"]`。
5. 测试 `import`，添加、删除各种包，保存文件会自动删除、添加，Job Done。
