# Git 常用命令速查

这份文档按日常使用场景整理。你可以先看“我想做什么”，再直接复制对应命令。

## 1. 查看当前状态

### 我想看哪些文件被修改了

```bash
git status
```

说明：显示当前分支、哪些文件被修改、哪些文件已暂存、哪些文件还没有被 Git 跟踪。

常用简洁版：

```bash
git status --short
```

说明：用更短的格式显示状态，适合快速扫一眼。

## 2. 查看远程仓库

### 我想看我的远程库连接的是谁

```bash
git remote -v
```

说明：查看当前本地仓库连接了哪些远程仓库，以及对应的拉取地址和推送地址。

输出示例：

```text
origin  https://github.com/yourname/project.git (fetch)
origin  https://github.com/yourname/project.git (push)
```

其中 `origin` 是远程仓库的常用默认名字。

### 我想添加远程仓库

```bash
git remote add origin https://github.com/yourname/project.git
```

说明：把本地仓库和一个远程仓库连接起来。`origin` 是远程仓库名称，可以理解为这个远程地址的别名。

### 我想修改远程仓库地址

```bash
git remote set-url origin https://github.com/yourname/new-project.git
```

说明：当远程地址写错了，或者仓库迁移了，用这个命令修改。

### 我想删除远程仓库连接

```bash
git remote remove origin
```

说明：删除本地仓库里名为 `origin` 的远程连接。这个命令不会删除 GitHub/Gitee 上的远程仓库本身。

## 3. 搞清楚 `origin` 和 `master`

### 一句话区分

```text
origin 是远程仓库的名字。
master 是分支的名字。
```

它们不是同一种东西，只是经常一起出现，所以容易混。

### `origin` 是什么

`origin` 是本地 Git 给远程仓库起的一个别名。

比如你执行：

```bash
git remote add origin https://github.com/Ma-zhengyu/AIops.git
```

意思是：

```text
以后我在这个本地仓库里，用 origin 这个名字代表 https://github.com/Ma-zhengyu/AIops.git 这个远程仓库。
```

所以：

```bash
origin
```

不是分支名，也不是 GitHub 用户名，而是一个远程仓库的本地别名。

你可以用下面命令查看 `origin` 到底指向哪里：

```bash
git remote -v
```

可能看到：

```text
origin  https://github.com/Ma-zhengyu/AIops.git (fetch)
origin  https://github.com/Ma-zhengyu/AIops.git (push)
```

这表示：

```text
origin = https://github.com/Ma-zhengyu/AIops.git
```

### `master` 是什么

`master` 是一个分支名。

分支可以有很多个，比如：

```text
master
main
dev
feature/git-notes
feature/login
```

你可以用下面命令查看本地有哪些分支：

```bash
git branch
```

如果看到：

```text
* master
```

说明你当前在本地 `master` 分支上。

注意：现在很多新仓库默认分支叫 `main`，老一些的仓库常见默认分支叫 `master`。它们本质上都是分支名，只是名字不同。

### `origin/master` 又是什么

`origin/master` 可以理解为：

```text
远程仓库 origin 上的 master 分支，在你本地看到的样子。
```

拆开看：

```text
origin/master
```

意思是：

```text
origin 这个远程仓库
/
master 这个远程分支
```

所以：

```text
origin/master 不是一个本地分支
```

它通常是一个远程跟踪分支，用来告诉你：上次从远程同步时，远程 `master` 分支长什么样。

### 本地 `master` 和远程 `origin/master` 的关系

你本地可以有一个：

```text
master
```

远程仓库上也可以有一个：

```text
origin/master
```

它们名字相似，但不是同一个东西。

可以这样理解：

```text
master        = 你电脑上的本地分支
origin/master = GitHub 远程仓库里的 master 分支在本地的映射
```

当你提交代码时：

```bash
git commit -m "提交说明"
```

提交先进入本地 `master`。

当你推送代码时：

```bash
git push
```

或者第一次推送：

```bash
git push -u origin master
```

Git 才会把本地 `master` 的提交推送到远程 `origin/master`。

### `git push -u origin master` 到底怎么读

```bash
git push -u origin master
```

可以按下面方式理解：

```text
git push        推送
-u              顺便建立长期对应关系
origin          推送到哪个远程仓库
master          推送哪个本地分支
```

完整意思是：

```text
把我当前本地的 master 分支，推送到 origin 这个远程仓库里的 master 分支，并建立对应关系。
```

这里命令里只出现了一个 `master`，但 Git 会默认理解成：

```bash
git push -u origin master:master
```

完整格式其实是：

```bash
git push 远程仓库名 本地分支名:远程分支名
```

所以：

```bash
git push -u origin master:master
```

意思是：

```text
把本地 master 分支，推送到 origin 远程仓库里的 master 分支，并建立对应关系。
```

两个 `master` 分别是：

```text
左边 master：本地分支 master
右边 master：远程分支 master
```

而：

```bash
git push -u origin master
```

是同名分支推送的简写。因为只写了一个 `master`，Git 默认远程分支也叫 `master`。

如果你想让本地分支和远程分支名字不一样，也可以明确写出来：

```bash
git push -u origin master:main
```

意思是：

```text
把本地 master 分支，推送到 origin 远程仓库里的 main 分支，并建立对应关系。
```

### `-u` 建立的是仓库关系还是分支关系

`-u` 建立的是分支之间的对应关系，不是仓库之间的对应关系。

比如：

```bash
git push -u origin master
```

建立的是：

```text
本地分支 master  <-->  远程分支 origin/master
```

不是建立：

```text
本地仓库  <-->  远程仓库 origin
```

仓库和仓库的连接，是下面这类命令建立的：

```bash
git remote add origin https://github.com/Ma-zhengyu/AIops.git
```

这句话的意思是：

```text
给当前本地仓库添加一个远程仓库，名字叫 origin。
```

而：

```bash
git push -u origin master
```

是在已经有 `origin` 这个远程仓库连接的基础上，进一步告诉 Git：

```text
以后我在本地 master 分支上执行 git push 或 git pull，
默认就去找 origin/master。
```

可以分成两层理解：

```text
第一层：仓库和仓库的连接
git remote add origin 仓库地址

第二层：分支和分支的对应关系
git push -u origin master
```

再说得更短一点：

```text
origin 管“远程仓库是谁”。
-u 管“当前本地分支默认对应远程哪个分支”。
```

如果你有多个本地分支，它们的 upstream 是各自独立的：

```text
本地 master  ->  远程 origin/master
本地 dev     ->  远程 origin/dev
本地 feature ->  远程 origin/feature
```

所以每个新分支第一次推送时，通常都要单独建立一次 upstream：

```bash
git push -u origin 分支名
```

建立对应关系后，以后你在本地 `master` 分支上就可以直接：

```bash
git push
```

不用每次都写：

```bash
git push origin master
```

### `origin` 可以改名吗

可以，但通常没必要。

比如你可以把远程仓库叫 `github`：

```bash
git remote add github https://github.com/Ma-zhengyu/AIops.git
```

那推送时就要写：

```bash
git push -u github master
```

但是日常最推荐用默认习惯：

```text
origin
```

因为大多数教程、工具、团队协作都会默认使用这个名字。

### `master` 可以改名吗

可以。

比如很多项目现在用 `main` 作为默认分支。那第一次推送就会变成：

```bash
git push -u origin main
```

这里：

```text
origin 还是远程仓库名
main 是分支名
```

所以不要死记 `master`，要先看你当前分支叫什么：

```bash
git branch
```

当前分支前面会有 `*`。

### 最容易记混的地方

#### 错误理解

```text
origin 是主分支。
master 是远程仓库。
```

这是反的。

#### 正确理解

```text
origin 是远程仓库别名。
master 是分支名。
```

#### 再加一层

```text
origin/master 是 origin 远程仓库里的 master 分支。
```

### 一个完整例子

假设你的远程仓库是：

```text
https://github.com/Ma-zhengyu/AIops.git
```

你本地当前分支是：

```text
master
```

那么第一次推送：

```bash
git push -u origin master
```

可以翻译成：

```text
把我电脑上的 master 分支，推送到 GitHub 上 origin 指向的那个仓库，并在远程也叫 master。
```

之后日常推送：

```bash
git push
```

可以翻译成：

```text
把当前分支的新提交，推送到它已经绑定好的远程分支。
```

### 三个常用查看命令

查看 `origin` 指向哪个远程仓库：

```bash
git remote -v
```

查看当前在哪个本地分支：

```bash
git branch
```

查看本地分支和远程分支的对应关系：

```bash
git branch -vv
```

记住这三条，`origin` 和 `master` 基本就不会再糊成一团。

## 4. 初始化和克隆仓库

### 我想把当前文件夹变成 Git 仓库

```bash
git init
```

说明：在当前目录创建一个新的 Git 仓库。执行后会生成 `.git` 目录。

### 我想从远程仓库下载一份代码

```bash
git clone https://github.com/yourname/project.git
```

说明：把远程仓库完整复制到本地。

指定本地文件夹名：

```bash
git clone https://github.com/yourname/project.git my-folder
```

说明：把远程仓库克隆到 `my-folder` 文件夹。

## 5. 添加和提交修改

### 我想把某个文件加入暂存区

```bash
git add 文件名
```

示例：

```bash
git add README.md
```

说明：把指定文件的修改放入暂存区，准备提交。

### 我想把当前目录下所有修改都加入暂存区

```bash
git add .
```

说明：把当前目录及子目录里的新增、修改、删除都加入暂存区。

### 我想提交一次修改

```bash
git commit -m "提交说明"
```

示例：

```bash
git commit -m "docs: add git command cheatsheet"
```

说明：把暂存区里的修改提交到本地仓库。提交说明要尽量写清楚这次改了什么。

### 我想跳过暂存，直接提交已跟踪文件的修改

```bash
git commit -am "提交说明"
```

说明：只适用于已经被 Git 跟踪的文件。新文件不会被自动加入，需要先 `git add 新文件名`。

## 6. 查看修改内容

### 我想看还没有暂存的具体改动

```bash
git diff
```

说明：查看工作区里尚未加入暂存区的修改。

### 我想看已经暂存、准备提交的具体改动

```bash
git diff --staged
```

说明：查看已经 `git add`、但还没有 `git commit` 的修改。

### 我想看某个文件的修改

```bash
git diff 文件名
```

示例：

```bash
git diff docs/01-general-aiops.md
```

## 7. 查看提交历史

### 我想看提交记录

```bash
git log
```

说明：查看完整提交历史，包括提交 ID、作者、日期和提交说明。

### 我想用一行显示每次提交

```bash
git log --oneline
```

说明：更适合快速查看历史。

### 我想看图形化分支历史

```bash
git log --oneline --graph --all
```

说明：用简单图形展示分支和合并关系。

## 8. 分支操作

### 我想看当前有哪些分支

```bash
git branch
```

说明：列出本地分支，当前所在分支前面会有 `*`。

### 我想看本地和远程所有分支

```bash
git branch -a
```

说明：同时显示本地分支和远程分支。

### 我想新建一个分支

```bash
git branch 分支名
```

示例：

```bash
git branch feature/login
```

说明：创建分支，但不会自动切换过去。

### 我想切换到某个分支

```bash
git switch 分支名
```

示例：

```bash
git switch main
```

说明：切换到指定分支。

老版本 Git 也可以用：

```bash
git checkout 分支名
```

### 我想新建并切换到这个分支

```bash
git switch -c 分支名
```

示例：

```bash
git switch -c feature/git-notes
```

说明：创建新分支，并立刻切换过去。

老版本 Git 也可以用：

```bash
git checkout -b 分支名
```

### 我想删除本地分支

```bash
git branch -d 分支名
```

说明：删除已经合并过的本地分支。

如果确认要强制删除：

```bash
git branch -D 分支名
```

说明：强制删除分支，即使它还没有合并。使用前要确认分支上的内容不再需要。

## 9. 拉取和推送

### 我想把远程仓库的最新内容拉到本地

```bash
git pull
```

说明：从当前分支对应的远程分支拉取最新内容，并合并到本地。

### 我想只获取远程更新，但先不合并

```bash
git fetch
```

说明：下载远程仓库的最新信息，但不会自动改动当前工作区。

### 我想把本地提交推送到远程仓库

```bash
git push
```

说明：把本地当前分支的提交推送到对应远程分支。

### 我第一次推送新分支到远程

```bash
git push -u origin 分支名
```

示例：

```bash
git push -u origin feature/git-notes
```

说明：把本地分支推送到远程，并建立本地分支和远程分支的跟踪关系。以后在这个分支上可以直接用 `git push` 和 `git pull`。

### 我第一次 `git push` 报错：当前分支没有 upstream

如果你执行：

```bash
git push
```

看到类似错误：

```text
fatal: The current branch master has no upstream branch.
```

意思是：当前本地分支还没有和远程分支建立对应关系。Git 不知道你想把本地这个分支推送到远程的哪个分支。

推荐执行：

```bash
git push -u origin master
```

如果当前分支不是 `master`，把 `master` 换成你的分支名：

```bash
git push -u origin 当前分支名
```

说明：`-u` 是 `--set-upstream` 的简写，意思是建立本地分支和远程分支的长期对应关系。

建立之后，以后在这个分支上就可以直接用：

```bash
git push
git pull
```

### `git push`、`git push origin 分支名`、`git push -u origin 分支名` 有什么区别

#### 已经建立 upstream 后，直接推送

```bash
git push
```

说明：把当前分支推送到它已经绑定的远程分支。

适合场景：这个分支已经执行过 `git push -u origin 分支名`，或者已经有远程跟踪分支。

#### 明确推送到远程某个分支

```bash
git push origin 分支名
```

示例：

```bash
git push origin master
```

说明：把本地 `master` 分支推送到远程 `origin/master`。如果远程还没有 `master` 分支，通常会创建一个远程同名分支。

注意：这个命令会推送，但不一定帮你建立长期 upstream。也就是说，下次你直接执行 `git push`，仍然可能提示没有 upstream。

#### 第一次推送新分支，推荐写法

```bash
git push -u origin 分支名
```

示例：

```bash
git push -u origin master
```

说明：完成两件事：

1. 把本地分支推送到远程。
2. 建立本地分支和远程分支的对应关系。

以后在这个分支上可以直接：

```bash
git push
```

或者：

```bash
git pull
```

### 远程怎么创建新分支

远程分支通常不是单独用一个“创建命令”创建的，而是在推送时创建。

比如你本地新建了一个分支：

```bash
git switch -c feature/git-notes
```

这时候只是创建了本地分支，远程仓库里还没有这个分支。

第一次推送它：

```bash
git push -u origin feature/git-notes
```

如果远程 `origin` 里还没有 `feature/git-notes`，Git 会在远程创建一个同名分支：

```text
本地分支：feature/git-notes
远程分支：origin/feature/git-notes
```

同时，`-u` 会建立对应关系。以后你在这个本地分支上直接执行：

```bash
git push
```

就会推送到远程的 `origin/feature/git-notes`。

### 本地创建新分支后，远程会自动创建吗

只执行本地建分支命令，不会。

例如：

```bash
git switch -c feature/git-notes
```

这个命令只是在你电脑上创建本地分支。远程 GitHub/Gitee 上不会立刻出现这个分支。

远程分支要等你第一次推送时才会创建：

```bash
git push -u origin feature/git-notes
```

或者：

```bash
git push origin feature/git-notes
```

两者区别是：

```text
git push origin feature/git-notes
```

会把本地 `feature/git-notes` 推送到远程同名分支。如果远程没有这个分支，会创建它。

```text
git push -u origin feature/git-notes
```

除了会创建远程同名分支，还会建立 upstream。以后可以直接 `git push` 和 `git pull`。

所以日常更推荐：

```bash
git push -u origin 新分支名
```

### 远程分支能不能默认自动创建

可以，但要分清两个层次。

#### 只创建本地分支时

```bash
git switch -c feature/git-notes
```

不会自动创建远程分支。

Git 不会因为你本地新建了一个分支，就马上去 GitHub/Gitee 创建远程分支。

#### 第一次直接 `git push` 时

默认情况下，如果这个新分支还没有 upstream，直接执行：

```bash
git push
```

可能会报错：

```text
fatal: The current branch feature/git-notes has no upstream branch.
```

如果你开启了下面配置：

```bash
git config --global push.autoSetupRemote true
```

那么以后新分支第一次直接：

```bash
git push
```

Git 会尝试自动做类似下面这件事：

```bash
git push -u origin 当前分支名
```

也就是：在远程创建同名分支，并建立 upstream。

不过刚开始学 Git 时，建议先手动写清楚：

```bash
git push -u origin 当前分支名
```

这样你会更清楚自己正在把哪个本地分支推到哪个远程分支。

### 每换一个新分支，都要重新建立 upstream 吗

如果这个本地分支是第一次推送到远程，一般需要建立一次。

例如：

```bash
git switch -c feature/git-notes
git push -u origin feature/git-notes
```

之后在 `feature/git-notes` 分支上，就可以直接：

```bash
git push
```

可以这样记：

```text
每个新分支第一次推送：git push -u origin 分支名
同一个分支后续推送：git push
```

### 我怎么查看当前分支有没有 upstream

```bash
git branch -vv
```

说明：查看本地分支和远程分支的对应关系。

输出示例：

```text
* master da4f60e [origin/master] 首次总结
```

其中 `[origin/master]` 表示当前本地 `master` 分支已经对应远程 `origin/master`。

如果没有类似 `[origin/xxx]` 的内容，说明这个分支可能还没有建立 upstream。

### 我想让 Git 自动给新分支建立 upstream

可以设置：

```bash
git config --global push.autoSetupRemote true
```

说明：开启后，对于没有 upstream 的新分支，直接执行 `git push` 时，Git 会尝试自动把它推送到远程同名分支，并建立对应关系。

查看是否已经开启：

```bash
git config --global --get push.autoSetupRemote
```

如果输出：

```text
true
```

说明已经开启。

如果你是 Git 新手，建议先熟悉：

```bash
git push -u origin 分支名
```

理解清楚 upstream 之后，再考虑是否开启自动设置。

## 10. 撤销和恢复

### 我想撤销某个文件还没有暂存的修改

```bash
git restore 文件名
```

示例：

```bash
git restore README.md
```

说明：把文件恢复到最近一次提交或暂存的状态。这个操作会丢掉当前未暂存的修改。

### 我想把已经暂存的文件取消暂存

```bash
git restore --staged 文件名
```

说明：把文件从暂存区拿出来，但保留工作区里的修改。

### 我想撤销最近一次提交，但保留文件修改

```bash
git reset --soft HEAD~1
```

说明：撤销最近一次提交，修改仍然保留在暂存区。

### 我想撤销最近一次提交，并保留修改但不暂存

```bash
git reset HEAD~1
```

说明：撤销最近一次提交，修改保留在工作区。

### 我想用一个新的提交来撤销某次提交

```bash
git revert 提交ID
```

说明：生成一个新的提交，用来抵消指定提交的内容。这个方式适合已经推送到远程仓库的提交。

## 11. 暂存当前工作

### 我想临时保存当前修改，先去做别的事

```bash
git stash
```

说明：把当前未提交的修改临时存起来，让工作区变干净。

### 我想查看临时保存了哪些内容

```bash
git stash list
```

说明：查看所有 stash 记录。

### 我想恢复最近一次临时保存的修改

```bash
git stash pop
```

说明：恢复最近一次 stash，并从 stash 列表中删除它。

### 我想恢复 stash，但不删除记录

```bash
git stash apply
```

说明：恢复 stash 内容，但 stash 记录仍然保留。

## 12. 标签

### 我想查看所有标签

```bash
git tag
```

说明：列出当前仓库里的所有标签，常用于版本号。

### 我想创建一个标签

```bash
git tag v1.0.0
```

说明：给当前提交打一个标签。

### 我想把标签推送到远程

```bash
git push origin v1.0.0
```

说明：把指定标签推送到远程仓库。

## 13. 常见工作流程

### 我修改完文件后，想提交并推送

```bash
git status
git add .
git commit -m "提交说明"
git push
```

说明：先确认修改，再加入暂存区，然后提交，最后推送到远程。

### 我开始工作前，想先同步远程最新代码

```bash
git status
git pull
```

说明：先确认本地有没有未提交修改，再拉取远程最新内容。

### 我想新开一个功能分支并推送到远程

```bash
git switch -c feature/your-feature
git push -u origin feature/your-feature
```

说明：创建并切换到新分支，然后把这个新分支推送到远程。

## 14. 推荐记住的高频命令

```bash
git status
git remote -v
git add .
git commit -m "提交说明"
git pull
git push
git log --oneline
git branch
git switch 分支名
git switch -c 新分支名
git diff
```

如果只记一条排查命令，优先记：

```bash
git status
```

它会告诉你当前仓库大部分关键状态。
