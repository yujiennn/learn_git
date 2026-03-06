# learn_git
这个仓库用来学习和巩固git

## Git流程原理

### 工作区 (Working Directory)
- 本地开发的地方
- 包含项目的所有文件

### 暂存区 (Staging Area / Index)
- 中间缓冲区
- 用 `git add` 命令将文件从工作区添加到暂存区

### 本地仓库 (Local Repository)
- 存储提交历史的地方
- 用 `git commit` 命令将暂存区的文件提交到本地仓库

### 远程仓库 (Remote Repository)
- GitHub、GitLab等托管平台上的仓库
- 用 `git push` 推送本地更改到远程仓库
- 用 `git pull` 拉取远程仓库的更新到本地

### Git工作流程图
```
工作区 --(git add)--> 暂存区 --(git commit)--> 本地仓库 --(git push)--> 远程仓库
  ↑                                                 ↓
  |----------------------------------------(git pull)--------|
```

## Git常用命令

### 初始化和配置
| 命令 | 说明 |
|------|------|
| `git init` | 初始化一个新的git仓库 |
| `git clone <url>` | 克隆远程仓库到本地 |
| `git config --global user.name "name"` | 配置全局用户名 |
| `git config --global user.email "email"` | 配置全局邮箱 |

### 查看状态
| 命令 | 说明 |
|------|------|
| `git status` | 查看工作区和暂存区的状态 |
| `git log` | 查看提交历史 |
| `git log --oneline` | 单行显示提交历史 |
| `git diff` | 查看工作区与暂存区的差异 |
| `git diff --cached` | 查看暂存区与本地仓库的差异 |
| `git show <commit>` | 查看某个提交的详细信息 |

### 添加和提交
| 命令 | 说明 |
|------|------|
| `git add <file>` | 添加指定文件到暂存区 |
| `git add .` | 添加所有修改文件到暂存区 |
| `git commit -m "message"` | 提交暂存区的文件到本地仓库 |
| `git commit -am "message"` | 跳过暂存区，直接提交已追踪文件 |
| `git commit --amend` | 修改最后一次的提交 |

### 分支管理
| 命令 | 说明 |
|------|------|
| `git branch` | 列出本地分支 |
| `git branch -a` | 列出所有分支（本地和远程） |
| `git branch <branch-name>` | 创建新分支 |
| `git checkout <branch-name>` | 切换到指定分支 |
| `git checkout -b <branch-name>` | 创建并切换到新分支 |
| `git switch <branch-name>` | 切换分支（新语法） |
| `git merge <branch-name>` | 合并指定分支到当前分支 |
| `git branch -d <branch-name>` | 删除分支 |
| `git branch -D <branch-name>` | 强制删除分支 |

### 远程仓库操作
| 命令 | 说明 |
|------|------|
| `git remote -v` | 查看远程仓库列表 |
| `git remote add origin <url>` | 添加远程仓库 |
| `git remote remove origin` | 移除远程仓库 |
| `git push origin <branch>` | 推送指定分支到远程仓库 |
| `git push -u origin <branch>` | 推送并设置上游分支 |
| `git pull origin <branch>` | 拉取并合并远程分支 |
| `git fetch origin` | 获取远程更新但不合并 |

### 撤销和修改
| 命令 | 说明 |
|------|------|
| `git restore <file>` | 恢复工作区文件到最后一次提交状态 |
| `git restore --staged <file>` | 从暂存区移除文件 |
| `git reset HEAD <file>` | 取消暂存区的文件 |
| `git reset --soft HEAD~1` | 撤销最后一次提交，保留更改在暂存区 |
| `git reset --mixed HEAD~1` | 撤销最后一次提交，保留更改在工作区 |
| `git reset --hard HEAD~1` | 完全撤销最后一次提交，丢弃所有更改 |
| `git revert <commit>` | 通过新提交来撤销指定提交的更改 |
| `git clean -fd` | 删除未追踪的文件和目录 |

### 高级操作
| 命令 | 说明 |
|------|------|
| `git rebase <branch>` | 重新应用当前分支的提交到另一分支上 |
| `git stash` | 暂存当前的未提交更改 |
| `git stash pop` | 恢复最近一次暂存的更改 |
| `git cherry-pick <commit>` | 将指定提交应用到当前分支 |
| `git tag <tag-name>` | 创建标签 |
| `git tag -a <tag-name> -m "message"` | 创建带注释的标签 |

## 常见Git工作流程

### 开发新功能流程
```
1. git checkout -b feature/new-feature      # 创建功能分支
2. # 进行开发和修改
3. git add .                                # 添加更改到暂存区
4. git commit -m "Add new feature"         # 提交更改
5. git push -u origin feature/new-feature  # 推送到远程
6. # 在GitHub/GitLab上创建Pull Request
7. git checkout main                       # 切换回主分支
8. git merge feature/new-feature           # 合并功能分支
9. git push origin main                    # 推送到远程
```

### 日常开发流程
```
1. git pull origin main                    # 拉取最新的远程更改
2. # 进行开发工作
3. git status                              # 查看更改状态
4. git add <changed-files>                 # 添加修改到暂存区
5. git commit -m "Descriptive message"    # 提交更改
6. git push origin <branch-name>           # 推送到远程仓库
```

## 提交信息规范

良好的提交信息应该遵循以下格式：

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type（类型）
- `feat`: 新功能
- `fix`: 修复bug
- `docs`: 文档更新
- `style`: 代码格式化（不影响功能）
- `refactor`: 代码重构
- `test`: 添加或修改测试
- `chore`: 构建过程、依赖管理等

### 示例
```
feat(user-auth): add login functionality

Implemented user login with email and password validation.
Added session management for user persistence.

Closes #123
```
