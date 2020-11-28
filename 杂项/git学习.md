## git学习

### 底层命令

1. git对象
   1. git hash-object -w fileUrl	：生成一个key：value键值对。存到.get/objects
   2. git cat-file -p hash    ：拿对应对象的内容
   3. git cat-file -t hsh        ：拿对应对象的类型
2. tree对象
3. commit对象

### 查看暂存区

git ls-files -s

### 初始化仓库

git init

### 新增操作

git status

git add ./

git commit -m "msg"

### 修改

git status

git add ./

git commit -m "msg"

### 删除&重命名

git rm 要删除的文件		git mv 老文件名    新文件名

git status

git commit -m "msg"

### 查询操作

git status	:查看文件状态(已跟踪,未跟踪(已提交,已暂存,已修改))

git diff	:未暂存修改

git diff --cache	:未提交暂存

git log --oneline	

git log --oneline --decorate --graph --all

### 分支

git branch	:查看分支列表

git branch name	:在当前提交对象上创建新分支

git branch name commithash	:在指定的提交对象上创建分支

git checkout name	:切换分支

git branch -d name	:删除已经合并的分支

git branch -D name	:强制删除

git branch -v	:查看分支指向的最新提交

### 切换分支

动三个地方:

最佳实践:每次切换分支前,当前分支一定是干净状态(已提交)

坑:在切换分支时,当前分支上有未暂存的修改(第一次),或有未提交的暂存(第一次).分支可以切换,可能会污染其他分支

​	HEAD

​	暂存区

​	工作目录

### 合并分支

1. **快速合并**
2. **典型合并**

### git存储

git stash

git stash list

git stash apply stash@{}

git stash pop

git stash drop name

### 后悔药

- ___工作区___
  - git checkout --文件名
- ___暂存区___
  - git reset HEAD filename
- ___版本库___
  - git commit --amend



#### rest

- 三部曲
  - 第一步：git reset --soft HEAD~      本质是撤销了上一次的commit（只动HEAD，带着分支一起动）。git reset --soft  hash
  - 第二步：git reset --mixed HEAD~    动HEAD、动暂存区
  - 第三步：git reset --hard HEAD~        动HEAD、动暂存区、动工作目录



