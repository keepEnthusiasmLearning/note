# 其他命令

## rev-parse 获取参数信息

	$ git rev-parse [<mode>] <args>…​

- `--parseopt`
	- `--keep-dashdash`
	- `--stop-at-non-option`
	- `--stuck-long`
- Filtering 过滤
	- `--revs-only - 不输出标记和参数`
	- `--no-revs - 不输出`
	- `--flags`
	- `--no-flags`
- Output
	- `--default <arg>`
	- `--prefix <arg>`
	- `--verify
	-q | --quiet`
	- `--sq`
	- `--not`
	- `--abbrev-ref[=(strict|loose)]`
	- `--symbolic`
	- `--symbolic-full-name`
- Objects
- Files
- Other 

## cat-file 打印对象信息

**模式**

	$ git cat-file <mode> [--path=<path>] <object>

`--path=<path>` - 分别指出对象名和路径时使用。

`<object>` - 要显示信息的对象名称

**Mode**

- `-t [--allow-unknown-type]` - 返回这个对象的类型
- `-s [--allow-unknown-type]`
- `-e` 
- `-p` - 返回这个对象的相关内容：指向、作者
- `<type>`
- `--textconv` 
- `--filters`

**选项**

	$ git cat-file <mode> [<options>]...

**Mode**

- `--batch[=<format>]`
- `--batch-check[=<format>]`

**Options**

- `--textconv | --filters`
- `--follow-symlinks`

## reflog 引用日志

	$ git reflog <mode> [<options>]

- 没有选项 - 等同于 show
- `show [<log-options>] [<ref>]` - 显示命令行中提供的引用的日志
- `expire <options>` - 过时，修剪较旧的 reflog 条目
	- `--expire=<time>` 
	- `--expire-unreachable=<time>`
	- `--rewrite` 
	- `--updateref` 
	- `--stale-fix`
	- `--dry-run | -n` 
	- `--verbose` 
	- `--all [--single-worktree] | <refs>...`
- `delete <options> <ref>@\{<specifier>\}...` - 从 reflog 中删除单个条目
	- `--rewrite` 
	- `--updateref`
	- `--dry-run | -n` 
	- `--verbose` 
- `exists <ref>` - 检查 ref 是否具有引用日志

## ls-files 显示有关"索引区"和"工作树"信息。

	$ git ls-files <options>...

`[-s|--stage]` - 打印索引区

