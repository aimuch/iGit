# i Play Git
*这是极客时间苏玲老师的《玩转Git三剑客》笔记*

## 添加配置
```bash
git config [--local | --global | --system] user.name 'Your name'
git config [--local | --global | --system] user.email 'Your email'
```

## 查看配置
```bash
git config --list [--local | --global | --system]
```
### 区别
```bash
local：区域为本仓库
global: 当前用户的所有仓库
system: 本系统的所有用户
```
## `git add .` 和 `git add -u`区别

```bash
git add . ：将工作空间新增和被修改的文件添加的暂存区
git add -u :将工作空间被修改和被删除的文件添加到暂存区(不包含没有纳入Git管理的新增文件)
```    

## 创建仓库
```bash
git init [project folder name]  初始化 git 仓库
git add [fileName]  把文件从工作目录添加到暂存区
git commit -m'some information'  用于提交暂存区的文件
git commit -am'Some information' 用于提交跟踪过的文件
git log  查看历史
git status  查看状态
```

**额外**    
git add -u 可以添加所有已经被 git 控制的文件到暂存区
以前删除文件夹只会用 「-rf」，今天学到了 「-r」，并得知它们两个区别：「-r」 有时候会提示是否确认删除。    

## 给文件重命名的简便方法
```bash
git  mv  [old file name]  [new file name]
git commit -m 'some information'
```

## 通过`git log`查看版本演变历史
```bash
git log --all 查看所有分支的历史
git log --all --graph 查看图形化的 log 地址
git log --oneline 查看单行的简洁历史。
git log --oneline -n4 查看最近的4条简洁历史。
git log --oneline --all -n4 --graph 查看所有分支最近4条单行的图形化历史。
git help --web log 跳转到git log 的帮助文档网页
```

```bash
git branch -v 查看本地有多少分支
```

## 通过图形界面工具来查看版本历史
```bash
gitk
```

## 探密`.git`目录
查看`.git`文件夹下的内容：    
```bash
ls .git/ -al
```
如下:   
```shell
drwxr-xr-x 1 Andy 197609   0 12月 17 22:38 ./
drwxr-xr-x 1 Andy 197609   0 12月 17 21:50 ../
-rw-r--r-- 1 Andy 197609   7 12月 17 22:38 COMMIT_EDITMSG
-rw-r--r-- 1 Andy 197609 301 12月 12 22:55 config
-rw-r--r-- 1 Andy 197609  73 12月 12 22:55 description
-rw-r--r-- 1 Andy 197609  96 12月 19 00:00 FETCH_HEAD
-rw-r--r-- 1 Andy 197609  23 12月 12 22:55 HEAD
drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 hooks/
-rw-r--r-- 1 Andy 197609 249 12月 17 22:38 index
drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 info/
drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 logs/
drwxr-xr-x 1 Andy 197609   0 12月 17 22:38 objects/
-rw-r--r-- 1 Andy 197609 114 12月 12 22:55 packed-refs
drwxr-xr-x 1 Andy 197609   0 12月 12 22:55 refs/
```

```bash
cat命令主要用来查看文件内容，创建文件，文件合并，追加文件内容等功能。
cat HEAD 查看HEAD文件的内容
git cat-file 命令 显示版本库对象的内容、类型及大小信息。
git cat-file -t b44dd71d62a5a8ed3 显示版本库对象的类型
git cat-file -s b44dd71d62a5a8ed3 显示版本库对象的大小
git cat-file -p b44dd71d62a5a8ed3 显示版本库对象的内容
```

`.git`里几个常用的如下：    
```bash
HEAD：指向当前的工作路径
config：存放本地仓库（local）相关的配置信息。
refs/heads: 存放分支
refs/heads/master/: 指向master分支最后一次commit
refs/tags: 存放tag，又叫里程牌 （当这次commit是具有里程碑意义的 比如项目1.0的时候 就可以打tag）
objects：核心文件，存储文件
```
.git/objects/ 存放所有的 git 对象，对象哈希值前 2 位作为文件夹名称，后 38 位作为对象文件名, 可通过 git cat-file -p 命令，拼接文件夹名称+文件名查看。    

## `commit`、`tree`和`blob`三个对象之间的关系
![tree](./images/img1.jpg)     

```bash
commit: 提交时的镜像
tree: 文件夹
blob: 文件
```

**【同学问题】** 每次commit，git 都会将当前项目的所有文件夹及文件快照保存到objects目录，如果项目文件比较大，不断迭代，commit无数次后，objects目录中文件大小是不是会变得无限大？    
**【老师解答】** Git对于内容相同的文件只会存一个blob，不同的commit的区别是commit、tree和有差异的blob，多数未变更的文件对应的blob都是相同的，这么设计对于版本管理系统来说可以省很多存储空间。其次，Git还有增量存储的机制，我估计是对于差异很小的blob设计的吧。    


## `分离头指针`情况下的注意事项

detached HEAD   

## 进一步理解`HEAD`和`branch`
```bash
git checkout -b new_branch [具体分支 或 commit] 创建新分支并切换到新分支
git diff HEAD HEAD~1 比较最近两次提交
git diff HEAD HEAD~2 比较最近和倒数第三次提交
git diff HEAD HEAD^  比较最近两次提交
git diff HEAD HEAD^^ 比较最近和倒数第三次提交
```   

## 怎么删除不需要的分支？
查看分支：   
```bash
git branch -av
```
删除分支命令：    
```bash
git branch -d [branch name]  删除
git branch -D [branch name]  强制删除
```

## 怎么修改最新commit的message？
```bash
git commit --amend  对最近一次的commit信息进行修改
```

## 怎么修改老旧commit的message？
```bash
git rebase -i [要更改的commit的上一级commit]
```
接下来就是一个交互过程...    
这期间会产生一个detached HEAD，然后将改好的commit指向该detached HEAD，如下图所示：    
![rebase](./images/img2.jpg)    

**git rebase工作的过程中，就是用了分离头指针。rebase意味着基于新base的commit来变更部分commits。它处理的时候，把HEAD指向base的commit，此时如果该commit没有对应branch，就处于分离头指针的状态，然后重新一个一个生成新的commit，当rebase创建完最后一个commit后，结束分离头状态，Git让变完基的分支名指向HEAD。**    

## 怎样把连续的多个commit整理成1个？

