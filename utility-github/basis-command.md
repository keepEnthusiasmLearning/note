# 基础指令

## init 初始化

创建一个空的 Git 存储库或重新初始化现有的 Git 存储库，添加 `.git` 文件。它包含 `-objects`、`refs/heads`、`--initial-branch`、`refs/tags`目录。

	$ git init [<options>]...

- `-q | --quiet` - 仅打印错误和警告消息。
- `--bare` -  创建空的储存库。
- `--template=<template-directory>` - 指定使用一个模板。
- `--separate-git-dir <git-dir>` - 创建一个包含实际存储库路径的文本文件。
- `--object-format=<format>` - 指定储存库的给定对象格式，即"哈希算法"格式。
- `-b <branch-name> | --initial-branch=<branch-name>` - 初始化分支
- `--shared[=<permissions>]` - 指定在多个用户之间共享 Git 存储库。
	- false
	- true
	- umask
	- group
	- all
	- world
	- everybody
	- <perm>
- `<directory>` - 指定目录，未指定则为当前目录。

## add 添加

将指定文件转换为 blob 对象并添加到"索引库"。

	$ git add [<options>]...		

- `--verbose | -v` - 详情
- `--dry-run | -n` - 显示这些文件是否存在或将被忽略，而不添加它们。
- `--force | -f` - 
- `--interactive | -i` - 交互，以交互方式将工作树中已修改的内容添加到索引中。
- `--patch | -p` - 补丁，以交互方式在索引和工作树之间选择大块补丁，并将其添加到索引中。
- `--edit | -e` - 编辑器，在编辑器中打开差异与索引。
- Mode
	- [-A | --all | --no-ignore-removal] - 添加、修改和删除"索引库"以匹配"工作区"
	- [ --no-all | --ignore-removal] - 添加和修改"索引库"以匹配"工作区"，但不删除"工作区"已删除文件索引。
	- [--update | -u] - 删除或修改"索引库"使其匹配"工作区"，但不添加文件。
- `--sparse`
- `--intent-to-add | -N` 
- `--refresh`
- `--ignore-errors` 
- `--ignore-missing` 
- `--renormalize`
- `--chmod=(+|-)x` 

## commit 提交

创建一个新的提交对象 commit ，它包含当前索引内容和描述，更新 HEAD 指针指向它。（除非没有分支与工作树相关联，HEAD 处于分离状态。

	$ git commit [<options>]... [--am] [--] [<pathspec>]...

`--am` - 同时执行 `$ git add`

- `-a | --interactive | --patch`
- `-s`
- `-v`
- `-u<mode>`
- `--amend`
- `--dry-run`
- `(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>)`
- `-F <file> | -m <msg>`
- `--reset-author`
- `--allow-empty`
- `--allow-empty-message`
- `--no-verify`
- `-e`
- `--author=<author>`
- `--date=<date>`
- `--cleanup=<mode>`
- `--[no-]status`
- `-i | -o`
- `(--trailer <token>[(=|:)<value>])…​`
- `-S[<keyid>]` - GPG 签名

## reset 复位

**将条目从 `<tree-ish>` 复制到索引**

	$ git reset [-q] [<tree-ish>] [--] <pathspec>…​

**将 HEAD 指针重置到指定 commit**

	$ git reset [<mode>] [-q] [<commit>]

`<commit>` - 回退到这个提交，可以是哈希值、指针、commit。

`-q` - 只报告错误

**Mode**

- `--soft` 	- 工作区：不变、暂存区：不变、提交状态：回退
- `--mixed [-N]` - 工作区：不变、暂存区：回退、提交状态：回退
- `--hard` 	- 工作区：回退、暂存区：回退、提交状态：回退
- `--merge`
- `--keep`

在只想回退工作区的情况下，使用 $ git checkout 指令

## restore 恢复

使用"还原源"内容恢复"工作树"中的"指定路径"。  
如果"指定路径"不存在于"还原源"，则自动从跟踪中删除。

	$ git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…​

`--staged | -S` - 指定还原"暂存区"

`--worktree | -W` - 指定还原"工作区"

`-s <tree> | --source=<tree>` - 指定"还原源"，未指定则从"暂存区"还原。

**Options**

- `-q | --quiet`
- `--progress | --no-progress`
- `--ours | --theirs`
- `-m | --merge`
- `--conflict=<style>`
- `--ignore-unmerged`
- `--ignore-skip-worktree-bits`
- `--recurse-submodules | --no-recurse-submodules`
- `--overlay | --no-overlay`

## log 日志

打印提交记录

	$ git log [<options>] [<revision-range>] [--] [<pathspec>…​]

`<revision-range>` - 指定显示范围，未指定则显示到当前 HEAD 指针的所有记录。

`-- <path>…​` - 指定一个路径，只显示与 path 相关的历史提交。

**Options**

- `--oneline` - 以简易模式查看提交信息。
- `–-graph` - 以文本图形表示提交历史。
- `--merges` - 只打印合并提交。
- `--no-merges` - 跳过合并。

## status 状态

显示"暂存区"和"HEAD commit"之间的差异。

	$ git status [<options>​]... [--] [<pathspec>…​]

## rm 删除

从"暂存区"和被跟踪的"工作区"中删除文件，不会真正删除文件。

	$ git rm [<options>]... [--] [<pathspec>…​]

`-- <pathspec>…`​ - 指定要删除文件

**Options**

- `-f | --force` 
- `-n` 
- `-r`
- `--cached`
- `--ignore-unmatch`
- `--quiet`

## mv 移动

移动或重命名文件、目录或符号链接

	$ git mv <options>... <args>...

`<args>` - 用于重命名，`folder_1 folder_2`

**Options**

- `-f | --force`
- `-k`
- `-n | --dry-run`
- `-v | --verbose`

## config 配置

配置项操作，包括添加、删除、更改 <section>.<key> <value>

	git config [<options>]... [<mode>]

**Mode**

- 指定 <name> <value> 替换匹配的项。[--replace-all] 选项替换匹配的所有值。
- `--add` - 指定 <name> <value> 添加新项。 
- 获取 
	- `--get` - 指定 <name> <value-pattern>，获取匹配的最后一个值。
	- `--get-all` - 指定 <name> <value-pattern>，获取匹配的所有值。
	- `--get-regexp` - 指定 <name-regex> <value-pattern>，获取匹配正则表达式的项。[--name-only] 选项只输出匹配的键名。
	- `--get-urlmatch` - 指定 <name> <URL>，获取匹配的值。
- `--unset` - 指定 <name> <value-pattern>，删除最后一个匹配键。
- `--unset-all` - 指定 <name> <value-pattern>，删除所有匹配键。
- `--rename-section` - 指定 <old-name> <new-name>，更改 section 名字。
- `--remove-section` - 指定 <name> 删除指定 section。
- `--get-color` - 指定 <name> [<default>]
- `--get-colorbool` - 指定 <name> [<stdout-is-tty>]
- `-e | --edit` - 打开编译器修改配置表
- `-l | --list` - 列出配置表中设置的所有变量和值

**Options**

- [<file-option>] - 指定读/写配置项的位置(级别)。
	- `--system`
	- `--global`
	- `--local`
	- `--worktree`
	- `--file <filename>`
- [--type=<type>] - 指定输入值和输出值
- [--fixed-value] - 指定确定的值而非正则表达式
- [--show-origin] - 指定增加输出类型：file, standard input, blob, command line, config file path, ref, or blob id if applicable
- [--show-scope] - 指定增加输出范围：local, global, system, command
- [-z|--null] - 使用换行符或空格分隔输出项

## help 帮助

打印帮助 `help` 和 `--help` 是相等的。

	$ git help [<options>] [<format>] [<mode>]

**Mode**
	
- 没有选项 - 所有帮助
- <command> - 打印一个命令的帮助页
- <guide> - 打印一个指定项的帮助页

**Options**

- 没有选项 - 打印 git 命令概要和常用命令列表
- `-a|--all [--[no-]verbose]` - 打印所有可用命令
- `-g|--guides` - 打印常用 git 指南
- `-c|--config`

**Format**

`-i|--info` - 以信息格式显示
`-m|--man` - 以 man 格式显示
`-w|--web` - 以 Web 格式显示
