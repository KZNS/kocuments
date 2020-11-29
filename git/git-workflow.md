# Git Workflow

本文包含使用git工作时的一些推荐工作流程与规范。

- [1. 分支管理](#1-分支管理)
- [2. commit message](#2-commit-message)
  - [2.1. Header](#21-header)
    - [2.1.1. type](#211-type)
    - [2.1.2. scope](#212-scope)
    - [2.1.3. subject](#213-subject)
  - [2.2. Body](#22-body)
  - [2.3. Footer](#23-footer)
    - [2.3.1. 不兼容变动](#231-不兼容变动)
    - [2.3.2. 关闭 Issue](#232-关闭-issue)
  - [2.4. Revert](#24-revert)

## 1. 分支管理

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

## 2. commit message

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

### 2.1. Header

#### 2.1.1. type

type用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

#### 2.1.2. scope

scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

#### 2.1.3. subject

subject是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）

### 2.2. Body

Body 部分是对本次 commit 的详细描述，可以分成多行。

有两个注意点。

1. 使用第一人称现在时，比如使用change而不是changed或changes。
2. 应该说明代码变动的动机，以及与以前行为的对比。

### 2.3. Footer

Footer 部分只用于两种情况。

#### 2.3.1. 不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

#### 2.3.2. 关闭 Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

```text
Closes #234
```

也可以一次关闭多个 issue 。

```text
Closes #123, #245, #992
```

### 2.4. Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

```text
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

Body部分的格式是固定的，必须写成`This reverts commit <hash>.`，其中的hash是被撤销 commit 的 SHA 标识符。
