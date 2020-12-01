# git-test

用于测试git功能



# 常用命令行

### 添加文件追踪

`git add [file-name]` 添加单个或多个文件
`git add .` 添加所有文件


### 提交文件并添加描述 `git commit -m "some descriptions"`

### 推送到远程服务器 `git push`

### 推送分支到远程服务器 `git push --set-upstream origin <BranchName>`
```
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'secondary' on GitHub by visiting:
remote:      https://github.com/Coley48/git-test/pull/new/secondary
remote:
To https://github.com/Coley48/git-test
 * [new branch]      secondary -> secondary
Branch 'secondary' set up to track remote branch 'secondary' from 'origin'.
```


### 查看当前状态 `git status`

```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

### 查看分支列表 `git branch`

```
  test
  dev
* main
```

### 创建分支 `git branch <BranchName>`


### 切换分支 `git checkout <BranchName>`

```
Switched to branch 'main'
M       README.md
Your branch is up to date with 'origin/main'.
```

### 合并分支 `git merge <BranchName>`

```
error: Your local changes to the following files would be overwritten by merge:
        README.md
Please commit your changes or stash them before you merge.
Aborting
Updating 12876d8..a5b0277
```

### 创建并切换到该分支 `git checkout -b <BranchName>`

```
Switched to a new branch 'test'
```

### 删除分支  `git branch -d <BranchName>`

```
Deleted branch test (was 12876d8).
```

### 删除远程分支 `git push origin --delete <BranchName>`

```
To https://github.com/Coley48/git-test
 - [deleted]         secondary
 ```s