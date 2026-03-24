### Git常用命令总结

#### 基础操作

```
git init
# 初始化一个新的 Git 仓库

git clone [url]
# 克隆远程仓库到本地

git status
# 查看当前工作区和暂存区的状态

git add [file] or .
# 将文件添加到暂存区

git commit -m "message"
# 提交暂存区的文件到版本库
```



#### 分支管理

```
git branch
# 列出本地分支

git checkout [branch]
# 切换到指定分支

git checkout -b [branch]
# 创建并切换到新的分支

git merge [branch]
# 合并指定分支到当前分支

git branch -d [branch]
# 删除指定分支
```



#### 版本控制

```
git log
# 查看提交日志

git diff
# 查看工作区、暂存区与版本库的差异

git reset --hard [commit]
# 恢复到指定的提交版本
```



#### 远程操作

```
git remote -v
# 查看远程仓库信息

git pull
# 拉取远程仓库的更新

git push [remote] [branch]
# 推送本地分支到远程仓库
```



#### 标签与协作

```
git tag [tagname]
# 创建标签

git fetch
# 从远程仓库下载对象和引用

git cherry-pick [commit]
# 将指定提交应用于当前分支
```



#### 高级操作

```
git rebase [branch]
# 将当前分支的提交移到目标分支之后

git stash
# 保存当前工作进度并恢复到上一次提交状态

git bisect
# 二分查找引入 bug 的提交
```



#### 撤销与回复

```
git checkout -- [file]
# 撤销对文件的修改，恢复到最近一次提交的状态

git revert [commit]
# 撤销指定提交的修改，生成新的提交记录

git reset HEAD [file]
# 将文件从暂存区移出，放回工作区
```

