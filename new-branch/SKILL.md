---
name: new-branch
description: 根据新需求描述，按团队规范创建并推送新开发分支，同时在 README 版本管理章节新增该分支小节
disable-model-invocation: true
---

请按以下步骤为新需求创建规范分支：

## 第一步：收集需求信息

询问我以下信息（如果我已经在命令中提供则直接使用，无需重复询问）：

1. **需求类型**（从下列选项中选择）：
   - `feature` — 新功能 / 需求开发
   - `bugfix` — 测试 Bug / 线上 Bug 修复
   - `hotfix` — 线上紧急修复
   - `optimize` — 性能优化 / 重构
2. **功能描述**：简短英文描述，小写、单词间用连字符 `-` 分隔（如 `user-login`、`pay-error-fix`）
3. **需求概述**（中文）：用于写入 README，简要说明本次需求的背景与目标

## 第二步：生成分支名


按规范拼接分支名：

```
{类型}/{功能描述}
```

- 功能描述小写、单词间用 `-` 分隔

示例：`user-login`

将完整分支名展示给我确认，**等我确认后再执行后续步骤**。

## 第三步：从 release 拉取最新代码并创建分支

依次执行：

```bash
git fetch origin
git switch -c {分支名} --no-track origin/release
```

**必须加 `--no-track`**：新分支只用 `origin/release` 作为起点（基线代码），但**不追踪** release 作为 upstream。否则后续 `git push` 会把代码直接推到 release，污染发布分支。

如果当前有未提交的改动，提示我先处理（stash 或提交），不要强行切换分支。

## 第四步：更新 README.md 版本管理章节

读取 `README.md`，在 `## 版本管理` 章节**末尾**追加新分支的小节：

```markdown
### {需求概述}（{分支名}）
```

示例：

```markdown
### 用户登录功能（zhangsan-user-login）
```

该小节初始内容为空，后续由 `/commit` 负责追加每次提交记录。

将更新后的 README.md 单独提交：

```
docs: 新增 {分支名} 版本管理章节
```

不要添加 Co-Authored-By 行。

## 第五步：首次推送并设置正确的远端 tracking

执行：

```bash
git push -u origin {分支名}
```

`-u` 让当前分支的 upstream 指向 `origin/{分支名}`（和本地同名的远端分支），**覆盖**第三步创建分支时可能留下的任何 release 指向。以后在该分支上 `git push` / `git pull` 都作用于 `origin/{分支名}`，不会误动 release。

## 完成后输出摘要

- 分支名
- 基于 release 分支创建（`--no-track`）
- README 新增小节位置
