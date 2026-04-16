---
name: commit
description: 提交代码并将本次变更记录追加到 README.md 的版本管理章节
disable-model-invocation: true
---

## 绝对禁止（最高优先级）

- **绝对不要**将当前分支合并（merge/rebase）到 release 分支
- **绝对不要**将代码推送到 release 分支（包括 `git push origin HEAD:release`、`git push origin release` 等任何形式）
- **绝对不要**在本次 skill 执行过程中运行 `git push`、`git merge`、`git rebase` 到 release 的任何命令
- 即使本地分支的上游追踪是 `origin/release`，也**绝对不要**执行 `git push`
- 本 skill 的职责仅限于"本地提交 + 更新 README"，**不涉及任何远程操作**
- 如需合并到 release，必须由用户在 skill 执行之外另行明确指令

请按以下步骤执行提交并更新 README：

## 第一步：收集信息

并行执行：

1. 运行 `git status` 查看改动文件列表
2. 运行 `git diff` 查看具体改动内容
3. 运行 `git branch --show-current` 获取当前分支名
4. 运行 `git config user.name` 获取作者名
5. 读取 `README.md`，定位 `## 版本管理` 章节

## 第二步：生成 commit message

根据改动内容，生成符合 Conventional Commits 规范的中文 commit message：
- 格式：`type(scope): 简短描述`
- type 使用：feat / fix / refactor / style / docs / chore / optimize
- 描述使用中文，简洁说明"做了什么"（不超过 50 字）
- 如改动涉及多个模块，在正文用 `-` 列表逐条说明

展示 commit message 给我确认，**等我确认后再执行后续步骤**。

## 第三步：更新 README.md 版本管理章节

在 `## 版本管理` 章节中找到与**当前分支**对应的小节（格式为 `### 需求概述（分支名）`）。

- 如果找到对应小节，在该小节末尾追加一条记录
- 如果**未找到**对应小节，在 `## 版本管理` 章节末尾新增小节

追加的记录格式如下：

```
- `YYYY-MM-DD` **[作者]** type(scope): 简短描述

  - 明细1
  - 明细2

```

- 日期使用今天的实际日期（ISO 格式），作者取 git user.name
- 第一行与 commit message 第一行完全一致
- 如 commit message 有正文列表，原样缩进追加在标题下方

## 第四步：提交

1. 将所有相关文件加入暂存区（包括更新后的 README.md，不含 .env、密钥等敏感文件）
2. 不要提交 .umirc.ts、vite.config.ts 文件
3. 执行提交，**不要**添加 Co-Authored-By 行

如有不确定是否应该提交的文件，先列出来询问我。

## 提交完成后的动作

- 提交完成后**仅**输出 commit 结果（commit id、改动文件数），然后**立即停止**
- **不要**自动执行 `git push`
- **不要**执行任何合并/推送到 release 的操作
- 如当前分支上游追踪分支是 `origin/release`，需在输出中提醒用户"避免误推到 release"，但**不要**自己执行推送
