# Inspection、Comparison and Patching 检查、比较和修补

## diff 比较

	$ git diff [<options>] [<mode>] [--] [<path>...]

`[--merge-base]`

- 选项为空 - 比较"工作区"和"暂存区"，即修改后未暂存内容。
- <commit> | <branch> - 比较"工作区"和指定"提交"或"分支"，未指定则为最新 commit。
- <commit>..<commit> - 比较两次"提交"或"分支"的差异。
- <commit>...<commit> - 比较第一个"提交"与给定多个父节点的差异集合。
- `--no-index [--] [<path> | <blob>] [<path> | <blob>]` - 对比俩个文件差异
- `--staged <commit>` - 比较"暂存区"和"版本库"差异
- `--cached <commit>` - 比较"暂存区"和"版本库"差异
- `--stat` - 仅仅比较统计信息

## rebase 基础合并

> branch_1 和 branch_2 并行开发而且各自产生了 commit 时。   
> 将 branch_1 合并到 branch_2 但不产生合并历史。（看起来是 branch_2 连贯的提交）。  
> 常用于合并来自远程仓库其他开发者的分支 commit。  

	$ git rebase <mode> [<options>]

**Mode**

- 没有选项
- `--root`
- `--continue`
- `--skip`
- `--abort`
- `--quit`
- `--edit-todo`
- `--show-current-patch`

**Options**

- `-i | --interactive` 
- `<options>` 
- `--exec <cmd>`
- `--onto <newbase> | --keep-base` 
- `<upstream> [<branch>]`
- `<branch>`

## revert 重做

**重新编辑单个或多个 commit 并重新提交**

	$ git revert [<options>...] (<commit> | <commit_1>..<commit_2>)​

- `[--[no-]edit]` 
- `[-n]` 
- `[-m parent-number]` 
- `[-s]`
- `[-S[<keyid>]]`

<commit> - 重做单个 commit

<commit_1>..<commit_n> - 重做 commit_1 到 commit_n 之间的所有提交

**重做发生冲突时**

	$ git revert <options>

- `--continue`
- `--skip`
- `--abort` - 冲突时退出，相当于没有合并。
- `--quit` - 保留

## shortlog

汇总 log 日志输出。

	$ git shortlog [<options>] [<revision-range>] [[--] <path>…​]

使用 log 指令实现汇总

	$ git log --pretty=short

## describe

显示离当前提交最近的标签。

	$ git describe [<options>]... (--dirty[=<mark>] | [<commit-ish>…​])

- `--all`
- `--tags`
- `--contains`
- `--abbrev=<n>`