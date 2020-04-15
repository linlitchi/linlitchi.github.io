---
layout: post
title: 学习笔记 | 初探Git和Github
---

零基础萌新的Git和Github探索道路

#### 参考
* [MAC上Git安装与GitHub基本使用](https://www.jianshu.com/p/7edb6b838a2e)  
* [『Git』知道这些就够了](https://www.bilibili.com/video/BV1BE411g7SV?t=43)

## Git部份

1. 八百年前已经安装的git，听说终端输入git返回下面结果就算安装成功

```
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add       Add file contents to the index
   mv        Move or rename a file, a directory, or a symlink
   restore   Restore working tree files
   rm        Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect    Use binary search to find the commit that introduced a bug
   diff      Show changes between commits, commit and working tree, etc
   grep      Print lines matching a pattern
   log       Show commit logs
   show      Show various types of objects
   status    Show the working tree status

grow, mark and tweak your common history
   branch    List, create, or delete branches
   commit    Record changes to the repository
   merge     Join two or more development histories together
   rebase    Reapply commits on top of another base tip
   reset     Reset current HEAD to the specified state
   switch    Switch branches
   tag       Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch     Download objects and refs from another repository
   pull      Fetch from and integrate with another repository or a local branch
   push      Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
```

2. 设置用户名和邮箱

```
git config --global user.name "linlitchi"
git config --global user.email "511074688@qq.com"
```

3. 通过终端命令创建ssh key

```
ssh-keygen -t rsa -C "511074688@qq.com" 
```
查看公钥文件并复制里面的所有内容（听说邮箱可以不用复制）
```
open .ssh/id_rsa.pub 
```
如果执行后找不到这个文件，可能是因为文件夹隐藏了，先打开隐藏目录ssh
```
open ~/.ssh
```

4. 进入github账号的setting的SSH and GPG keys，点击右上角new SSH key，把上一步复制的内容粘贴进去，保存

5. 链接验证

```
ssh -T git@github.com 
```
返回这样的结果（小朋友你是否有很多问号？？？）
```
Hi linlitchi! You've successfully authenticated, but GitHub does not provide shell access.
```
不慌！经[查证](https://bbs.csdn.net/topics/392383668)，这个结果的意思是不能通过ssh协议登录github，但不影响本地使用ssh协议进行git操作并提交到github上。

6. cd到指定目录下，初始化仓库

```
git init
```
查看仓库状态：
```
git status
```
空荡荡的，如同我的余额：
```
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

7. 把我珍藏多年的hello world的html文件拷贝到初始化仓库的目录下，这个html文件和.git目录同级，出现红名玩家（抓起来抓起来）
 
```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	index.html

nothing added to commit but untracked files present (use "git add" to track)
```

8. 将文件加入暂存区

```
git add index.html
```
再次用status查看状态，它绿了它绿了它绿了
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   index.html
```

如果有八百个想变绿（？）的文件：

```
git add .
```

9. 提交变更，-m是message的意思，后面那句是变更相关描述

```
git commit -m "my first commit"
```
返回变更情况
```
[master (root-commit) e3065b0] my first commit
 1 file changed, 26 insertions(+)
 create mode 100644 index.html
```

10. add绿掉后悔了怎么办？用reset！

```
//把文件放到暂存区
git add .
//查看一下，确实变绿了
git status
//又不想变绿，reset一下吧
git reset new.png
//aoi~又红liao！
git status
```

## Github部份

1. 来到[github首页](https://github.com/)，new一个repository，简单填写了项目名称和项目描述，点击Create repository，复制SSH地址，clone到本地

```
git clone git@github.com:linlitchi/LearnGit.git
```

2. cd到clone的文件夹路径，把index.html放进去

```
//文件加入暂存区
git add .
//提交变更
git commit -m "第一次github作业"
//上传到github
git push
```

3. 回到github项目页面，发现已经index.html已经在项目中了，成功！
