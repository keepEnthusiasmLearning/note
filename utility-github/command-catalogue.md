# Github 常用命令

- [基础指令](/)
- [远程仓库](/)
- [分支操作](/)
- [检查、比较、修补](/)
- [其他指令](/)
- [公共参数说明](/)

## 基本指令

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

## 远程仓库

- remote - 远程
- clone - 克隆，将远程仓库克隆到本地。
- push - 推送，将本地仓库内容推送到远程仓库。
- fetch - 提取，将远程仓库更新提取到本地，以影子分支形式 `[repoName]/[branchName]`。
- pull - 拉取，将远程仓库更新提取到本地并合并到同名分支，相当于 `$ git fetch` 和 `$ git merge`。

## 分支操作

- branch - 分支操作，列出，创建或删除分支。
- checkout - 检出，切换分支或恢复工作区文件。
- merge - 合并，合并多个开发历史。
- mergetool - 合并工具，运行合并冲突解决工具来解决合并冲突。
- stash - 暂时储藏状态到当前分支 WIP
- tag - 标签

Inspection、Comparison and Patching 检查、比较和修补

- diff - 比较
- rebase - 基础合并，将指定分支合并到当前分支，但不产生合并记录。
- revert - 重做，重新编辑指定 commit 并重新提交。
- shortlog - 汇总 log 日志输出。
- describe - 显示离当前提交最近的标签。

## 其他指令

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
