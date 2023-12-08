# Github 版本控制系统

## 理论知识

### Git 对象

**哈希码**

使用 SHA1 算法将文件、目录、提交转换为对应的哈希码, 以 Git 对象形式保存到版本库 

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

### Git 区域

| worktree   | 工作区, 本地编辑的文本。
| staged   | 暂存区, 储存文件 blob 对象。`$ git add`
| repository | 版本库、本地仓库, 储存目录、提交 tree、commit 对象。`$ git commit`
| remote   | 远程仓库, 分为公有和私有仓库

- .gitignore - 忽略, 指定不上传的文件类型
- .git - 初始化时创建, 储存 Git 对象。`$ git init`
  + `./objects` - 对象库：保存 git 对象
  + `./index` - 索引库
  + `./HEAD` - 保存 HEAD 指针的指向 ref: refs/heads/master

### 分支

每个 commit 作为下一个 commit 的父相连组成的逻辑线称为分支。

- `master` - 默认指针，创建 repo 时自动创建。
- `HEAD` - 当前指针，它总是指向当前所处的分支指针，即当前所处分支的最新提交。
- `main` - gitHub 远程仓库的默认指针。

**分支指针**

总是指向当前分支的最新提交 commit。

- develop - 开发分支
- feature - 功能分支，根据功能需求创建。开发完成后合并到 develop
- release - bug 修复与测试分支
- hotfix - 紧急修复 master 分支 bug

**头分离**

HEAD 指针处于某个 commit 而非某个分支指针的状态

- `$ git checkout cbd3348` - 当检出某个提交时
- 可以在该状态开始修改，创建一个隐藏的分支。
- 为这个隐藏分支命名，使它变为真实的分支。

**`HEAD~[n]`**

表示相对于 HEAD 之前的第 n 个提交

-----------------------------------------------------------------------------------------
## 基本操作

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