###  git reset 和 git revert 的区别
> [!note] > 撤销(revert)被设计为撤销公开的提交(比如已经push)的安全方式，git reset被设计为重设本地更改



因为两个命令的目的不同，它们的实现也不一样：重设完全地移除了一堆更改，而撤销保留了原来的更改，用一个新的提交来实现撤销

两者主要区别如下：

-   git revert是用一次新的commit来回滚之前的commit，git reset是直接删除指定的commit
-   git reset 是把HEAD向后移动了一下，而git revert是HEAD继续前进，只是新的commit的内容和要revert的内容正好相反，能够抵消要被revert的内容
-   在回滚这一操作上看，效果差不多。但是在日后继续 merge 以前的老版本时有区别

git revert是用一次逆向的commit“中和”之前的提交，因此日后合并老的branch时，之前提交合并的代码仍然存在，导致不能够重新合并

但是git reset是之间把某些commit在某个branch上删除，因而和老的branch再次merge时，这些被回滚的commit应该还会被引入

如果回退分支的代码以后还需要的情况则使用git revert， 如果分支是提错了没用的并且不想让别人发现这些错误代码，则使用git reset