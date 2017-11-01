title: 使用markdown自动生成Restfull风格的文档
author: Ao
date: 2017-09-11 11:04:22
tags:
---
### mkdocs环境搭建
pip是Python的包管理器，类似于nodejs中的npm、ruby的gem。
安装都比较简单，windows下需要配置环境变量。
mac 已经自带python，但是ipython要自己安装。
##### 1.安装 pip 
```javascript
sudo easy_install pip

// 如果执行报错，可以执行： sudo easy_install -U pip
```
<!--more-->
##### 2.使用pip安装mkdocs
```javascript
pip install mkdocs
pip install mkdocs-material

// mkdocs-material 是一款主题
```

##### 3 启动
```javascript
mkdocs serve
```
mkdocs内置server会将markdown编译成html并部署到8000端口，直接 http://localhost:8000 访问就可以了。