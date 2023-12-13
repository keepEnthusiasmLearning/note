# 远程仓库

## remote 远程

	$ git remote [<mode>]

`--push` - 指定查询 `push urls` 而非 `fetch urls`

`-v | --verbose`

**Mode**

- 没有选项 - 打印远程仓库信息。
- `add <name> <URL>` - 指定一个远程仓库对应本地仓库
	- [-t <branch>] 
	- [-m <master>] 
	- [-f] 
	- [--[no-]tags] 
	- [--mirror=(fetch|push)] 
- rename - 指定 <old> <new>，重命名指定远程仓库
- remove - 指定 <name> 移除指定远程仓库
- set-head - 指定 <name> 和 (mode) 操作远程分支
	- -a
	- --auto
	- -d
	- --delete
	- <branch>
- set-branches - 指定 <name> <branch>… 更改远程仓库的分支，[--add] 选项添加分支而非更改
- get-url <name> - 检索远程仓库的 url，显示 `insteadOf` 和 `pushInsteadOf` 的配置
	- [--all] - 列出远程仓库所有 url 信息。
- set-url - 设置远程仓库的 url
	- 未指定则替换
	- `--add` - 添加 <newurl> 到仓库 <name> 而非设置
	- `--delete` - 删除 <URL> 在仓库 <name>
- show [-n] <name>…​ - 显示远程仓库信息
- prune [-n | --dry-run] <name>…​ - 删除过时的有关 <name> 信息
- update [-p | --prune] [(<group> | <remote>)…​] - 获取远程仓库更新

## clone 克隆

将远程仓库克隆到本地。

	$ git clone [<options>]...

- `--template=<template-directory>` - 模板
- `-l`
- `-s`
- `--no-hardlinks`
- `-q`
- `-n`
- `--bare`
- `--mirror`
- `-o <name>`
- `-b <name>`
- `-u <upload-pack>`
- `--reference <repository>`
- `--dissociate`
- `--separate-git-dir <git-dir>`
- `--depth <depth>`
- `--[no-]single-branch`
- `--no-tags`
- `--recurse-submodules[=<pathspec>]`
- `--[no-]shallow-submodules`
- `--[no-]remote-submodules`
- `--jobs <n>`
- `--sparse`
- `--[no-]reject-shallow`
- `--filter=<filter>`
- `-- <repository>` - 指定仓库
- <directory>

## push 推送

将本地内容推送到远程仓库。

	$ git push [<options>]

- 没有选项，直接将本地内容推送到远程仓库，根据对应的上游分支
- `--all | --mirror | --tags`
- `--follow-tags`
- `--atomic`
- `-n | --dry-run`
- `--receive-pack=<git-receive-pack>`
- `--repo=<repository>`
- `-f | --force`
- `-d | --delete`
- `--prune`
- `-v | --verbose`
- `-u | --set-upstream`
- `-o <string> | --push-option=<string>`
- `--[no-]signed|--signed=(true|false|if-asked)`
- `--force-with-lease[=<refname>[:<expect>]`
- `--force-if-includes]`
- `--no-verify`
- `<repository> [<refspec>…​]`

## fetch 提取

将远程仓库更新提取到本地，以影子分支形式 `[repoName]/[branchName]`。

	$ git fetch [<options>] <mode>

- [<repository> [<refspec>…​]]
- <group>
- --multiple [(<repository> | <group>)…​]
- --all

## pull 拉取

将远程仓库更新提取到本地并合并到同名分支，相当于 `$ git fetch` 和 `$ git merge`。

	$ git pull [<options>] [<repository> [<refspec>…​]]