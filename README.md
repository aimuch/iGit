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
git add fileName  把文件从工作目录添加到暂存区
git commit -m'some information'  添加文件到版本历史库
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
## 探密.git目录

