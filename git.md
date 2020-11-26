# Git

- [1. 什么是Git](#1-什么是git)
  - [1.1. 什么是GitHub](#11-什么是github)
  - [1.2. 什么是GitLab](#12-什么是gitlab)
- [2. Git入门教程](#2-git入门教程)
- [3. Git安装](#3-git安装)
- [4. 初始化](#4-初始化)
- [5. 暂存区与工作区](#5-暂存区与工作区)
  - [5.1. 查看当前状态](#51-查看当前状态)
  - [5.2. 暂存区操作](#52-暂存区操作)
  - [5.3. 撤销修改](#53-撤销修改)
- [6. 分支](#6-分支)
  - [6.1. 提交到分支](#61-提交到分支)
  - [6.2. 新分支](#62-新分支)
  - [6.3. 删除远程分支](#63-删除远程分支)
- [7. 版本控制](#7-版本控制)
  - [7.1. 查看历史](#71-查看历史)
  - [7.2. 版本回退](#72-版本回退)
  - [7.3. 比较](#73-比较)
- [8. 使用建议](#8-使用建议)
  - [8.1. 分支管理](#81-分支管理)
  - [8.2. commit message](#82-commit-message)
    - [8.2.1. Header](#821-header)
      - [8.2.1.1. type](#8211-type)
      - [8.2.1.2. scope](#8212-scope)
      - [8.2.1.3. subject](#8213-subject)
    - [8.2.2. Body](#822-body)
    - [8.2.3. Footer](#823-footer)
      - [8.2.3.1. 不兼容变动](#8231-不兼容变动)
      - [8.2.3.2. 关闭 Issue](#8232-关闭-issue)
    - [8.2.4. Revert](#824-revert)

## 1. 什么是Git

Git 是一个先进、实用、开源的代码管理软件。  
通过一些简单的操作，你可以轻易的记录代码的每一次修改，随时回到过去的版本，
并且十分方便在和其他人一起修改代码的时候，对不同的修改进行合并。

你可以使用Git在本地管理自己的代码，也可以通过服务器向他人展示你的代码，或者共同编辑。  

Git在开源社区与工作中都有广泛的应用，非常值得学习使用。

### 1.1. 什么是GitHub

GitHub是一个代码托管平台，通过Git，你可以将代码上传的GitHub，从而分享代码或者共同编辑。

### 1.2. 什么是GitLab

GitLab是一个便于自行安装的代码托管平台，可以方便的搭建出一个类似GitHub的代码托管网站。  
GitLab适合内部网络使用。

## 2. Git入门教程

下面的博客讲解的十分不错，你可以通过它入门  
<https://www.liaoxuefeng.com/wiki/896043488029600>  

## 3. Git安装

Git的应用非常广泛，所以也有多种方式来使用它。  

- Git命令行工具
- GitGUI
- 编辑器的Git插件

## 4. 初始化

通过以下指令初始化一个代码仓库，Git所管理的代码应该放在一个代码仓库里。  

```shell
git init
```

## 5. 暂存区与工作区

### 5.1. 查看当前状态

```shell
git status
```

### 5.2. 暂存区操作

```shell
#添加到暂存区
git add <FileName>
git add -A
```

### 5.3. 撤销修改

```shell
#恢复到暂存区或
git checkout -- <FileName>

#撤销add操作，恢复到工作区中
git reset HEAD <FileName>
```

## 6. 分支

### 6.1. 提交到分支

```shell
#提交
git commit -m <Message>
git commit
```

### 6.2. 新分支

```shell
git checkout -b|-B <new_branch> [<start point>]
```

### 6.3. 删除远程分支

```shell
#删除远程分支
git push origin --delete <branch_name>
#刷新本地缓存的远程分支列表
git remote update origin --prune
```

## 7. 版本控制

### 7.1. 查看历史

```shell
#查看版本log
git log

#查看命令log
git reflog
```

### 7.2. 版本回退

```shell
#返回上一个版本 HEAD^
git reset --hard HEAD^
```

### 7.3. 比较

???

```shell
git diff
```

## 8. 使用建议

### 8.1. 分支管理

为了优化分支图、方便**随意commit**和干一半做别的功能  
使用一个新的分支来完成修改（一项功能的添加）：  

1. 为修改创建分治
2. 修改过程中可以任意commit
3. 修改完成后
    1. 使用`--no-ff` merge到主分支
    2. 写一个合适的，总结这次修改的message
    3. 删除修改分支  

如果是十分简单的一次修改，也可以直接一次commit提交到主分支上。  
这样的话分支图大概这个样子，主分支上只有merge  

```text
*    feat: 添加一个feature
|\
| *  commit 3
| |
| *  commit 2
| |
| *  commit 1
|/
*    the first commit
```

### 8.2. commit message

来自[阮一峰的网络日志](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

使用[AngularJS](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.uyo6cb12dt6w)标准  
即：

```text
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

#### 8.2.1. Header

##### 8.2.1.1. type

type用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

##### 8.2.1.2. scope

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

##### 8.2.1.3. subject

subject是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）

#### 8.2.2. Body

Body 部分是对本次 commit 的详细描述，可以分成多行。

有两个注意点。

1. 使用第一人称现在时，比如使用change而不是changed或changes。
2. 应该说明代码变动的动机，以及与以前行为的对比。

#### 8.2.3. Footer

Footer 部分只用于两种情况。

##### 8.2.3.1. 不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

##### 8.2.3.2. 关闭 Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

```text
Closes #234
```

也可以一次关闭多个 issue 。

```text
Closes #123, #245, #992
```

#### 8.2.4. Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

```text
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

Body部分的格式是固定的，必须写成`This reverts commit <hash>.`，其中的hash是被撤销 commit 的 SHA 标识符。
