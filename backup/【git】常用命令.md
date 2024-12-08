1. **配置命令**
   - `git config`：用于配置Git，例如设置用户姓名和邮箱。
     - `git config --global user.name "Your Name"`：设置全局用户名。
     - `git config --global user.email "your@email.com"`：设置全局用户邮箱。
2. **仓库初始化和克隆命令**
   - `git init`：在当前目录初始化一个新的Git仓库，会创建一个隐藏的`.git`目录来管理仓库信息。
   - `git clone [repository - url]`：克隆一个远程仓库到本地，例如`git clone https://github.com/username/repository.git`。
3. **基本文件操作命令**
   - `git add [file - name]`或`git add.`：将文件添加到暂存区。前者是添加指定文件，后者是添加当前目录下所有更改的文件。
   - `git commit -m "commit - message"`：将暂存区的文件提交到本地仓库，`commit - message`是提交说明，用于记录本次提交的内容。
   - `git status`：查看仓库的状态，包括文件的修改、暂存情况等。
4. **分支操作命令**
   - `git branch`：查看本地分支列表。
   - `git branch [branch - name]`：创建一个新的本地分支。
   - `git checkout [branch - name]`：切换到指定的分支。
   - `git merge [branch - name]`：将指定分支合并到当前分支。
5. **远程仓库操作命令**
   - `git remote add [remote - name] [remote - repository - url]`：添加一个远程仓库，例如`git remote add origin https://github.com/username/repository.git`，其中`origin`是远程仓库别名，后面是远程仓库的URL。
   - `git push [remote - name] [branch - name]`：将本地分支推送到远程仓库，例如`git push origin master`。
   - `git pull [remote - name] [branch - name]`：从远程仓库拉取并合并指定分支的最新内容到本地分支，例如`git pull origin master`。
6. **查看历史记录命令**
   - `git log`：查看提交历史记录，包括作者、日期、提交信息等内容。可以使用`git log --oneline`来查看简洁的提交记录，一行显示一个提交。