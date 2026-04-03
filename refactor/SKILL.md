---
name: refactor
description: 重构指定文件或代码，提取重复逻辑、简化复杂度、改善可维护性
argument-hint: "[文件路径或重构目标描述]"
---

对以下代码进行重构：**$ARGUMENTS**

## 重构原则

- **最小改动**：只重构有明确收益的部分，不引入不必要的抽象
- **行为不变**：重构后功能与原来完全一致
- **可读性优先**：代码应更易理解，而不是更"聪明"

## 重构步骤

### 1. 分析现状
先读取文件，识别以下问题：
- 重复代码（DRY 原则违反）
- 过长的函数（超过 50 行考虑拆分）
- 复杂的条件嵌套
- 可以用 Hook 提取的状态逻辑
- 可以用配置替代 switch/if-else 的枚举映射

### 2. 制定重构计划
列出要做的改动，并说明理由。等用户确认后再执行（如果改动较大）。

### 3. 执行重构
按计划修改代码，每次只做一种类型的重构：
- 提取函数/Hook
- 简化条件
- 消除重复
- 改善命名

### 4. 验证
- 确认导出的接口没有变化
- 确认 props 类型没有变化
- 检查是否引入了新的依赖

## 常见重构模式

```typescript
// 枚举映射替代 switch
const STATUS_MAP = {
  [StatusEnum.ACTIVE]: '启用',
  [StatusEnum.INACTIVE]: '禁用',
} as const;

// 提取列表操作为 Hook
const useXxxList = () => {
  const [data, setData] = useState([]);
  const refresh = useCallback(() => { ... }, []);
  return { data, refresh };
};
```
