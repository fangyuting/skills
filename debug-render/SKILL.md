---
name: debug-render
description: 分析 React 组件不必要的重渲染问题，定位原因并给出优化方案
argument-hint: "[组件文件路径或问题描述]"
---

分析以下组件的重渲染问题：**$ARGUMENTS**

## 分析步骤

### 1. 读取组件代码
识别所有可能导致重渲染的模式。

### 2. 常见重渲染原因检查清单

**Props 问题**
- [ ] 父组件每次渲染时创建新的对象/数组字面量作为 props（`{}`、`[]`）
- [ ] 父组件每次渲染时创建新的函数作为 props（`() => ...` 未用 `useCallback`）
- [ ] 传入的 Context 对象包含不相关的字段变化

**State 问题**
- [ ] state 对象整体替换但只需局部更新
- [ ] 多个相关 state 更新触发多次渲染（可合并为一个对象）
- [ ] 用 state 存储可以从其他 state 派生的值

**useEffect 问题**
- [ ] 依赖数组包含对象/函数引用（每次渲染都是新引用）
- [ ] 依赖数组遗漏导致 effect 过早/过晚执行

**组件结构问题**
- [ ] 大组件中局部状态变化导致整体重渲染
- [ ] 列表渲染未用 `React.memo` 包裹列表项

### 3. 输出诊断报告

对每个发现的问题：
```
问题：[描述]
位置：第 X 行，[代码片段]
原因：[为什么这会导致重渲染]
修复：[具体的修复代码]
```

### 4. 优化建议

给出优先级排序的优化方案，从收益最大的开始：

```typescript
// 优化前
const handler = () => doSomething(id);  // 每次渲染新函数引用

// 优化后
const handler = useCallback(() => doSomething(id), [id]);
```

### 5. 验证方法

提供验证重渲染问题已解决的方法：
- 在组件顶部添加 `console.count('XxxComponent render')` 观察渲染次数
- 使用 React DevTools Profiler 录制前后对比
