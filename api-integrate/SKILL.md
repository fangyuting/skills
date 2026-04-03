---
name: api-integrate
description: 根据接口信息生成请求函数、TypeScript 类型定义和调用示例
argument-hint: "[接口路径或描述]"
---

根据以下接口信息，生成完整的前端集成代码：**$ARGUMENTS**

请按以下结构生成：

## 1. TypeScript 类型定义

为请求参数和响应数据生成精确的 TS 类型，放在 `types.ts` 中：

```typescript
// 请求参数类型
export interface XxxParams {
  // ...
}

// 响应数据类型
export interface XxxData {
  // ...
}

// 分页响应（如果是列表接口）
export interface XxxPageResult {
  records: XxxData[];
  total: number;
  current: number;
  size: number;
}
```

## 2. 请求函数

放在 `services.ts` 中：

```typescript
import { request } from '@newgrand/udp-ui';
import { XxxParams, XxxData } from './types';

// GET 请求示例
export const getXxxPage = (params: XxxParams) =>
  request.get<XxxData>({ url: '/xxx/page', data: params });

// POST 请求示例
export const saveOrUpdateXxx = (params: XxxParams) =>
  request.body<boolean>({ url: '/xxx/saveOrUpdate', data: params });

// DELETE 示例
export const deleteXxx = (id: string | number) =>
  request.get({ url: '/xxx/delete', data: { id } });
```

## 3. 调用示例

展示在组件中如何调用，并处理响应：

```typescript
const res = await getXxxPage(params);
if (res.code === 200) {
  // 处理数据
}
```

## 注意事项

- 响应结构统一为 `{ code: number, data: T, msg: string }`
- 成功判断用 `res.code === 200`
- 分页参数用 `current`（页码）和 `size`（每页数量）
- 如果接口信息不完整，列出需要补充的字段并给出合理推断
