# Git Command

本文包含关于git命令的一些内容。

- [1. Git入门](#1-git入门)
  - [1.1. 什么是Git](#11-什么是git)
    - [1.1.1. 什么是GitHub](#111-什么是github)
    - [1.1.2. 什么是GitLab](#112-什么是gitlab)
  - [1.2. Git安装](#12-git安装)
- [2. 初始化](#2-初始化)
- [3. 暂存区与工作区](#3-暂存区与工作区)
  - [3.1. 查看当前状态](#31-查看当前状态)
  - [3.2. 暂存区操作](#32-暂存区操作)
  - [3.3. 撤销修改](#33-撤销修改)
- [4. 分支](#4-分支)
  - [4.1. 提交到分支](#41-提交到分支)
  - [4.2. 新分支](#42-新分支)
  - [4.3. 删除远程分支](#43-删除远程分支)
- [5. 版本控制](#5-版本控制)
  - [5.1. 查看历史](#51-查看历史)
  - [5.2. 版本回退](#52-版本回退)
  - [5.3. 比较](#53-比较)
- [6. 危险操作](#6-危险操作)
  - [6.1. 修改历史 commits 中的用户名和邮箱](#61-修改历史-commits-中的用户名和邮箱)
  - [6.2. 强制上传到远端并覆盖](#62-强制上传到远端并覆盖)

## 1. Git入门

下面的博客讲解的十分不错，你可以通过它入门  
<https://www.liaoxuefeng.com/wiki/896043488029600>  

### 1.1. 什么是Git

Git 是一个先进、实用、开源的代码管理软件。  
通过一些简单的操作，你可以轻易的记录代码的每一次修改，随时回到过去的版本，
并且十分方便在和其他人一起修改代码的时候，对不同的修改进行合并。

你可以使用Git在本地管理自己的代码，也可以通过服务器向他人展示你的代码，或者共同编辑。  

Git在开源社区与工作中都有广泛的应用，非常值得学习使用。

#### 1.1.1. 什么是GitHub

GitHub是一个代码托管平台，通过Git，你可以将代码上传的GitHub，从而分享代码或者共同编辑。

#### 1.1.2. 什么是GitLab

GitLab是一个便于自行安装的代码托管平台，可以方便的搭建出一个类似GitHub的代码托管网站。  
GitLab适合内部网络使用。

### 1.2. Git安装

Git的应用非常广泛，所以也有多种方式来使用它。  

- Git命令行工具
- GitGUI
- 编辑器的Git插件

## 2. 初始化

通过以下指令初始化一个代码仓库，Git所管理的代码应该放在一个代码仓库里。  

```shell
git init
```

## 3. 暂存区与工作区

### 3.1. 查看当前状态

```shell
git status
```

### 3.2. 暂存区操作

```shell
#添加到暂存区
git add <FileName>
git add -A
```

### 3.3. 撤销修改

```shell
#恢复到暂存区或
git checkout -- <FileName>

#撤销add操作，恢复到工作区中
git reset HEAD <FileName>
```

## 4. 分支

### 4.1. 提交到分支

```shell
#提交
git commit -m <Message>
git commit
```

### 4.2. 新分支

```shell
git checkout -b|-B <new_branch> [<start point>]
```

### 4.3. 删除远程分支

```shell
#删除远程分支
git push origin --delete <branch_name>
#刷新本地缓存的远程分支列表
git remote update origin --prune
```

## 5. 版本控制

### 5.1. 查看历史

```shell
#查看版本log
git log

#查看命令log
git reflog
```

### 5.2. 版本回退

```shell
#返回上一个版本 HEAD^
git reset --hard HEAD^
```

### 5.3. 比较

???

```shell
git diff
```

## 6. 危险操作

### 6.1. 修改历史 commits 中的用户名和邮箱

```sh
git filter-branch -f --env-filter '
OLD_EMAIL="原来的邮箱"
CORRECT_NAME="现在的名字"
CORRECT_EMAIL="现在的邮箱"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

### 6.2. 强制上传到远端并覆盖

```sh
git push --force
```
