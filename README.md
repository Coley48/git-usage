# git-usage

该项目用于记录 git 学习笔记，同时也用于测试 git 各种命令等。

### progit 学习笔记

- [在线文档](https://git-scm.com/book/zh/v2)
- [PDF电子书](https://github.com/progit/progit2-zh/releases/download/2.1.55/progit_v2.1.55.pdf)

### 关于版本控制

> 版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。 在本书所展示的例子中，我们对保存着软件源代码的文件作版本控制，但实际上，你可以对任何类型的文件进行版本控制。

git 是基于差异（delta-based）的版本控制工具；

在 Git中，每当你提交更新或保存项目状态时，它基本上就会对当时的全部文件创建一个快照并保存这个快照的索引。为了效率，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

git 会为每个版本都创建一个快照。

### git 工作方式

基本的 Git 工作流程如下：
1. 在工作区中修改文件。
2. 将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。
3. 提交更新，找到暂存区的文件，将快照永久性存储到 Git 目录。


文件的三种状态：已提交（committed）、已修改（modified） 和 已暂存（staged）。
- 已修改表示修改了文件，但还没保存到数据库中。
- 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
- 已提交表示数据已经安全地保存在本地数据库中。

结合文件的三种状态，与之对应的有三个位置：工作区（workspace）、暂存区（index）、Git仓库（repository）；
- 工作区是对项目的某个版本独立提取出来的内容。 这些从 Git 仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。
- 暂存区是一个文件，保存了下次将要提交的文件列表信息，一般在 Git 仓库目录中。 按照 Git 的术语叫做“索引”，不过一般说法还是叫“暂存区”。
- Git仓库是 Git 用来保存项目的元数据和对象数据库的地方。 这是 Git 中最重要的部分，从其它计算机克隆仓库时，复制的就是这里的数据。

![git工作三个阶段](./image/git三个阶段.png)

### 安装 git

Windows 上安装：

1. 从官网下载，[地址](https://git-scm.com/downloads)；
2. 执行安装程序，不更改默认选项，一路确认完成安装；
3. 安装完成后查看 git 版本，`git --version` ；

[Linux、Mac 安装](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

### 使用 git


#### 配置 git

安装完 Git 之后，要做的第一件事就是设置你的用户名和邮件地址。 这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改。该配置项会被写入用户文件夹下的.gitconfig 文件中。

```bash
$ git config --global user.name "username"
$ git config --global user.email username@example.com
```

查看配置信息

```bash
$ git config <key> # 显示指定配置项
$ git config --list # 显示所有配置信息
$ git config --list --show-origin # 显示配置信息及配置文件路径
$ git config --global core.editor "path/to/editor" # 配置默认的编辑器
```

#### 创建仓库

创建仓库一般分为两种方式

1. 在本地创建

```bash
$ cd /path/to/myProject # 进入到项目文件夹下
$ git init # 在本地创建git仓库，将尚未进行版本控制的本地目录转换为 Git 仓库；
```

`git init`命令将创建一个名为 .git 的子目录（隐藏文件夹），这个子目录包括初始化的 Git 仓库中所有的必须文件，这些文件是Git 仓库的骨干。

2. 从远程克隆

```bash
$ git clone https://github.com/User/Project.git # 使用http协议在当前文件夹下下载Project项目
$ git clone git@github.com:User/Project.git # 使用git协议在当前文件夹下下载Project项目
$ git clone https://github.com/User/Project.git newName # 下载Project项目到newName文件夹中，也可以跟路径，下载到指定位置
$ git clone -b <branchName> https://github.com/User/Project.git # 下载项目指定分支
# 下载链接后的 .git 可以不加；
```

当执行`git clone`命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。

#### git 修改与提交

```bash
$ git status # 查看文件状态
$ git status -s/--short # 查看文件状态的简略信息
$ git add <file> # 添加跟踪文件到暂存区
$ git add *.c # 添加所有.c文件
$ git add . # 添加所有文件
$ git diff <file> # 比较工作目录中当前文件和暂存区域快照之间的差异；
$ git diff --staged # 比对已暂存文件与最后一次提交的文件差异;
$ git commit # 提交代码到本地仓库，
$ git commit -m "comments" # 提交代码并添加注释
```

`git status -s/--short`命令显示的简略信息中，文件名前会显示两列标志，左栏指明了暂存区的状态，右栏指明了工作区的状态，?表示未跟踪，A表示新增，M表示修改过

#### git 

#### 获取帮助

查看命令的解释，以及详细用法；打开的是本地的英文网页文档；

```bash
$ git help <action>
$ git <action> --help
$ git <action> -h # 命令缩写
```

#### 忽略文件

当项目中有一些缓存文件、日志文件、临时文件、测试文件等不需要跟踪的文件时，可以在项目根目录下新建一个`.gitignore`文件，将不需要跟踪的文件添加进去，git 会忽略到这些文件。

`.gitignore`文件格式规范：

- 所有空行或者以 # 开头的行都会被 Git 忽略，注释。
- 可以使用标准的 glob 模式匹配，它会递归地应用在整个工作区中。
- 匹配模式可以以（/）开头防止递归。
- 匹配模式可以以（/）结尾指定目录。
- 要忽略指定模式以外的文件或目录，可以在模式前加上叹号（!）取反。

其中 glob 模式是指 shell 所使用的简化了的正则表达式。、
- 星号（*）匹配零个或多个任意字符；
- [abc] 匹配任何一个列在方括号中的字符；
- 问号（?）只匹配一个任意字符；
- 如果在方括号中使用短划线分隔两个字符，表示匹配这两个字符范围内的字符；
- 使用两个星号（\*\*）表示匹配任意中间目录；


更新.gitignore文件
git rm -r --cached .

创建单独分支
git checkout --orphan <branch-name>

移除所有文件
git rm -rf .

查看所有分支，包括远程分支
git branch -a

删除远程分支
git push origin --delete <branch-name>


! [rejected] gh-pages -> gh-pages (non-fast-forward)
git push --set-upstream origin gh-pages


#### 推送分支到远程服务器 `git push --set-upstream origin <BranchName>`

```bash
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'secondary' on GitHub by visiting:
remote:      https://github.com/Coley48/git-test/pull/new/secondary
remote:
To https://github.com/Coley48/git-test
 * [new branch]      secondary -> secondary
Branch 'secondary' set up to track remote branch 'secondary' from 'origin'.
```

#### 删除分支  `git branch -d <BranchName>`

```
Deleted branch test (was 12876d8).
```

#### 删除远程分支 `git push origin --delete <BranchName>`

```
To https://github.com/Coley48/git-test
 - [deleted]         secondary
 ```

### git 可视化工具

#### github desktop

#### git gui

### 参考资料

[git 官网](https://git-scm.com/)