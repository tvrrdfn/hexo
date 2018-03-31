title: 如何在Jenkins中给Git自动打Tag？
author: Ao
tags:
  - jenkins
  - git
categories:
  - git
  - jenkins
date: 2018-03-08 10:56:00
---
>如果希望能在每次发布操作后，及时的打上Tag。我们可以在Jenkins中通过利用GIT Publisher这个插件来完成需求.

#### 插件依赖
**GIT Publisher**

#### 操作及配置
1. 在 **构建后操作** 中选择 **GIT Publisher**。
2. 点击 **Add Tag** 按钮，出现设置界面。
3. **Tag to push** 可以按分支添加标签格式，例如：**master-$BUILD_ID**. **$BUILD**可以根据实际情况替换成其他变量，例如时间戳。
4. **Create new tag** 一定要勾选。
5. **Target remote name** 默认填入 **origin**

以上完成，在下次执行任务的时候就能自动在Git上打Tag了。


#### 资源
1. [Jenkins的插件安装及管理](http://www.cnblogs.com/linJie1930906722/p/5965626.html)