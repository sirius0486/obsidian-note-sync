## 多人协同相关

### 拉取代码遇到冲突怎么办

###  分支操作

### 

## 本地 git 操作

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
# 1. 创建新的 branch

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

都用于 **合并分支** ,
- merge 合并代码会产生一次新的 commit
- rebase 则会保持提交树的线性

## 多项目管理
### submodule 和 monorepos

