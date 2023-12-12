## git命令

### 

Workspace：工作区
Index / Stage：暂存区
Repository：本地仓库区
Remote：远程仓库

### 新建代码仓库

```shell
# 初始化git代码仓库
git init

# 新建一个目录 将其初始化成git代码仓库
git init [projetc-name]

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