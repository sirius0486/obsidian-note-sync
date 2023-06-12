## 多人协同相关

### 拉取代码遇到冲突怎么办

```sh
# 1. merge
git pull   # 等价于 git fetch + git merge 


# 2. rebase
git pull --rebase

```

### 正在开发遇到其他分支紧急 bug 需要修复, 如何处理?
```sh
# 功能未完成 commit 不了, 切换不了分支, 可以使用 stash 临时保存内容
git stash

# 修完 bug 后再切回 开发分支 弹出原来的代码
git stash pop

# 可以 stash 多次, 对应 pop 多次, 和 堆栈的结构是一样的, 先入后出

# 如果文件是新建的, 也就是 untracked 的状态, 是不能直接使用 git stash 的
git stash save -u

# 就是新建了文件，但是没有用 `git add .` 追踪文件，那么 `git stash` 是无法存储的

```

### 其他分支有你需要的代码, 通过 cherry-pick 加入到你的分支
```sh

# 我们可以把其他分支的 commit 移到当前分支
git cherry-pick <commit_Ids>

```


## 本地 git 操作

### git init 做了什么?

从根本上来讲 Git 是一套内容寻址 (content-addressable) 文件系统，在此之上提供了一个 VCS 用户界面。

当你在一个新目录或已有目录内执行 git init 时，Git 会创建一个 .git 目录， 几乎所有 Git 存储和操作的内容都位于该目录下。如果你要备份或复制一个库， 基本上将这一目录拷贝至其他地方就可以了。

其中有四个重要的文件或目录：HEAD 及 index 文件，objects 及 refs 目录。 objects 目录存储所有数据内容，refs 目录存储指向数据 (分支) 的提交对象的指针，HEAD 文件指向当前分支，index 文件保存了暂存区域信息。


### 如何恢复到 git add 之前?

```sh
git reset <file>

# file此时变成 unstage 状态
```


### 如何更改还未提交的 commit ? 

```sh
# 方法一
git commit --amend

# 方法二
git rebase -i HEAD~{number}

# number 表示 你要编辑 commit 的个数
```

### 恢复到 commit 之前, add 之后的状态?

```sh
# 回到 git add 后，commit 前
git reset --soft HEAD~1

# 回到 git add 之前
git reset HEAD~1

# 这种方式比较危险。会抛弃所有的更改
git reset --hard HEAD~1
```

### 误删了一个 commit, 如何 通过 git reflog 恢复?
```sh
git reflog
# reflog能看到所有 commit 记录, 包括被删除的, 找到要恢复位置的 commit sha

# -b 不带，默认当前 branch
git checkout -b newBranch <sha>
```

### branch 操作
```sh
# 1. 查看 本地 所有branch
git branch

# 2. 查看 本地和远端 所有branch
git branch -a

# 3. 创建新的 branch
git checkout -b <newBranch>

# 4. 重命名 branch
git branch -m <oldBranch> <newBranch>

# 5. 删除本地或远程分支

# 删除远程分支 origin 
git push -d origin <branch_name>

# 删除本地分支 local
git branch -d <branch_name>

```

### 将多个 commit 合并成一个 commit
```sh
#查看 commit 历史
git log

>>> output
* b1b8189 - (HEAD -> master) Commit-3
* 5756e15 - Commit-2
* e7ba81d - Commit-1
* 5d39ff2 - Commit-0

# 假如合并前三个 commit 为一个, 那么我们可以
git rebase -i 5d39ff2
#or
git rebase -i HEAD~3


# 进入到 rebase 交互页面

pick e7ba81d Commit-1
pick 5756e15 Commit-2
pick b1b8189 Commit-3

# 改成如下

pick e7ba81d Commit-1
s 5756e15 Commit-2
s b1b8189 Commit-3

# 保存退出后, 进入新的界面, 填写此次合并后的 commit message

```



## 版本回滚相关

### git reset 和 git revert 的区别
> [!note] > 撤销(revert)被设计为撤销公开的提交(比如已经push)的安全方式，git reset被设计为重设本地更改

因为两个命令的目的不同，它们的实现也不一样：重设完全地移除了一堆更改，而撤销保留了原来的更改，用一个新的提交来实现撤销

**两者主要区别如下：**

-   git revert是用一次新的commit来回滚之前的commit，git reset是直接删除指定的commit
-   git reset 是把HEAD向后移动了一下，而git revert是HEAD继续前进，只是新的commit的内容和要revert的内容正好相反，能够抵消要被revert的内容
-   在回滚这一操作上看，效果差不多。但是在日后继续 merge 以前的老版本时有区别

git revert是用一次逆向的commit“中和”之前的提交，因此日后合并老的branch时，之前提交合并的代码仍然存在，导致不能够重新合并

但是git reset是之间把某些commit在某个branch上删除，因而和老的branch再次merge时，这些被回滚的commit应该还会被引入

如果回退分支的代码以后还需要的情况则使用git revert， 如果分支是提错了没用的并且不想让别人发现这些错误代码，则使用git reset

## git merge 和 git rebase 区别

>[!info] > merge操作会生成一个新的节点，之前提交分开显示
>>而rebase操作不会生成新的节点，是将两个分支融合成一个线性的操作。 

如果 主分支 中新的提交和你的工作是相关的。为了将新的提交并入你的分支，你有两个选择：**merge 或 rebase**
- merge 合并代码会产生一次新的 commit
- rebase 则会保持提交树的线性
- rebase 分为 自动式 和 交互式 (-i)
- 未解决完冲突, 可以 `git merge --abort` 中止合并操作

## 项目管理

### git submodule 和 monorepos
某些项目需要包含并使用另外一个项目, 则可以把该项目当做项目的子模块, 它允许你将一个 Git 仓库作为另一个 Git 仓库的子目录。它能让你将另一个仓库克隆到自己的项目中，同时还保持提交的独立

### git hooks

-   在使用 Git 的项目中，我们可以为项目设置 Git Hooks 来帮我们在提交代码的各个阶段做一些代码检查等工作
-   钩子（Hooks） 都被存储在 Git 目录下的 hooks 子目录中。也就是绝大部分项目中的 `.git/hook` 目录

### pre-commit

-   `pre-commit` 就是在代码提交之前做些东西，比如代码打包，代码检测，称之为钩子（hook）
-   在 commit 之前执行一个函数（callback）。这个函数成功执行完之后，再继续 commit，但是失败之后就阻止 commit
-   在 .git->hooks->下面有个 pre-commit.sample* ，这个里面就是默认的函数(脚本)样本

### 清空所有commit信息
> 有时候Git不小心将一些敏感信息提交，所以需要删除提交记录以彻底清除提交信息，以得到一个干净的仓库且代码不变

1. 删除 `.git` 文件夹 重新 `git init`  , 最后 `git push -f` 覆盖
	- 如果项目有多个分支，请慎用这种方法，因为还原成本很高！
2. 新建分支然后覆盖原分支
```bash
# 1. Checkout
git checkout --orphan new_branch

# 2. Add all the files
git add .

# 3. Commit the changes
git commit -am "commit message"

# 4. Delete the branch
git branch -D main

# 5. Rename the current branch to main
git branch -m main

# 6. Force update your repository
git push -f origin main
```


### 修改之前commit的author name

```bash
# 使用 --amend 来修改最近的commit
git commit --amend --author="John Doe <john@doe.org>"

# 使用 git rebase -i Head^{commit_number} 来修改多个 commit

git rebase -i HEAD^{commit_number}

# 将 pick 修改为 Edit
# 逐个修改


```
 git rebase --continue

```