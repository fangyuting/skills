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

先执行以下命令获取当前日期和 git 用户名：

```bash
date +%y%m%d
git config user.name
```

按规范拼接分支名：

```
{类型}/{日期}/{作者}-{功能描述}
```

- 日期格式：`YYMMDD`（如 `260403`）
- 作者取 git user.name，转小写
- 功能描述小写、单词间用 `-` 分隔

示例：`feature/260403/zhangsan-user-login`

将完整分支名展示给我确认，**等我确认后再执行后续步骤**。

## 第三步：从 release 拉取最新代码并创建分支

依次执行：

```bash
git checkout release
git pull origin release
git checkout -b {分支名}
git push -u origin {分支名}
```

如果当前有未提交的改动，提示我先处理（stash 或提交），不要强行切换分支。

## 第四步：更新 README.md 版本管理章节

读取 `README.md`，在 `## 版本管理` 章节**末尾**追加新分支的小节：

```markdown
### {需求概述}（{分支名}）
```

示例：

```markdown
### 用户登录功能（feature/260403/zhangsan-user-login）
```

该小节初始内容为空，后续由 `/version-commit` 负责追加每次提交记录。

将更新后的 README.md 单独提交：

```
docs: 新增 {分支名} 版本管理章节
```

不要添加 Co-Authored-By 行。

## 完成后输出摘要

- 分支名
- 基于 release 分支创建
- README 新增小节位置
