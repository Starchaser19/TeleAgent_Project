# 协作规范

本文档约定三人团队的 Git 工作流。目标：`main` 随时可运行，改动可追溯，冲突尽量少。

## 1. 角色与权限

| 角色 | 人员 | 权限 |
| --- | --- | --- |
| Owner | Starchaser19 | Admin，负责仓库设置、邀请成员、处理合并冲突 |
| Member | 待补充 | Write，可推送分支、创建 PR |

- 每位成员使用自己的 GitHub 账号，不要把账号密码或 Token 发给别人。
- 修改仓库可见性、删除仓库、管理成员等操作只由 Owner 执行。

## 2. 一次性配置

```bash
git config --global user.name "你的名字"
git config --global user.email "你的GitHub邮箱"
git config --global pull.rebase true   # 可选：让提交历史更线性
```

克隆仓库：

```bash
git clone https://github.com/Starchaser19/TeleAgent_Project.git
```

没有配置 SSH key 时使用 HTTPS 即可；push 时使用 GitHub 账号 + Personal Access Token，或直接用 GitHub Desktop / VS Code 登录。

## 3. 分支模型

- `main`：稳定分支，只接受 PR 合并，任何时候都应该能运行。
- `feat/<姓名>-<主题>`：新功能
- `fix/<姓名>-<主题>`：修复问题
- `docs/<姓名>-<主题>`：文档或材料
- `chore/<姓名>-<主题>`：配置、依赖、杂项

示例：`feat/zhangsan-agent-flow`、`docs/lisi-report-outline`。

规则：

- 一个任务一个分支，尽量 1~2 天内合并。
- 分支合并后删除，不要长期保留。
- 不建 `dev` 分支：三人规模用不上，反而多一层同步成本。

## 4. 日常流程

### 开工

```bash
git switch main
git pull
git switch -c feat/你的名字-主题
```

### 开发与提交

```bash
git add <改动的文件>
git commit -m "feat: 一句话说明"
git push -u origin feat/你的名字-主题
```

提交信息前缀：

| 前缀 | 用途 |
| --- | --- |
| `feat:` | 新功能 |
| `fix:` | 修复问题 |
| `docs:` | 文档 |
| `refactor:` | 重构 |
| `chore:` | 配置、依赖、杂项 |

一次提交只做一件事；不要把临时文件、调试输出、个人配置一起提交。

### 开 PR

1. 在 GitHub 上从你的分支向 `main` 开 Pull Request。
2. 标题写清楚改了什么，描述按模板填写：改了什么、为什么、怎么验证。
3. 指定另一名成员 review；至少一人看过再合并。紧急情况下 Owner 可自行合并，并在群里说明。
4. 合并方式选 **Squash and merge**，保持 `main` 历史干净。
5. 合并后删除远程分支，本地切回 `main` 并 `git pull`。

### 合并后

```bash
git switch main
git pull
git branch -d feat/你的名字-主题   # 删除本地分支
```

## 5. 冲突处理

冲突通常来自“太久没同步”或“两个人改同一文件的同一区域”。

```bash
git switch main
git pull
git switch feat/你的名字-主题
git rebase main        # 或 git merge main
# 解决冲突后
git add <冲突文件>
git rebase --continue  # 若使用 rebase
git push --force-with-lease
```

注意：

- 只有自己的分支可以 force push；**永远不要 force push `main`**。
- 不确定怎么解冲突时，先在群里沟通，不要凭感觉删别人的代码。

## 6. 分工建议

按目录或模块切分，减少同文件冲突：

- 成员 A：智能体流程、提示词、平台配置（`code/`）
- 成员 B：文档、作品报告、演示材料（`doc/`）
- 成员 C：资料整理、测试与验收
- 交叉部分提前在 Issue 里认领，避免重复劳动。

## 7. 不能提交的内容

- 密钥、Token、账号密码（放 `.env`，只提交 `.env.example`）
- 个人隐私数据、未脱敏的调研数据
- 模型权重、大型数据集（确需版本管理时使用 Git LFS）
- 虚拟环境、缓存、IDE 配置、日志

## 8. Issue 使用

- 每个任务开一个 Issue，写清目标、验收标准、负责人、截止时间。
- PR 描述里写 `Closes #<Issue编号>`，合并后自动关闭。
- 讨论结论要回到 Issue 或 PR，不要只留在聊天记录里。

## 9. 常见问题

**push 被拒绝（non-fast-forward）**

说明远程有你没有的提交。先 `git pull`（或 `git pull --rebase`），解决冲突后再 push。

**不小心把密钥提交了**

立即吊销该密钥，再从 Git 历史中移除。只删除文件不够，历史记录里仍然可见。

**两个人改了同一个文件**

先沟通，由一人主改；另一人基于最新 `main` 重新应用改动，不要互相覆盖。

**误删了文件**

未提交的删除可用 `git restore <文件>` 恢复；已提交的可用 `git log` 找到 commit 后执行 `git checkout <commit> -- <文件>`。
