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

## 3. 初始化和克隆仓库

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

## 4. 添加和提交修改

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

## 5. 查看修改内容

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

## 6. 查看提交历史

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

## 7. 分支操作

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

## 8. 拉取和推送

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

## 9. 撤销和恢复

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

## 10. 暂存当前工作

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

## 11. 标签

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

## 12. 常见工作流程

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

## 13. 推荐记住的高频命令

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
