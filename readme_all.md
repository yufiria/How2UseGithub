# Git 命令详细教程

Git 是目前最流行的分布式版本控制系统，掌握常用命令能极大提升开发效率。下面从零开始，系统介绍 Git 的核心命令与使用场景。

---

## 1. Git 基础概念

- **工作区（Working Directory）**：你电脑上能看到的目录。
- **暂存区（Staging Area / Index）**：介于工作区和版本库之间，用于临时存放改动。
- **本地仓库（Local Repository）**：存放在 `.git` 目录中，保存所有历史版本。
- **远程仓库（Remote Repository）**：托管在服务器上的仓库（如 GitHub、GitLab）。

---

## 2. 安装与配置

### 安装

- **Linux**：`sudo apt install git`（Debian/Ubuntu）或 `sudo yum install git`（RHEL/CentOS）
- **Mac**：`brew install git` 或下载安装包
- **Windows**：下载 [Git for Windows](https://git-scm.com/download/win)

### 首次配置

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git config --global core.editor "vim"          # 设置默认编辑器
git config --global color.ui auto              # 开启颜色显示
```

查看配置：`git config --list`

---

## 3. 创建与克隆仓库

### 初始化新仓库

```bash
git init                    # 在当前目录创建.git仓库
```

### 克隆远程仓库

```bash
git clone <url>             # 克隆到当前目录
git clone <url> <dir>       # 克隆到指定目录
```

---

## 4. 基本操作

### 查看状态

```bash
git status                  # 查看工作区与暂存区状态
git status -s               # 简洁输出
```

### 添加文件到暂存区

```bash
git add <file>              # 添加指定文件
git add .                   # 添加所有改动（包括新文件、修改、删除）
git add -A                  # 与 . 类似，但也会添加删除的文件
```

### 提交

```bash
git commit -m "message"     # 提交暂存区内容
git commit -a -m "message"  # 跳过 git add，直接提交所有已跟踪文件的修改（不含新文件）
```

### 查看提交历史

```bash
git log                     # 完整历史
git log --oneline           # 简洁一行显示
git log --graph --oneline --all   # 图形化显示分支历史
git log -n 3                # 只显示最近3条
```

---

## 5. 撤销与回退

### 撤销工作区修改（未 add）

```bash
git checkout -- <file>      # 丢弃工作区的修改（危险，不可恢复）
```

### 撤销暂存区（已 add 未 commit）

```bash
git reset HEAD <file>       # 将文件从暂存区移回工作区（保留工作区修改）
git reset HEAD               # 撤销所有暂存区文件
```

### 撤销提交（已 commit）

```bash
git reset --soft HEAD~1     # 撤销最后一次提交，但修改保留在暂存区
git reset --mixed HEAD~1    # 撤销提交，修改保留在工作区（默认）
git reset --hard HEAD~1     # 完全删除最后一次提交，修改也丢失（危险）
```

### 撤销远程提交（回退后强制推送）

```bash
git reset --hard <commit-id>
git push --force            # 谨慎使用，会覆盖远程历史
```

---

## 6. 分支管理

### 查看分支

```bash
git branch                  # 本地分支
git branch -r               # 远程分支
git branch -a               # 所有分支
```

### 创建分支

```bash
git branch <branch-name>    # 基于当前分支创建新分支
git checkout -b <branch>    # 创建并切换到新分支
```

### 切换分支

```bash
git checkout <branch-name>  # 切换到已有分支
git switch <branch-name>    # Git 2.23+ 推荐
```

### 合并分支

```bash
git checkout main           # 切换到目标分支
git merge <feature>         # 将 feature 合并到当前分支
```

### 删除分支

```bash
git branch -d <branch>      # 删除已合并分支
git branch -D <branch>      # 强制删除未合并分支
git push origin --delete <branch>  # 删除远程分支
```

---

## 7. 远程仓库

### 查看远程仓库

```bash
git remote -v               # 查看远程仓库地址
```

### 添加远程仓库

```bash
git remote add origin <url>
```

### 推送本地分支

```bash
git push origin <branch>    # 推送指定分支
git push -u origin <branch> # 推送并设置上游跟踪（之后可直接 git push）
git push --all              # 推送所有本地分支
```

### 拉取远程更新

```bash
git fetch                   # 下载远程内容，但不合并
git pull                    # 相当于 git fetch + git merge
git pull --rebase           # 使用 rebase 方式合并
```

### 克隆特定分支

```bash
git clone -b <branch> <url>
```

---

## 8. 标签（Tag）

### 创建标签

```bash
git tag v1.0                # 轻量标签
git tag -a v1.0 -m "message" # 附注标签
```

### 推送标签

```bash
git push origin v1.0        # 推送单个标签
git push --tags             # 推送所有标签
```

### 删除标签

```bash
git tag -d v1.0             # 本地删除
git push origin --delete v1.0 # 远程删除
```

---

## 9. 比较与差异

### 查看工作区与暂存区的差异

```bash
git diff
```

### 查看暂存区与最新提交的差异

```bash
git diff --staged           # 或 git diff --cached
```

### 查看两次提交的差异

```bash
git diff <commit1> <commit2>
```

### 查看某个文件的修改历史

```bash
git log -p <file>
```

---

## 10. 储藏（Stash）

### 临时保存当前工作区

```bash
git stash                  # 保存所有未提交修改
git stash save "message"   # 带说明保存
```

### 查看储藏列表

```bash
git stash list
```

### 恢复储藏

```bash
git stash apply            # 恢复最近储藏，但不删除
git stash pop              # 恢复并删除最近储藏
git stash apply stash@{1}  # 恢复指定储藏
```

### 删除储藏

```bash
git stash drop stash@{0}
git stash clear            # 清空所有储藏
```

---

## 11. 变基（Rebase）

### 基本用法

```bash
git checkout feature
git rebase main            # 将 feature 分支变基到 main 分支最新提交之上
```

### 交互式变基（修改历史）

```bash
git rebase -i HEAD~3       # 修改最近3次提交（可合并、修改、删除提交）
```

### 注意

- **不要对已推送的公共分支进行变基**，否则会重写历史，导致团队协作混乱。

---

## 12. 高级技巧

### 修改最后一次提交

```bash
git commit --amend -m "new message"   # 修改提交信息
git add forgotten_file && git commit --amend   # 补充遗漏文件
```

### 清理未跟踪文件

```bash
git clean -n               # 列出会删除的文件（预览）
git clean -fd              # 删除未跟踪文件和目录
```

### 查找谁是某行代码的作者

```bash
git blame <file>
```

### 子模块（Submodule）

```bash
git submodule add <url> path
git submodule update --init --recursive
```

---

## 13. 常见工作流示例

### 开发新功能并合并到 main

```bash
git checkout -b feature/new-login
# 修改代码
git add .
git commit -m "Add login feature"
git push -u origin feature/new-login   # 推送到远程，便于协作
# 创建 Pull Request 或合并
git checkout main
git pull origin main
git merge feature/new-login
git push origin main
git branch -d feature/new-login
git push origin --delete feature/new-login
```

### 同步上游仓库（Fork 场景）

```bash
git remote add upstream <original-repo-url>
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

---

## 14. 配置文件与别名

### 配置文件位置

- 系统级：`/etc/gitconfig`
- 用户级：`~/.gitconfig`
- 项目级：`.git/config`

### 设置别名（简化命令）

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"
```

之后可以用 `git co`、`git br`、`git st`、`git lg`。

---

## 15. 常见问题与解决

### 合并冲突

```bash
# 冲突时，手动编辑文件，删除 >>> <<< 等标记
git add <file>
git commit -m "resolve conflict"
```

### 误提交敏感信息

```bash
# 使用 git filter-branch 或 BFG Repo-Cleaner 彻底清除
# 推荐 BFG：https://rtyley.github.io/bfg-repo-cleaner/
```

### 忘记添加 .gitignore，提交了不需要的文件

```bash
echo "node_modules/" >> .gitignore
git rm -r --cached node_modules
git commit -m "Remove node_modules from repo"
```

---

以上是 Git 的常用命令及用法。实际使用中，建议多练习并结合图形化工具（如 GitKraken、SourceTree、VS Code 内置 Git）辅助理解。熟记核心命令，配合 `git help <command>` 可随时查看帮助。
