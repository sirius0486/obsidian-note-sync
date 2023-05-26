## 本地修改文件(但没有 git add 到暂存区), 想放弃修改

### 单文件
```bash
git checkout --filename
```
### 多文件
```bash
git checkout .
```

## 本地新增文件(且没有 git add)

### 单文件
直接删除新增文件即可, 或者 `rm filename / rm dir -rf`

### 多文件
`git clean -xdf`

## 本地修改/新增一堆文件, 且git add到暂存区了, 想放弃修改

### 单个文件/文件夹：

```shell
git reset HEAD filename
```

### 所有文件/文件夹：

```bash
git reset HEAD .
```

## 撤销某次 commit
```bash
git reset commit_id
```

## git初始配置

### 用户名和邮箱
```shell
# 全局设置
git config --global user.name 'Your User Name'
git config --global user.email 'Your User email'

# 当前项目设置
git config user.name 'Your User Name'
git config user.email 'Your User email'

# 查看配置信息是否正确
git config --list
```


### 自动追踪远程分支

```shell
git config --global push.default current
git config --global push.autoSetupRemote true

# 查看自动追踪上游分支是否正确
git config --get push.default
git config --get push.autoSetupRemote
```