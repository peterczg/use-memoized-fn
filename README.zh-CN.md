# useMemoizedFn

一个用于持久化函数引用的 React Hook。

[English](./README.md) | [简体中文](./README.zh-CN.md)

## 介绍

`useMemoizedFn` 是一个自定义 React Hook，用于记忆化函数，以避免因函数引用变化导致的不必要重渲染。它类似于 `useCallback`，但提供了更强大的持久化能力，确保返回的函数引用始终保持稳定。

## 安装

```bash
npm install use-memoized-fn
# 或
yarn add use-memoized-fn
```

## 使用方法

```tsx
import { useMemoizedFn } from 'use-memoized-fn'

function MyComponent() {
  const [count, setCount] = useState(0)

  // 使用 useMemoizedFn 记忆化函数
  const handleClick = useMemoizedFn(() => {
    setCount(count + 1)
  })

  return <button onClick={handleClick}>Click Me: {count}</button>
}
```

## 特性

- 返回的函数引用永远不会变化
- 内部总是使用最新的函数实现
- 支持函数的 `this` 上下文
- 支持 TypeScript，提供完整的类型推断

## 与 useCallback 的区别

`useCallback` 需要传入依赖数组，当依赖变化时会返回新的函数引用。而 `useMemoizedFn` 返回的函数引用永远保持不变，同时内部逻辑会自动使用最新的函数实现。

```tsx
// useCallback 示例 - 依赖变化时返回新的函数引用
const handleClick = useCallback(() => {
  setCount(count + 1)
}, [count]) // 依赖 count，count 变化时函数引用改变

// useMemoizedFn 示例 - 函数引用永远不变
const handleClick = useMemoizedFn(() => {
  setCount(count + 1)
}) // 不需要依赖数组，函数引用永远不变
```

## 实现原理

`useMemoizedFn` 内部使用 `useRef` 存储最新的函数实现，并返回一个不变的函数引用，该函数在调用时会调用存储的最新函数实现。

## 致谢与许可证

本项目的 `useMemoizedFn` Hook 实现基于 [ahooks](https://github.com/alibaba/hooks) 中的同名 Hook。感谢 ahooks 团队提供的优秀实现。

ahooks 使用 MIT 许可证，本项目同样遵循 MIT 许可证。