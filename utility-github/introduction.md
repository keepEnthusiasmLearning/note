# Introduction 简介

## Git 对象

Description: 使用 SHA1 算法将文件、目录、提交转换为对应的哈希码并保存到 Git 版本库。

**blob**

- 代表单个文件块
- 执行 `$ git add` 时创建
- 指向该文件内容

**tree**

- 代表单个文件目录
- 执行 `$ git commit` 时创建
- 指向该目录下的所有直接子文件 blob 对象
- 指向该目录下的所有直接子目录 tree 对象

**commit**

- 代表一次提交状态
- 执行 `$ git commit` 时创建
- 指向根目录的 tree 对象
- 指向上一个提交状态的 commit 对象

## Git 区域

- worktree 工作区 - 本地编辑的文本
- staged 暂存区 - 储存 `$ git add` 添加的 blog 对象
- repository 本地仓库 - 储存 `$ git commit` 提交的 tree、commit 对象。
- remote 远程仓库 - Github

## Git 文件

- .gitignore - 定义忽略的，不上传的文件类型
- .git - `$ git init` 时创建，用于储存 Git 对象。
  + `./objects` - git 对象库
  + `./index` - 索引库
  + `./HEAD` - 保存 HEAD 指针的指向 `ref: refs/heads/master`

## Git 分支

Description: 每个 commit 作为下一个 commit 的父相连组成的逻辑线称为分支。

- `master` - 默认指针
- `HEAD` - 当前指针，它总是指向当前所处的分支指针，即当前所处分支的最新提交。
- `HEAD~[n]` - 当前指针之前的第 n 次提交。
- 分支指针 - 总是指向当前分支的最新提交 commit
- 头分离 - HEAD 指针处于某个 commit 而非某个分支指针的状态
  + `$ git checkout cbd3348` - 当检出某个提交时
  + 可以在该状态开始修改，创建一个隐藏的分支。
  + 为这个隐藏分支命名，使它变为真实的分支。
