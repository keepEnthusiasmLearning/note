# branch 分支操作

	$ git branch [<mode>]

- `(-m | -M)` - 移动或重命名分支。 [<oldbranch>] <newbranch>
- `(-c | -C)` - 复制分支，连同它的 reflog 记录。 [<oldbranch>] <newbranch>
- `(-d | -D)` - 删除分支，它必须是完全合并的。 [-r] <branchname>...
- `--edit-description` - 打开编译器编写文本解释分支。 [<branchname>]
- `--set-upstream-to=<upstream> | -u <upstream>` - 设置 [<branchname>] 的上游分支。
- `--unset-upstream` - 取消 [<branchname>] 上游分支关联。
- git branch <branchname> - 创建分支
	- [--track[=(direct|inherit)] | --no-track] [-f]
	- [<start-point>]

## 分支信息展示

	$ git branch [<options>]...

- 没有选项 - 打印所有分支
- `--color[=<when>] | --no-color`
- `--show-current`
- `-v [--abbrev=<n> | --no-abbrev]` - 打印分支，包括"哈希值"和"注释信息"
- `--column[=<options>] | --no-column`
- `--sort=<key>`
- `--merged [<commit>]`
- `--no-merged [<commit>]`
- `--contains [<commit>]`
- `--no-contains [<commit>]`
- `--points-at <object>`
- `--format=<format>`
- `(-r | --remotes) | (-a | --all)`
- `--list`
- `<pattern>…​`

## checkout 检出

切换分支或恢复工作区文件

	$ git checkout [<mode>] [<options>...] [<branch>]

**Mode**

- 没有选项 - 检出到指定分支
- `--detach` - 分离头，指定 <commit> 检出到特定提交
- `[-b|-B|--orphan] <new-branch>` - 从头创建一个新分支，它不关联任何其他分支。指定 [<start-point>] 为它的起点
- `-p|--patch` 以交互方式执行命令
- <tree-ish> - 检出到一个目录。
	- [--] <pathspec>
	- --pathspec-from-file=<file> [--pathspec-file-nul]

**Options**

- `-q` 
- `-f` 
- `-m`
- `--ours`
- `--theirs`
- `--conflict=<style>`

## merge 合并

> 将 branchName 合并到当前分支，即 $ checkout 检出的分支。  
> "Fast-forward" 模式，快速合并。  
> 合并提交。
> (master|MERGING) - 合并冲突，分支处于合并中状态。
> - slove_1 - 修复冲突，再次使用 `$ git commit` 提交。
> - slove_2 - 放弃合并，使用 `git merge –abort` 指令回到合并前状态。

**Mode**

	$ git merge <mode> [branchName] -m "annotation"

- `--ff`
- `--no-ff` - 明确指定不使用 "Fast-forward" 而是创建合并提交进行合并。
- `--ff-only` - 只在满足 "Fast-forward" 条件下进行合并。
- `--continue`
- `--abort`
- `--quit`

**Options**

	$ git merge [<options>...]

- `-n`
- `--stat`
- `--no-commit` - 禁止自动创建提交，而是手动分支
- `--squash`
- `--[no-]edit` - 使用默认注释，跳过编辑。
- `--no-verify`
- `-s <strategy>`
- `-X <strategy-option>`
- `-S[<keyid>]`
- `--[no-]allow-unrelated-histories`
- `--[no-]rerere-autoupdate`
- `-m <msg>`
- `-F <file>`
- `--into-name <branch>`
- `<commit>...`

## mergetool 合并工具

运行合并冲突解决工具来解决合并冲突。

	$ git mergetool [--tool=<tool>] [-y | --[no-]prompt] [<file>…]

## stash 储藏

默认情况下储藏列表为分支上的 WIP，保存在 `refs/stash` 中，暂时储藏状态到当前分支 WIP。

	$ git stash [<mode>]

- 没有选项 - 等同于 `push`
- `push` - 暂时的储藏当前"工作区"和"暂存区"并恢复工作区到 HEAD 指针
	- [-p|--patch]` 
	- `[-k|--[no-]keep-index]`
	- `[-q|--quiet]`
	- `[-u|--include-untracked]` 
	- `[-a|--all]` 
	- `[-m|--message <message>]]`
    - `[--]`
	- `[<pathspec>…​]]`
- `list [<options>]` - 列出储藏的修改
- `show` - 检查 - 指定 [<stash>]
	-  [-u|--include-untracked|--only-untracked] 
	-  [<diff-options>] 
- `drop [-q|--quiet]` - 指定	 [<stash>]
- `( pop | apply )` - 恢复，指定 [<stash>] 
	- [--index]
	- [-q|--quiet] 
- `branch <branchname>` - 指定 [<stash>]
- `clear`
- `create [<message>]`
- `store  <commit>`
	- [-m|--message <message>] 
	- [-q|--quiet]