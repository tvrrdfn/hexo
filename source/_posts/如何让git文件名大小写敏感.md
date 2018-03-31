title: '如何让git文件名大小写敏感 '
author: Ao
tags:
  - git
categories:
  - git
date: 2018-03-16 18:41:00
---
git 默认不区分文件名大小写


当你创建一个文件后,叫 readme.md 写入内容后 提交到线上代码仓库.

然后你在本地修改文件名为 Readme.md 接着你去提交,发现代码没有变化.

```
git status
```
无任何提示信息.
<!--more-->
其实 git 默认对于文件名大小写是不敏感的,所以上面你修改了首字母大写,但是git 并没有发现代码任何改动.

那么如何才能让 git 识别文件名大小写变化.

#### 一  配置git 使其对文件名大小写敏感

```
git config core.ignorecase false
```

#### 二 从git 本地仓库删除此文件,然后添加再提交
(1) 删除
```
git rm readme.md
```
(2) 重新添加
```
git add Readme.md
```
(3)提交
```
git commit -m 'Readme.md'
```

推荐第一种方法,配置好git 对文件名大小写敏感.