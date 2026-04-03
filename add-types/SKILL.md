---
name: add-types
description: 为 JS 文件或弱类型的 TypeScript 代码补全类型定义，消除 any
argument-hint: "[文件路径]"
---

为以下文件补全 TypeScript 类型：**$ARGUMENTS**

## 工作流程

### 1. 读取文件
分析现有代码，找出所有类型缺失或不精确的地方：
- 函数参数类型
- 返回值类型
- 组件 Props 接口
- State 类型
- API 响应类型
- 事件处理器类型

### 2. 推断类型
根据以下线索推断类型：
- 变量的使用方式（访问哪些字段）
- 函数调用传入的实参
- 条件判断中的类型守卫
- 注释和变量命名

### 3. 生成类型定义
优先顺序：
1. 精确的接口/类型（最优）
2. 联合类型（次优）
3. 泛型约束
4. `unknown` + 类型断言（比 `any` 更安全）
5. `any`（最后手段，需加注释说明原因）

### 4. 放置位置
- 组件私有类型：放在文件顶部
- 共享类型：放在 `types.ts`
- API 响应类型：放在 `services.ts` 或 `types.ts`

## 常用类型模板

```typescript
// React 组件 Props
interface XxxProps {
  id: string | number;
  data?: XxxData;
  onSuccess?: (result: XxxData) => void;
  children?: React.ReactNode;
}

// 分页请求参数
interface PageParams {
  current: number;
  size: number;
  [key: string]: unknown;
}

// 统一响应结构
interface ApiResponse<T> {
  code: number;
  data: T;
  msg: string;
}
```

修改后确保 `tsc --noEmit` 不报错。
