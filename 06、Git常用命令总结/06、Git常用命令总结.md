# Git常用命令总结

### 一   常用命令

1. 初始化新仓库 `git init`
2. 克隆旧仓库 `git clone +https://github.com/Jeasonstand/arr.git`
3. 查看状态 `git status`
4. 提交单个文件 `git add index.php`
5. 提交所有文件 `git add -A`
6. 使用通配符提交 `git add *.js`
7. 提交到仓库中 `git commit -m '提示信息'`
8. 提交已经跟踪过的文件，不需要执行add `git commit -a -m '提交信息'`
9. 删除版本库与项目目录中的文件 `git rm index.php`
10. 只删除版本库中文件但保存项目目录中文件 `git rm --cached index.php`
11. 修改最后一次提交 `git commit --amend`



### 二   回滚提交

1. 放弃没有提交的修改 `git checkout .`
2. 删除没有add 的文件和目录 `git clean -fd`
3. 显示将要删除的文件或目录 `git clean -n`



### 三   清理资源

git clean命令用来从工作目录中删除所有没有跟踪（tracked）过的文件

1. `git clean -n`是一次clean的演习, 告诉你哪些文件会被删除
2. `git clean -f`删除当前目录下没有tracked过的文件，不会删除.gitignore指定的文件
3. `git clean -df`删除当前目录下没有被tracked过的文件和文件夹



### 四   恢复提交

使用reset恢复到历史提交点，重置暂存区与工作目录的内容。

1. 清空工作区和暂存区的改动 `git reset --hard`
2. 恢复前三个版本 `git reset --hard HEAD^^^`
3. 保留工作区的内容，把文件差异放进暂存区 `git reset --soft`



### 五   日志查看

1. 查看日志 `git log`
2. 查看最近2次提交日志并显示文件差异 `git log -p -2`
3. 显示已修改的文件清单 `git log --name-only`
4. 显示新增、修改、删除的文件清单 `git log --name-status`
5. 一行显示并只显示SHA-1的前几个字符 `git log --oneline`



### 六   定义别名

通过创建命令别名可以减少命令输入量。

```text
git config --global alias.c commit
```

> 可以在配置文件 ~/.gitconfig 中查看或直接编辑

下面是一个Git命令Alias配置

```text
[alias]
	a = add .
	c = commit
	s = status
	l = log
	b = branch
```

现在可以使用 `git a` 实现 `git add .` 一样的效果了。



### 七   常用别名

在 `~/.zshrc` 文件中定义常用的别名指令

```text
alias gs="git status"
alias gc="git commit -m "
alias gl="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit  "
alias gb="git branch"
alias ga="git add ."
alias go="git checkout"
```

命令行直接使用 `gs` 即可以实现 `git status` 一样的效果了。

> window 系统需要使用 git for window 中的 `Git Base` 软件

### 八   .gitignore

.gitignore用于定义忽略提交的文件

- 所有空行或者以注释符号 `＃` 开头的行都会被 Git 忽略。
- 匹配模式最后跟反斜杠（`/`）说明要忽略的是目录。
- 可以使用标准的 glob 模式匹配。

```text
.idea
/vendor
.env
/node_modules
/public/storage
*.txt
```

### 九   Branch

分支用于为项目增加新功能或修复Bug时使用。

1. 创建分支 `git branch dev`

2. 查看分支 `git branch`

3. 切换分支 `git checkout dev`

4. 创建并切换分支 `git checkout -b feature/bbs`

5. 合并dev分支到master

   ```text
   git checkout master
   git merge dev
   ```

6. 删除分支 `git branch -d dev`

7. 删除没有合并的分支`git branch -D dev`

8. 删除远程分支 `git push origin :dev`

9. 查看未合并的分支(切换到master) `git branch --no-merged`

10. 查看已经合并的分支(切换到master) `git branch --merged`

### 十   冲突解决

不同分修改同一个文件或不同开发者修改同一个分支文件都可能造成冲突，造成无法提交代码。

1. 使用编辑器修改冲突的文件
2. 添加暂存 `git add .` 表示已经解决冲突
3. git commit 提交完成

### 十一   Stashing

当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，你不想提交进行了一半的工作，否则以后你无法回到这个工作点。

"暂存" 可以获取你工作目录的中间状态——也就是你修改过的被追踪的文件和暂存的变更——并将它保存到一个未完结变更的堆栈中，随时可以重新应用。

1. 储藏工作 `git stash`
2. 查看储藏列表 `git stash list`
3. 应用最近的储藏 `git stash apply`
4. 应用更早的储藏 `git stash apply stash@{2}`
5. 删除储藏`git stash drop stash@{0}`
6. 应用并删除储藏 `git stash pop`

### 十二   Tag

Git 也可以对某一时间点上的版本打上标签 ，用于发布软件版本如 v1.0

1. 添加标签 `git tag v1.0`
2. 列出标签 `git tag`
3. 推送标签 `git push --tags`
4. 删除标签 `git tag -d v1.0.1`
5. 删除远程标签 `git push origin :v1.0.1`

### 十三   打包发布

对mster分支代码生成压缩包供使用者下载使用，`--prefix` 指定目录名

```text
git archive master --prefix='hdcms/' --format=zip > hdcms.zip
```