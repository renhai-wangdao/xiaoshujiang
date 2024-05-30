---
title: linux 添加字体文件
category: /小书匠/日记/2024-05
emoji: "😜"
grammar_cjkRuby: true
---

----------

# 1、准备好字体，可以从网上下载，也可以直接从咱们的windows电脑中拷贝出来：


```text
C:\Windows\Fonts 从这里拷贝windows上的字体
```

# 2、上传到服务器上
Linux字体目录是 /usr/share/fonts 我们在这个目录里面新建一个自己能够记住的目录，然后放入我们需要的字体
```text
cd  /usr/share/fonts 
mkdir new
cd new
```
# 3、加载这些字体
```text
fc-cache -fv
```


