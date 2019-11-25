---
layout: post
title: "Git 常用命令"
date: 2019-06-22 14:14:51
tags:
  - 工具
  - 方法
toc: true
comments: true
---

![image](/assets/mdImg/01-gitms03.jpeg)

### 1、创建本地仓库到连接远程

0、安装 git hub 后初始化。
全局设置：先要设置提交的用户名和邮箱，不设置则无法提交代码。

```bash
git config --global user.name 名字     # 叫啥名字
git config --global user.email 邮箱     # 怎么联系你
```
<!-- more -->

去掉--global 则只在当前项目中有效

```js
git config user.name 名字     # 叫啥名字
git config user.email 邮箱    # 怎么联系你
```

查看配置信息
`git config --list` , 查看命令如何使用，如`git commit --help`

1.初始化建立本地仓库

```js
 git init
```

2.创建远程仓库：在 github 或者 gitlab 创建远程仓库
注：创建一个空的库，不需要远程库初始化
步骤：
a、在自己的 git hub 上面 New 一个仓库，
![image](/assets/mdImg/1-gitsm02.png)
3.让本地仓库和远程仓库进行关联

- SSH 方式
  git remote add origin + 远程仓库的 SSH 链接接

```js
git remote add origin <这里填远程仓库的ssh地址>
```

注: 第一次操作本地没有 SSH 密钥时，参考文档最底下的描述 4.进行添加和提交操作

```js
 git add .
    option：.点跟*，都表示所有文件，也可以写文件名
 git status
    查看暂存区状态:

 git commit -m"添加文件"
    option：-m"这里是备注信息"

 取消已跟踪的文件取消继续跟踪
 git rm --cached <name>
```

5.push 到远程

> 由于远程库是空的，第一次推送 master 分支时，加上-u 参数，Git 不但会把本地的 master 分支内容推送的远程新的 master 分支，还会把本地的 master 分支和远程的 master 分支关联起来。

```js
1.首次推送加-u可以使本地master跟远程的master关联起来，不想关联就不写
git push -u origin master：master
    option:origin后面是本地分支跟远程分支的选项,当同分支时可以简写只写master
2.第二次推送不需要加-u；本地master推送到远程dev
git push origin master：dev
```

---
###### 创建 SSH 密钥

1.创建 SSH Key

- 在用户主目录（这里在 windows 下是指 c/user/Administrator/.ssh/id_rsa）下，看看有没有.ssh 目录。
- 如果有，再看看这个目录下有没有 id_rsa 和 id_rsa.pub 这两个文件，如果已经有了，可直接跳到下一步。
- 如果没有，打开 Shell（Windows 下打开 Git Bash），创建 SSH Key：

```javascript
 ssh-keygen -t rsa -C "youremail@example.com"
```

- 需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可。
- 由于这个 Key 也不是用于军事目的，所以也无需设置密码。
- （测试的结果：C:\Users\Administrator.ssh 里面有 id_rsa 和 id_rsa.pub 两个文件，这两个就是 SSH Key 的秘钥对，id_rsa
  是私钥，不能泄露出去，id_rsa.pub 是公钥，可以放心地告诉任何人。）

  2.登陆 GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意 Title，在 Key 文本框里粘贴 id_rsa.pub 文件的内容。点“Add Key”，你就应该看到已经添加的 Key：
  **注意两点：**

- 为什么 GitHub 需要 SSH Key 呢？因为 GitHub 需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而 Git 支持 SSH 协议，所以，GitHub 只要知道了你的公钥，就可以确认只有你自己才能推送。
- GitHub 允许你添加多个 Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的 Key 都添加到 GitHub，就可以在每台电脑上往 GitHub 推送了。

  3.测试 SSH key 是否添加成功
  输入如下命令进行测试

```js
ssh -T git@github.com
```

如果出现:

```js
Hi zhanghaoming You;ve successfully auth.......
```

说明添加成功了

---

### 2、更新远程覆盖本地

```js
 git fetch --all            #fetch所有分支上的内容，也可以选择只备份一部分内容
```

```js
git reset --hard origin/master          #重置本地分支
```

```js
git pull          拉取覆盖本地
```

### 3、切换版本

> 在 Git 中，用 HEAD 表示当前版本。上一个版本就是 HEAD，上上一个版本就是 HEAD。，当然往上 100 个版本写 100 个比较容易数不过来，所以写成 HEAD~100。

- 查看提交日志（所有的提交日志，最近到最远）

```js
git log
```

- 查看提交的内容（比如更改了哪些类，删除了哪些文件等）

```js
git log -p -1  //-p 选项展开每次提交的内容差异，用-1 则仅显示最近两次更新
```

- 查看命令历史（即：我们每一个命令）

```js
git reflog
```

- 通过 git log 或者 git reflog 可以拿到每个版本的 commit_id，然后通过**切换版本/回退版本**的命令即可：

```js
git reset --hard commit_id
```

##### 回退版本流程

- 回退版本操作：

```js
  //git log 拿到commit_id
  git log
  //回到commit_id那个版本
  git reset --hard commit_id
```

- 已经回退到了之前的版本，又想回到新版本

```js
  //查看所有的命令，然后找到新版本提交的 commit_id
  git reflog
  //去到新版本
  git reset --hard commit_id
```

- 让这个文件回到最近一次 git commit 或 git add 时的状态

```js
git checkout -- readme.txt
```

### 4、解决冲突

- 合并冲突
  > 1.通过 git status 查看冲突文件
  > 2.Git 用
  > , <<<<<<<
  > 要合并的
  > , =======
  > 之前的
  > , >>>>>>>
  > 标记出不同分支的内容
  > 3.修改文件，保存，再次提交即可
  > 4.通过 git log 查看分支合并的情况

```js
  //提交的文件如果出现冲突就会出现这种提示
  CONFLICT (content): Merge conflict in readme.txt

  Automatic merge failed; fix conflicts and then commit the result.
```


## 二、分类操作详解

#### 1、add 操作

- 添加单个文件

```js
git add readme.txt
```

- 添加所有改变的文件

```js
1、添加所有内容
git add -A

2、添加新文件和编辑过的文件不包括删除的文件
git add . or *

3、添加编辑或者删除的文件，不包括新添加的文件
git add -u

4、添加同时提交内容
git commit -am"添加并提交到仓库的备注信息"
```

#### 2、分支(branch)操作

一下操作无特殊备注的**双引号均为了高亮**

- 查看分支

```js
git branch
```

- 创建分支

```js
git branch "name"
```

- 切换分支

```js
git checkout "name"
```

- 创建+切换分支

```js
git checkout -b "name"
```

- 合并某分支到当前分支

```js
git merge "name"
```

- 删除本地分支

```js
git branch -d "name"
```

- 查看远程分支列表

```js
绿色代表当前项目所在的分支，红色就是远程分支列表

git branch -a
```

- 提交本地分支到远程分支

```js
 dev:master  提交本地的dev分支到远程的master分支
 dev  提交本地的dev分支到远程的dev分支
 dev:null 提交本地的dev分支到远程的null分支，远程没有null分支会自动创建

git push origin dev:dev
```

- 从远程获取 dev 分支内容

```js
git pull origin dev
```

- 删除远程分支

```js
git push origin --delete "branchName"
```

- 重命名本地分支

```js
git branch -m "oldbranch" "newbranch"
```

- 重命名远程分支

```js
删除远程分支 -> 重名名本地分支 -> 推送new的本地分支
```

#### 3、标签(tag)操作

一下操作无特殊备注的**双引号均为了高亮**

- 新建一个新标签

```js
默认新的标签是搭载在最近的commit上
git tag "name"
```

- 查看某个标签信息（标签不是按时间顺序列出，而是按字母排序的）

```js
git show "tagname"
```

- 查看所有标签（标签不是按时间顺序列出，而是按字母排序的）

```js
git tag
```

- 创建带有说明的标签，用-a 指定标签名，-m 指定说明文字

```js
git tag -a v0.1 -m "说明..." 1234567
```

- 删除本地标签

```js
 git tag -d "v0.1"
```

- 推送一个本地标签到远程

```js
git push origin "tagname"
```

- 推送全部未推送过的本地标签到远程

```js
git push origin --tags
```

- 删除一个远程标签(注意：先删除本地的)

```js
  git push origin :refs/tags/<tagname>
```

- tag 默认是打在最新的 commit 上的，如果想给已经 commit 过的内容添加标签如下：

```js
  git reflog //找到历史版本的 commit id = 1234567
  git tag v1.0.0 1234567
```

- 获取远程 tag

```js
 git fetch origin tag <tagname>
```

- 推送全部未推送过的本地标签到远程

```js
git push origin --tags
```

- 推送全部未推送过的本地标签到远程

```js
git push origin --tags
```

#### 4、数据合并、查看

- 修改本地远程仓库地址：

```js
git remote add origin url   # 设置本地的远程仓库地址
git remote rm origin    # 移除本地远程仓库地址
```

- 从远程服务器获取内容:

```js
git pull orgin master 拉取远程仓库代码并合并
git fetch orgin master 拉取远程仓库代码不会合并，需要执行git merge origin/merge进行合并
```

- 远程代码强制合并本地代码：

```js
git pull origin master --allow-unrelated-histories
```

- 仓库地址

```js
git remote  -v       #查看本地的远程仓库地址
git remote rm origin  #移除本地远程仓库地址
git remote add origin  git@github.com:用户名/仓库名.git   #设置本地的远程仓库地址
```

- 查看文件的每行代码是谁写的(那个分支写的)，
  git blame files

#### 特殊处理

- 仓库上传忽略

```js
.gitignore 忽略文件 内容要忽略推送的.文件名 *.jpg node_modules/
```

### 参考博客

* [Git常用命令--了解这些就够了](https://www.jianshu.com/p/f92ed1ca8120)
