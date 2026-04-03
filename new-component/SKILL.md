---
name: new-component
description: 按项目规范生成新组件
disable-model-invocation: true
---

用户想创建一个新组件：$ARGUMENTS

请按照项目规范创建组件文件，规范如下：

**技术栈**
- React + TypeScript，使用 `FC` 类型
- 样式使用 Tailwind CSS
- UI 组件使用 antd-mobile
- 路径别名使用 `@/`

**文件结构**
- 通用组件放在 `src/components/<ComponentName>/index.tsx`
- Props 类型定义在组件文件顶部

**代码规范**
- Props 用 `type Props = { ... }` 定义，不用 interface
- 组件默认导出：`export default ComponentName`
- 只接收必要的 props，不过度设计
- 如果组件需要与 antd-mobile Form 配合使用，需支持 `value` / `onChange` 受控模式

**步骤**
1. 确认组件名称、用途和 props
2. 创建组件文件
3. 如果需要，给出使用示例

如果用户没有说明组件用途，先问清楚。
