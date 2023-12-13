# Github 版本控制系统

## 常用指令

将本地文件夹初始化为 github 仓库

    $ git init

关联远程仓库与本地仓库

    $ git remote add origin https://github.com/[ userName ]/[ repoName ].git

重命名分支

    $ git branch -M [ branchName ]

将内容保存到暂存区

    $ git add .

提交内容到本地仓库

    $ git commit -m "description"

从本地仓库推送到 GitHub 仓库

    $ git push -u origin [ branchName ]

从 GitHub 拉取到本地仓库

    $ git pull origin [ branchName ]

将指定目录提交到指定分支

    $ git subtree push --prefix=[ treeName ] origin [ branchName ]

-----------------------------------------------------------------------------------------
## Introduction 简介

**Git 对象**

Description: 使用 SHA1 算法将文件、目录、提交转换为对应的哈希码并保存到 Git 版本库。

- blob 对象
  + 代表单个文件块
  + 执行 `$ git add` 时创建
  + 指向该文件内容
- tree 对象
  + 代表单个文件目录
  + 执行 `$ git commit` 时创建
  + 指向该目录下的所有直接子文件 blob 对象
  + 指向该目录下的所有直接子目录 tree 对象
- commit 对象
  + 代表一次提交状态
  + 执行 `$ git commit` 时创建
  + 指向根目录的 tree 对象
  + 指向上一个提交状态的 commit 对象

**Git 区域**

- worktree 工作区 - 本地编辑的文本
- staged 暂存区 - 储存 `$ git add` 添加的 blog 对象
- repository 本地仓库 - 储存 `$ git commit` 提交的 tree、commit 对象。
- remote 远程仓库 - Github

**Git 文件**

- .gitignore - 定义忽略的，不上传的文件类型
- .git - `$ git init` 时创建，用于储存 Git 对象。
  + `./objects` - git 对象库
  + `./index` - 索引库
  + `./HEAD` - 保存 HEAD 指针的指向 `ref: refs/heads/master`

**Git 分支**

Description: 每个 commit 作为下一个 commit 的父相连组成的逻辑线称为分支。

- `master` - 默认指针
- `HEAD` - 当前指针，它总是指向当前所处的分支指针，即当前所处分支的最新提交。
- `HEAD~[n]` - 当前指针之前的第 n 次提交。
- 分支指针 - 总是指向当前分支的最新提交 commit
- 头分离 - HEAD 指针处于某个 commit 而非某个分支指针的状态
  + `$ git checkout cbd3348` - 当检出某个提交时
  + 可以在该状态开始修改，创建一个隐藏的分支。
  + 为这个隐藏分支命名，使它变为真实的分支。

-----------------------------------------------------------------------------------------
## [Basis Command 基本指令](https://keepenthusiasmlearning.github.io/note/utility-github/basis-command.html)

- config - 配置
- help - 帮助
- init - 初始化，创建或初始化已有文件夹作为版本库，添加 .git 文件。
- add - 添加，将指定文件转换为 blob 对象并添加到"暂存区"。
- commit - 提交，创建 tree 和 commit 对象，并将"暂存区"提交到"版本库"。
- reset - 重置，将 HEAD 指针重置到指定的状态。
- restore - 恢复，将工作区文件恢复到指定状态。
- log - 日志，打印 commit 提交记录。
- status - 状态，显示工作目录和暂存区的状态。
- rm - 删除
- mv - 移动

## [Remote Command 远程指令](https://keepenthusiasmlearning.github.io/note/utility-github/remote-command.html)

- remote - 远程
- clone - 克隆，将远程仓库克隆到本地。
- push - 推送，将本地仓库内容推送到远程仓库。
- fetch - 提取，将远程仓库更新提取到本地，以影子分支形式 `[repoName]/[branchName]`。
- pull - 拉取，将远程仓库更新提取到本地并合并到同名分支，相当于 `$ git fetch` 和 `$ git merge`。

## [Branch Command 分支指令](https://keepenthusiasmlearning.github.io/note/utility-github/branch-command.html)

- branch - 分支操作，列出，创建或删除分支。
- checkout - 检出，切换分支或恢复工作区文件。
- merge - 合并，合并多个开发历史。
- mergetool - 合并工具，运行合并冲突解决工具来解决合并冲突。
- stash - 暂时储藏状态到当前分支 WIP
- tag - 标签

## [Inspection、Comparison and Patching 检查、比较和修补](https://keepenthusiasmlearning.github.io/note/utility-github/inspection-comparison-patching.html)

- diff - 比较
- rebase - 基础合并，将指定分支合并到当前分支，但不产生合并记录。
- revert - 重做，重新编辑指定 commit 并重新提交。
- shortlog - 汇总 log 日志输出。
- describe - 显示离当前提交最近的标签。

## [Other Command 其他指令](https://keepenthusiasmlearning.github.io/note/utility-github/other-command.html)

- rev-parse - 打印完整哈希值。
- cat-file - 传入哈希值，打印信息。
- reflog - 打印指针记录。
- ls-files - 打印索引库。

## 公共参数说明

- `--` - 指定跟随内容为参数而非选项。
- `<pathspec>...` - 指定作用范围。
- `--pathspec-from-file=<file> [--pathspec-file-nul]` - 引用的 `<pathspec>`
- `-p|--patch` - 以交互方式执行命令。
- `-q | --quiet` - 安静，仅打印错误和警告消息。

