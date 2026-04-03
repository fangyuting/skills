---
name: new-page
description: 按项目规范生成新页面
disable-model-invocation: true
---

用户想创建一个新页面：$ARGUMENTS

请按照项目规范创建页面文件，规范如下：

**技术栈**
- React + TypeScript，使用 `FC` 类型
- 样式使用 Tailwind CSS
- UI 组件使用 antd-mobile
- 数据请求使用 ahooks 的 `useRequest`
- 路由使用 react-router-dom 的 `useNavigate` / `useParams`

**文件结构**
- 页面放在 `src/pages/<PageName>/index.tsx`
- 如需子组件，放在同目录下

**代码模板规范**
- 有数据请求时，加载中显示 `<Loading />` 组件（`import Loading from '@/components/Loading'`）
- 错误/空状态使用 antd-mobile 的 `ErrorBlock`
- 页面底部操作栏用 `sticky bottom-0` 固定，加 `<SafeArea position="bottom" />`
- 路径别名使用 `@/`

**步骤**
1. 确认页面名称和主要功能
2. 创建 `src/pages/<PageName>/index.tsx`
3. 询问是否需要在路由配置中注册（`src/router` 或类似位置）

如果用户没有说明页面功能，先问清楚页面要做什么。
