# Git

- [什么是Git](#什么是git)
  - [什么是GitHub](#什么是github)
  - [什么是GitLab](#什么是gitlab)
- [Git入门教程](#git入门教程)
  - [Git安装](#git安装)
  - [Git命令行的使用](#git命令行的使用)
- [初始化](#初始化)
- [暂存区与工作区](#暂存区与工作区)
  - [查看当前状态](#查看当前状态)
  - [暂存区操作](#暂存区操作)
  - [分支操作](#分支操作)
  - [撤销修改](#撤销修改)
- [版本控制](#版本控制)
  - [版本回退](#版本回退)
  - [区别](#区别)
- [分支](#分支)
- [使用建议](#使用建议)
  - [分支管理](#分支管理)
  - [commit message](#commit-message)
    - [Header](#header)
      - [type](#type)
      - [scope](#scope)
      - [subject](#subject)
    - [Body](#body)
    - [Footer](#footer)
      - [不兼容变动](#不兼容变动)
      - [关闭 Issue](#关闭-issue)
    - [Revert](#revert)

## 什么是Git

Git 是一个先进、实用、开源的代码管理软件。  
通过一些简单的操作，你可以轻易的记录代码的每一次修改，随时回到过去的版本，
并且十分方便在和其他人一起修改代码的时候，对不同的修改进行合并。

你可以使用Git在本地管理自己的代码，也可以通过服务器向他人展示你的代码，或者共同编辑。  

Git在开源社区与工作中都有广泛的应用，非常值得学习使用。

### 什么是GitHub

GitHub是一个代码托管平台，通过Git，你可以将代码上传的GitHub，从而分享代码或者共同编辑。

### 什么是GitLab

GitLab是一个便于自行安装的代码托管平台，可以方便的搭建出一个类似GitHub的代码托管网站。  
GitLab适合内部网络使用。

## Git入门教程

下面的博客讲解的十分不错，你可以通过它入门  
<https://www.liaoxuefeng.com/wiki/896043488029600>  

下文提供了一个简易教程，同时在入门教程之后记录了一些进阶指令

### Git安装

Git的应用非常广泛，所以也有多种方式来使用它。  

- Git命令行工具
- GitGUI
- 编辑器的Git插件

### Git命令行的使用

## 初始化

通过以下指令初始化一个代码仓库，Git所管理的代码应该放在一个代码仓库里。  

```shell
git init
```

## 暂存区与工作区

### 查看当前状态

```shell
git status
```

### 暂存区操作

```shell
git add <FileName>
git add -A

git rm <FileName>
```

### 分支操作

```shell
#提交
git commit -m <Message>
```

### 撤销修改

```shell
#恢复到暂存区或
git checkout -- <FileName>

#撤销add操作，恢复到工作区中
git reset HEAD <FileName>
```

## 版本控制

```shell
#查看版本log
git log

#查看命令log
git reflog
```

### 版本回退

```shell
#返回上一个版本 HEAD^
git reset --hard HEAD^

```

### 区别

???

```shell
git diff
```

## 分支

## 使用建议

### 分支管理

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

### commit message

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

#### Header

##### type

type用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

##### scope

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

##### subject

subject是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）

#### Body

Body 部分是对本次 commit 的详细描述，可以分成多行。

有两个注意点。

1. 使用第一人称现在时，比如使用change而不是changed或changes。
2. 应该说明代码变动的动机，以及与以前行为的对比。

#### Footer

Footer 部分只用于两种情况。

##### 不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

##### 关闭 Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

```text
Closes #234
```

也可以一次关闭多个 issue 。

```text
Closes #123, #245, #992
```

#### Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

```text
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

Body部分的格式是固定的，必须写成`This reverts commit <hash>.`，其中的hash是被撤销 commit 的 SHA 标识符。
