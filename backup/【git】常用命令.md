### 1. 仓库操作

#### 初始化仓库

```bash
git init
```

在当前目录下创建一个新的 Git 仓库。



#### 克隆远程仓库

```bash
git clone <远程仓库地址> [本地目录名]
```

例如 `git clone https://github.com/user/repo.git myrepo` 会将远程仓库克隆到本地的 `myrepo` 目录。



#### 设置用户名和邮箱

```
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```



#### 设置全局的 HTTP 代理

```
git config --global http.proxy http://127.0.0.1:[port]
git config --global https.proxy http://127.0.0.1:[port]
```



#### 查看配置信息

```
git config --list
```



### 2. 文件操作

#### 添加文件到暂存区

```bash
git add <文件路径>
```

可添加单个文件，也可使用 `.` 来添加当前目录下的所有文件，如 `git add .`。



#### 从暂存区移除文件

```bash
git rm --cached <文件路径>
```

该操作只是将文件从暂存区移除，不会删除本地文件。



#### 移动或重命名文件

```bash
git mv <原文件路径> <新文件路径>
```



### 3. 提交操作

#### 提交暂存区的文件到本地仓库

```bash
git commit -m "提交说明"
```

使用 `-a` 选项可以将所有已跟踪文件的修改直接提交，无需先 `git add`，如 `git commit -am "更新代码"`。



#### 修改上一次提交

```bash
git commit --amend -m "新的提交说明"
```

如果修改了文件内容，还可以在 `--amend` 时将新修改的内容合并到上一次提交中。



### 4. 查看状态和日志

#### 查看文件状态

```bash
git status
```

显示工作区、暂存区文件的状态，如哪些文件被修改、添加或删除。



#### 查看提交日志

```bash
git log
```

显示详细的提交历史，可使用 `--oneline` 选项简化输出，如 `git log --oneline`。



#### 查看文件修改差异

```bash
git diff
```

查看工作区与暂存区文件的差异；使用 `git diff --staged` 查看暂存区与最新提交的差异。



### 5. 分支管理

#### 查看分支

```bash
git branch
```

列出本地分支；使用 `-r` 查看远程分支，`-a` 查看所有分支。



#### 创建分支

```bash
git branch <分支名>
```

例如 `git branch new-feature` 创建一个名为 `new-feature` 的分支。



#### 切换分支

```bash
git checkout <分支名>
```

使用 `-b` 选项可以创建并切换到新分支，如 `git checkout -b new-feature`。



#### 合并分支

```bash
git merge <要合并进来的分支名>
```

例如在 `master` 分支上执行 `git merge new-feature` 会将 `new-feature` 分支的修改合并到 `master` 分支。



#### 删除分支

```bash
git branch -d <分支名>
```

使用 `-D` 选项可以强制删除未合并的分支。



### 6. 远程仓库交互

#### 添加远程仓库

```bash
git remote add <远程仓库别名> <远程仓库地址>
```

常见的别名是 `origin`，如 `git remote add origin https://github.com/user/repo.git`。



#### 修改远程仓库

```bash
git remote set-url <远程仓库别名> <远程仓库地址>
```



#### 查看远程仓库信息

```bash
git remote -v
```

显示远程仓库的别名和对应的地址。



#### 从远程仓库拉取代码

```bash
git pull <远程仓库别名> <分支名>
```

例如 `git pull origin master` 从 `origin` 远程仓库的 `master` 分支拉取代码并合并到本地。



#### 推送本地代码到远程仓库

```bash
git push <远程仓库别名> <分支名>
```

如 `git push origin master` 将本地 `master` 分支的代码推送到 `origin` 远程仓库的 `master` 分支。



#### 删除远程分支

```bash
git push <远程仓库别名> --delete <分支名>
```

例如 `git push origin --delete new-feature` 删除 `origin` 远程仓库的 `new-feature` 分支。



### 7. 标签管理

#### 创建标签

```bash
git tag <标签名>
```

创建轻量级标签；使用 `-a` 选项可以创建带注释的标签，如 `git tag -a v1.0 -m "版本 1.0 发布"`。



#### 查看标签

```bash
git tag
```

列出所有标签；使用 `git show <标签名>` 查看标签的详细信息。



#### 推送标签到远程仓库

```bash
git push <远程仓库别名> <标签名>
```

若要推送所有标签，使用 `git push <远程仓库别名> --tags`。

#### 删除本地标签

```bash
git tag -d <标签名>
```



#### 删除远程标签

```bash
git push <远程仓库别名> --delete <标签名>
```



### 8. 撤销操作

#### 撤销工作区的修改

```bash
git checkout -- <文件路径>
```

将文件恢复到上一次提交时的状态。



#### 撤销暂存区的文件

```bash
git reset HEAD <文件路径>
```

将文件从暂存区移除，但保留工作区的修改。



#### 回退到指定提交

```bash
git reset --hard <提交哈希值>
```

`--hard` 选项会同时修改工作区和暂存区；使用 `--soft` 只修改提交历史，不改变暂存区和工作区。



### 9. 贮藏操作

#### 贮藏当前修改

```bash
git stash
```

将工作区和暂存区的修改贮藏起来，使工作区回到干净状态。



#### 查看贮藏列表

```bash
git stash list
```



#### 应用贮藏

```bash
git stash apply [贮藏编号]
```

不指定贮藏编号则应用最近一次的贮藏；使用 `git stash pop` 应用并删除贮藏。



#### 删除贮藏

```bash
git stash drop [贮藏编号]
```

不指定编号则删除最近一次的贮藏。



### 10. 其他命令

#### 查找包含特定内容的提交

```bash
git log -S "<查找内容>"
```



#### 显示某个文件的修改历史

```bash
git blame <文件路径>
```

显示文件每行内容的最后修改者和提交信息。

这些命令涵盖了 Git 日常使用的大部分场景，你可以根据具体需求灵活运用它们来进行高效的版本控制。