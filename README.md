# git使用手册

## git配置
```
git config --global user.name "name"
git config --global user.email email@email.com
```

### 查看配置信息
```
git config --list
```

## git 分支
```
git branch - 查看本地分支
git branch -A 查看所有分支
git checkout branchName // 切换分支
git branch -D branchName // 删除分支
```

### 创建文件夹分支
```
git checkout -b folderName1/folderName2/branchName

```

## git stash
```
git stash save "message" // 将当前本地分支的更改存入堆栈,存储之前必须要执行 git add 操作
git stash list // 查看stash记录
git stash show stash@{Num} // 显示某一条stash做了哪些更改
git stash apply stash@{Num} // 将某一条stash恢复至本地
git stash pop stash@{Num} // 将某一条stash恢复至本地,并删除此条stash记录
git stash drop stash@{$num} // 删除某一条stash记录
git stash clear // 删除所有缓存的stash
```

## git 流程
```
git init [newrepo] // 初始化git仓库
git add . \ git add * // 将本地更改添加到暂存区
git commit -m "commit message" // 将暂存区内容提交到本地仓库
git push \ git push --set-upstream branchName - 将本地仓库内容推送到远端
```

### 从远端拉取项目
```
git clone href
git clone -b branchName href // 拉取指定分支
```
```
git fetch // 获取远端代码
git merge origin/branchName // 将远端指定分支代码合并至本地当前分支
```
```
git pull // 拉取并合并
```

## 实际问题

### 有merge时，删除分支
```
git add .
git stash save "save message" // 将当前更改存入堆栈中
git branch -D branch
```

### 误删stash
```
git fsck --unreachable \ git fsck --lost-found // 查看删除的stash\commit记录
git show id // 查看删除stash记录的具体信息
git merge id // 合并删除的stash
```

### 本地切换远程新建的分支
- 远程创建分支后
```
git fetch
git branch -a // 查看一下所有的分支
git checkout origin/branchName
git switch -c origin/branchName
```
### 本地切换远程分支并在本地创建新分支
```
git checkout -b branchName origin/branchName
```

### git commit失败

#### 报错信息 - pre-commit hook failed (add --no-verify to bypass)
```
$ git commit -m "message"
  > running pre-commit hook: lint-staged
 pre-commit hook failed (add --no-verify to bypass)
```
- 错误原因
  - 项目中有*error*，导致*eslint*检测未通过，提交失败。
- 解决方案
  - 在配置文件中，不需要使用eslint时，把lintOnSave设为false即可
  - 在项目中执行 *npm run lint*找到问题，并修改，之后再提交即可

### you have not concluded your merge
```
git fetch -all
git reset --hard origin/feature/daishoulun/master_addModule_zl_dsl_20220303
```
- 此方法会放弃本地所有修改
