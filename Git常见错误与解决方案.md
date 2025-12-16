# Git 常见错误与解决方案速查（实战版）

> 适用人群：Git 初学者 / 科研项目 / 日常工程开发

---

## 目录

1. push 被拒绝（fetch first）
2. merge 冲突（CONFLICT）
3. 提交到错误分支（main / develop）
4. 忘记 add 就 commit
5. 想撤销 commit / add / 修改
6. detached HEAD 状态
7. reset / revert 用错
8. pull 之后代码乱了
9. 误删分支 / 误删文件
10. .gitignore 不生效

---

## 1️⃣ push 被拒绝（fetch first）

### 错误信息

```text
! [rejected] main -> main (fetch first)
```

### 原因

* 远程仓库有你本地没有的提交（README / 他人提交）

### 解决方案（推荐）

```bash
git pull origin main --allow-unrelated-histories
git push origin main
```

⚠️ 谨慎方案

```bash
git push -f origin main
```

---

## 2️⃣ merge 冲突（CONFLICT）

### 错误信息

```text
CONFLICT (content): Merge conflict in xxx.py
```

### 原因

* 两个分支修改了同一行代码

### 解决步骤

```bash
git status
```

1. 打开冲突文件
2. 手动修改，删除 `<<<<<<< ======= >>>>>>>`
3. 保存后：

```bash
git add xxx.py
git commit -m "Resolve merge conflict"
```

---

## 3️⃣ 提交到了错误分支（非常常见）

### 场景

* 本应在 `feature/*`
* 却提交在 `main` 或 `develop`

### 尚未 push（推荐）

```bash
git checkout -b feature/xxx
git reset --soft HEAD~1
git commit -m "Correct commit"
```

### 已 push（不要 reset）

```bash
git revert HEAD
git checkout -b feature/xxx
```

---

## 4️⃣ 忘记 git add 就 commit

### 错误表现

```text
nothing to commit
```

### 正确流程

```bash
git add .
git commit -m "message"
```

---

## 5️⃣ 撤销操作速查（重点）

### 撤销修改（未 add）

```bash
git checkout -- file.py
```

### 撤销 add（回到工作区）

```bash
git reset file.py
```

### 撤销最近一次 commit（保留修改）

```bash
git reset --soft HEAD~1
```

### 撤销 commit（丢弃修改）⚠️

```bash
git reset --hard HEAD~1
```

---

## 6️⃣ detached HEAD 状态

### 现象

```text
You are in 'detached HEAD' state
```

### 原因

* checkout 了某个 commit 或 tag

### 正确做法

```bash
git checkout -b fix-from-old-commit
```

---

## 7️⃣ reset vs revert（高频混淆）

| 命令     | 是否改历史 | 适合场景      |
| ------ | ----- | --------- |
| reset  | ✅     | 本地、未 push |
| revert | ❌     | 已 push、协作 |

### 推荐口诀

> **改历史用 reset，共享历史用 revert**

---

## 8️⃣ git pull 后代码“乱了”

### 原因

* pull = fetch + merge

### 推荐替代方案

```bash
git fetch
git log origin/main --oneline
git merge origin/main
```

或使用 rebase（进阶）

```bash
git pull --rebase
```

---

## 9️⃣ 误删分支 / 文件

### 恢复被删分支

```bash
git reflog
git checkout -b recovered-branch <hash>
```

### 恢复被删文件

```bash
git checkout HEAD -- file.py
```

---

## 🔟 .gitignore 不生效

### 原因

* 文件已经被 Git 跟踪

### 解决方案

```bash
git rm --cached file.log
git commit -m "Remove tracked file"
```

---

## 十一、常用排查命令（必会）

```bash
git status
git log --oneline --graph --all
git branch -a
git remote -v
```

---

## 十二、给科研 / 新手的终极建议

* 不确定时：

```bash
git status
git log --oneline -5
```

* 不要害怕 Git 出错
* **90% 的问题都能恢复**

---

> 📌 推荐文件名：`docs/git-common-errors.md`
>
> 📌 建议长期保存在 GitHub 仓库中作为参考文档
