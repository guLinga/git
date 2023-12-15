## git命令

Workspace：工作区
Index / Stage：暂存区
Repository：本地仓库区
Remote：远程仓库

### 新建代码仓库

```shell
# 初始化git代码仓库
git init

# 新建一个目录 将其初始化成git代码仓库
git init [project-name]

# 下载一个项目和它的整个代码历史
git clone [url]
```

### git分支

git中代码分支分为‘本地分支’和‘远程分支’。

```shell
# 查看本地分支
git branch

# 查看本地分支 并查看每个分支的最后一次提交
git branch -v

# 查看远程分支
git branch -r

# 查看所有分支
git branch -a

# 当然查看远程分支和所有分支的时候也可以加上-v来查看分支的最后一次提交
# 查看分支时，当前的分支前面会有一个*，*只会加在本地分支前面

# 新建本地分支
git branch [branch-name]

# 切换分支
git checkout [branch-name]

# 新建分支并切换
git checkout -b [branch-name]

# 发布本地分支
git checkout [branch-name]
git push -u [origin] [branch-name]

# 删除本地分支
# 首先切换到其他分支
git checkout [main]
# 删除本地分支 如果这个分支包含了一些还没有合并到其他任何位置的更改, Git 会拒绝删除
git branch -d [branch-name]
# 强制删除本地分支
git branch -D [branch-name]

# 删除远程分支
git push -d [origin] [branch-name]

# 修改本地和远程分支名称
## 修改本地分支的名称
git branch -m [old-branch-name] [new-branch-name]
### 如果目前所在的分支就是要修改名称的分支则不需要输入[old-branch-name]
## 删除旧的远程分支
git push -d [origin] [old-branch-name]
## 将改过名的本地分支推送到远程
git push -u [origin] [old-branch-name]

# 合并分支到当前分支
git merge [branch-name]
```

### git仓库

```shell
# 查看已有的远程仓库
git remote -v

# 添加远程仓库
git remote add [remote-name] [remote-url]

# 删除远程仓库
git remote remove [remote-url] / git remote rm [remote-name]

# 修改远程仓库名称
git remote rename [old-remote-name] [new-remote-name]
```

### git配置

```shell
# 显示当前的git配置
git config --list
git config -l

git config --list --global
git config -l --global

# 编辑git配置文件
git config -e
git config -e --global

# 设置提交时的用户信息
git config user.name [name] --golbal
git config user.email [email] --global
```

### 暂存区

```shell
# 添加指定文件到暂存区
git add [file1-name] [file2-name]

# 添加指定目录到暂存区，包括子目录
git add [dir]

# 添加当前目录的所有文件到暂存区
git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
git add -p
git add [file-name] -p
## 如果使用了git add -p终端会有以下输出
## Stage this hunk [y,n,q,a,d,e,?]?
## 具体字母代表的什么会在下面介绍

# 将git add后还没commit的数据从暂存区移
git reset [file-name]
git reset
```

### git add -p

|名称|英文介绍|中文介绍|
|----|----|----|
|y|stage this hunk|存储这个hunk|
|n|do not stage this hunk|不存储这个hunk|
|q|quit; do not stage this hunk nor any of the remaining ones|离开，不存储这个hunk和其他hunk|
|a|stage this hunk and all later hunks in the file|存储这个hunk和这个文件后面的hunk|
|d|do not stage this hunk nor any of the later hunks in the file|不存储这个hunk和这个文件后面的hunk|
|g|select a hunk to go to|选择一个hunk|
|/|search for a hunk matching the given regex|通过正则查找hunk|
|j|leave this hunk undecided, see next undecided hunk|不确定是否存储这个hunk，看下一个不确定的hunk|
|J|leave this hunk undecided, see next hunk|不确定是否存储这个hunk，看下一个hunk|
|k|leave this hunk undecided, see previous undecided hunk|不确定是否存储这个hunk，看上一个不确定的hunk|
|K|leave this hunk undecided, see previous hunk|不确定是否存储这个hunk，看上一个hunk|
|s|split the current hunk into smaller hunks|把当前的hunk分成更小的hunks|
|e|manually edit the current hunk|手动编辑当前的hunk|
|?|print help|输出帮助信息|

### 工作区
```shell
# 撤销在工作区修改的内容
git checkout -- [file-name]
git checkout -- .
```

### 本地仓库区
```shell
# 提交代码到本地仓库区
git commit -m [commit-message]
git commit [file1-name] [file2-name] -m [commit-message]

# 合并 git add .和git commit -m的操作
git commit -am [commit-message]

# 改写上一次commit的信息
git commit --amend -m [message]
## git commit -amend -m [message]是使用一次新的commit，替代上一次提交
## 如果代码没有任何新变化，则用来改写上一次commit的提交信息
## 所以，如果想要改写上一次commit的信息，代码不能做任何更新

# 撤销所有的还没push的commit
git reset --soft origin/[branch-name]
```

### 标签
```shell
# 列出本地所有的tag
git tag

# 列出远程仓库所有的tag
git ls-remote --tags [remote-name]

新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
git tag [tag] [commit]

# 删除本地的tag
git tag -d [tag-name]

git push origin :refs/tags/[tagName]

# 查看tag信息
git show [tag]

# 提交指定tag
git push [remote] [tag]

# 提交全部的tag
git push [remote] --tag

# 新建一个分支指向某个tag
git checkout -b [branch-name] [tag-name]

# 切换到tag对应的代码状态
git checkout [tag-name]
## 如果分支名和tag名一样
git checkout refs/tags/[tag-name]
```

### 暂存

```shell
# 将暂时不想提交的同时暂存起来
git stash
git stash save [message]

# 取消暂存
git stash pop

# 查看git stash的信息
git stash list

# 查看stash修改了哪些内容
git stash show -p stash@{n}
```