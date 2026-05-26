# Git 学习笔记

## 一、Git 基础概念

### 1.1 什么是Git
Git是一个分布式版本控制系统，用于跟踪文件的变化，协调多人协作开发。

### 1.2 Git 工作区域
- **工作区（Working Directory）**：当前编辑的文件
- **暂存区（Staging Area）**：准备提交的文件
- **本地仓库（Local Repository）**：已提交的文件历史
- **远程仓库（Remote Repository）**：服务器上的仓库（如GitHub）

### 1.3 Git 文件状态
- **未跟踪（Untracked）**：新文件，未被Git管理
- **已修改（Modified）**：已跟踪的文件被修改
- **已暂存（Staged）**：修改已添加到暂存区
- **已提交（Committed）**：修改已保存到本地仓库

---

## 二、Git 配置

### 2.1 用户信息配置
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 2.2 查看配置
```bash
git config --list
git config user.name
git config user.email
```

### 2.3 代理配置（国内访问GitHub）
```bash
# 设置代理
git config --global http.proxy http://127.0.0.1:7892
git config --global https.proxy http://127.0.0.1:7892

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

---

## 三、Git 基本操作

### 3.1 初始化仓库
```bash
git init
```

### 3.2 查看状态
```bash
git status
git status -s  # 简洁模式
```

### 3.3 添加文件到暂存区
```bash
git add <file>          # 添加指定文件
git add .               # 添加所有文件
git add *.txt           # 添加所有txt文件
```

### 3.4 提交文件
```bash
git commit -m "提交信息"
git commit -am "提交信息"  # 添加并提交已跟踪的文件
```

### 3.5 查看提交历史
```bash
git log
git log --oneline        # 简洁模式
git log -5               # 查看最近5条
git log --graph          # 图形化显示
```

### 3.6 查看差异
```bash
git diff                 # 工作区 vs 暂存区
git diff --staged        # 暂存区 vs 最新提交
git diff HEAD            # 工作区 vs 最新提交
```

---

## 四、远程仓库操作

### 4.1 添加远程仓库
```bash
git remote add origin https://github.com/username/repo.git
```

### 4.2 查看远程仓库
```bash
git remote -v
```

### 4.3 推送到远程
```bash
git push origin master
git push -u origin master  # 首次推送，设置上游分支
git push                   # 后续推送
```

### 4.4 从远程拉取
```bash
git pull origin master
git pull                   # 拉取当前分支
```

### 4.5 克隆远程仓库
```bash
git clone https://github.com/username/repo.git
```

---

## 五、分支管理

### 5.1 查看分支
```bash
git branch               # 查看本地分支
git branch -a            # 查看所有分支（包括远程）
git branch -v            # 查看分支及最后提交
```

### 5.2 创建分支
```bash
git branch <branch-name>
```

### 5.3 切换分支
```bash
git checkout <branch-name>
git switch <branch-name>   # Git 2.23+
```

### 5.4 创建并切换分支
```bash
git checkout -b <branch-name>
git switch -c <branch-name>  # Git 2.23+
```

### 5.5 合并分支
```bash
git merge <branch-name>
```

### 5.6 删除分支
```bash
git branch -d <branch-name>      # 删除已合并的分支
git branch -D <branch-name>      # 强制删除
git push origin --delete <branch-name>  # 删除远程分支
```

---

## 六、撤销与回退

### 6.1 撤销工作区修改
```bash
git checkout -- <file>           # 旧版本
git restore <file>               # Git 2.23+
```

### 6.2 撤销暂存区文件
```bash
git reset HEAD <file>            # 旧版本
git restore --staged <file>      # Git 2.23+
```

### 6.3 回退提交
```bash
git reset --soft HEAD~1          # 回退到暂存区
git reset --mixed HEAD~1         # 回退到工作区（默认）
git reset --hard HEAD~1          # 彻底回退，丢弃修改
```

### 6.4 查看操作历史
```bash
git reflog
```

---

## 七、.gitignore 文件

### 7.1 基本语法
```bash
# 注释
*.txt              # 忽略所有txt文件
!readme.txt        # 但不忽略readme.txt
/temp              # 仅忽略根目录下的temp文件夹
build/             # 忽略build文件夹
doc/*.txt          # 忽略doc文件夹下的txt文件
```

### 7.2 常见忽略规则
```bash
# 操作系统文件
.DS_Store
Thumbs.db

# 编辑器文件
.vscode/
.idea/

# 编译文件
*.pyc
*.class
*.exe

# 依赖目录
node_modules/
venv/

# 环境变量
.env
```

---

## 八、SSH 配置

### 8.1 生成SSH密钥
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

### 8.2 查看公钥
```bash
cat ~/.ssh/id_ed25519.pub
```

### 8.3 添加到GitHub
1. 复制公钥内容
2. 访问 https://github.com/settings/keys
3. 点击 "New SSH key"
4. 粘贴公钥并保存

### 8.4 使用SSH地址
```bash
git remote set-url origin git@github.com:username/repo.git
```

---

## 九、常用场景

### 9.1 新建仓库并推送
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/username/repo.git
git push -u origin master
```

### 9.2 克隆并开始开发
```bash
git clone https://github.com/username/repo.git
cd repo
# 开始开发...
git add .
git commit -m "Your changes"
git push
```

### 9.3 解决冲突
```bash
# 1. 拉取最新代码
git pull origin master

# 2. 如果有冲突，手动编辑冲突文件
# 冲突标记：<<<<<<< HEAD ... ======= ... >>>>>>> branch-name

# 3. 解决冲突后
git add <conflicted-files>
git commit -m "Resolve merge conflicts"
git push
```

---

## 十、本次学习实践记录

### 10.1 操作步骤
1. ✅ 初始化Git仓库：`git init`
2. ✅ 配置用户信息：`git config user.name/email`
3. ✅ 创建README.md并提交
4. ✅ 创建vocabulary.txt（英语词汇表）
5. ✅ 创建.gitignore文件
6. ✅ 配置远程仓库：`git remote add origin`
7. ✅ 推送到GitHub：`git push`

### 10.2 遇到的问题及解决
1. **Token权限不足**：需要确保Personal Access Token有repo权限
2. **网络连接问题**：配置代理（端口7892）
3. **代理配置**：使用`git config --global http.proxy`

### 10.3 仓库地址
- GitHub: https://github.com/YunqiYQ/git_test.git

---

## 十一、快捷命令参考

| 命令 | 说明 |
|------|------|
| `git init` | 初始化仓库 |
| `git add .` | 添加所有文件到暂存区 |
| `git commit -m "msg"` | 提交 |
| `git push` | 推送到远程 |
| `git pull` | 拉取远程更新 |
| `git status` | 查看状态 |
| `git log --oneline` | 查看简洁历史 |
| `git branch` | 查看分支 |
| `git checkout -b name` | 创建并切换分支 |
| `git merge name` | 合并分支 |
| `git stash` | 暂存当前修改 |
| `git stash pop` | 恢复暂存的修改 |

---

*最后更新：2026-05-26*
