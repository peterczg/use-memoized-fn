# useMemoizedFn

A React Hook for persistent function references.

[English](./README.md) | [简体中文](./README.zh-CN.md)

## Introduction

`useMemoizedFn` is a custom React Hook for memoizing functions to avoid unnecessary re-renders caused by function reference changes. It's similar to `useCallback`, but provides stronger persistence capabilities, ensuring that the returned function reference remains stable.

## Installation

```bash
npm install use-memoized-fn
# or
yarn add use-memoized-fn
```

## Usage

```tsx
import { useMemoizedFn } from 'use-memoized-fn'

function MyComponent() {
  const [count, setCount] = useState(0)

  // Use useMemoizedFn to memoize the function
  const handleClick = useMemoizedFn(() => {
    setCount(count + 1)
  })

  return <button onClick={handleClick}>Click Me: {count}</button>
}
```

## Features

- The function reference never changes
- Always uses the latest function implementation internally
- Supports function `this` context
- Supports TypeScript with complete type inference

## Comparison with useCallback

`useCallback` requires a dependency array and returns a new function reference when dependencies change. In contrast, `useMemoizedFn` returns a function reference that never changes, while automatically using the latest function implementation internally.

```tsx
// useCallback example - returns a new function reference when dependencies change
const handleClick = useCallback(() => {
  setCount(count + 1)
}, [count]) // Depends on count, function reference changes when count changes

// useMemoizedFn example - function reference never changes
const handleClick = useMemoizedFn(() => {
  setCount(count + 1)
}) // No dependency array needed, function reference never changes
```

## Implementation

`useMemoizedFn` uses `useRef` internally to store the latest function implementation and returns a stable function reference that calls the stored latest function when invoked.

## Acknowledgements and License

The `useMemoizedFn` Hook implementation in this project is based on the same-named Hook from [ahooks](https://github.com/alibaba/hooks). Thanks to the ahooks team for their excellent implementation.

ahooks uses the MIT License, and this project follows the same MIT License.