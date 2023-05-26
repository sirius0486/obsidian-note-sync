---
date: 2023-05-26
author: keqing
tags: Git
---


---
## Git 常见命令和原理
> [!tip] > 通用概念

1. 工作区
2. 暂存区
3. 本地仓库
4. 远程仓库
![[Pasted image 20230131102037.png]]



---



## git init 
> [!success] > 执行该命令后会在本地目录生成 .git 隐藏文件夹, 

---

## git logs
---

## git reflog

---
## git merge

---
## git rebase
>[!info] > 第二种合并分支的方法是 `git rebase`。
>Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。

Rebase 的优势就是可以创造更线性的提交历史，这听上去有些难以理解。如果只允许使用 Rebase 的话，代码库的提交历史将会变得异常清晰。
![[Pasted image 20230129180622.png]]

---
## git pull
---
## git fetch
---
## git reset
---
## git switch {branchName}
---
## git checkout 
---
## git branch -f main {hashValue}
---