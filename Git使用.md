下面我按**“三个角色 + 一条完整主线”**给你一份 **Git 基础命令速查 + 实战流程**，覆盖你关心的三件事：

1️⃣ **你自己本地建立仓库**
2️⃣ **把项目发布到 GitHub**
3️⃣ **别人如何把代码提交到你的 GitHub 项目（标准协作方式）**

所有命令都可直接复制使用。

---

# 一、你自己：从 0 建立一个 Git 仓库（本地）

### 1️⃣ 初始化仓库

```bash
cd your_project_directory
git init
```

生成 `.git/` 目录，当前文件夹变成 Git 仓库。

---

### 2️⃣ 查看仓库状态

```bash
git status
```

---

### 3️⃣ 添加文件到暂存区

```bash
git add file1.py
git add .
```

> `.` 表示添加所有变更文件

---

### 4️⃣ 提交到本地仓库

```bash
git commit -m "Initial commit"
```

📌 **良好习惯**：提交信息要简洁、明确

---

# 二、你自己：把本地项目发布到 GitHub

## 方式一：GitHub 已创建空仓库（推荐）

### 1️⃣ 在 GitHub 上创建仓库

* New Repository
* 不勾选 README（避免冲突）
* 假设仓库地址是：

```text
https://github.com/yourname/project.git
```

---

### 2️⃣ 关联远程仓库

```bash
git remote add origin https://github.com/yourname/project.git
```

查看是否成功：

```bash
git remote -v
```

---

### 3️⃣ 推送代码到 GitHub

```bash
git branch -M main
git push -u origin main
```

`-u`：建立默认上游分支，后续可直接 `git push`

---

## 方式二：GitHub CLI（可选）

```bash
gh repo create project --public --source=. --push
```

---

# 三、别人：如何参与并向你的 GitHub 项目提交代码

这是**标准 GitHub 协作流程（Fork + Pull Request）**

---

## 👤 场景：别人要给你的项目提交代码

### Step 1️⃣ Fork 你的仓库（在 GitHub 页面）

对方点击你的仓库右上角 **Fork**
👉 会在 **他自己的 GitHub 账号下**生成一份拷贝

---

### Step 2️⃣ 克隆自己的 Fork 仓库

```bash
git clone https://github.com/otheruser/project.git
cd project
```

---

### Step 3️⃣ 添加你的仓库为上游（upstream）

```bash
git remote add upstream https://github.com/yourname/project.git
git remote -v
```

---

### Step 4️⃣ 基于 main / develop 创建功能分支

```bash
git checkout -b feature/my-change
```

---

### Step 5️⃣ 编写代码并提交

```bash
git add .
git commit -m "Add new feature xxx"
```

---

### Step 6️⃣ 推送到自己的 GitHub

```bash
git push origin feature/my-change
```

---

### Step 7️⃣ 在 GitHub 发起 Pull Request（PR）

* base repository：`yourname/project`
* base branch：`main` 或 `develop`
* compare branch：`otheruser:feature/my-change`

---

## 👤 你作为维护者要做什么？

### 1️⃣ 审查代码

* Review changes
* Comment / Request changes

---

### 2️⃣ 合并 PR

```text
Merge pull request
```

GitHub 自动完成合并

---

# 四、你作为维护者：如何允许别人“直接 push”（不推荐）

⚠️ **只适合非常熟的小团队**

### 1️⃣ 在 GitHub 仓库设置

```
Settings → Collaborators → Add people
```

---

### 2️⃣ 对方克隆你的仓库

```bash
git clone https://github.com/yourname/project.git
```

---

### 3️⃣ 对方直接提交

```bash
git checkout -b feature/xxx
git add .
git commit -m "..."
git push origin feature/xxx
```

你再在 GitHub 上合并分支。

---

# 五、你最常用的 10 个 Git 基础命令（速查）

```bash
git init              # 初始化仓库
git status            # 查看状态
git add .             # 添加所有文件
git commit -m "msg"   # 提交
git log --oneline     # 简洁日志
git branch            # 查看分支
git checkout -b xxx   # 创建并切换分支
git merge xxx         # 合并分支
git pull              # 拉取并合并
git push              # 推送
```

---

# 六、推荐你科研项目的最小协作流程（实践版）

```text
你：
  main        → 论文最终结果
  develop     → 日常实验

别人：
  fork → feature/xxx → PR → develop
```

---

# 七、常见新手坑（非常重要）

❌ 忘了 `git add` 就 `commit`
❌ 在 `main` 上直接写代码
❌ 不建分支就改功能
❌ PR 一次提交太多无关内容

