`const cachedValue = useMemo(calculateValue, dependencies)`

> 保存返回的结果 就叫做 **缓存**( `memoization`) , 这就是为什么这个 hook 叫做 `useMemo` 


>[!tip] useMemo有以下作用
>1. 跳过昂贵的重新计算   
>2. 跳过组件的重新渲染
>3. 缓存一个函数
>4. 缓存对另一个 hook 的依赖


## useage

使用 memo 通常有三个原因：
1.  ✅ 防止不必要的 effect。
2.  ❗️防止不必要的 re-render。
3.  ❗️防止不必要的重复计算

```js
// 没有使用useMemo, filterTodos函数会在每次 React 组件重新渲染时候重新执行, 尽管结果值没有发生变化, 大多数情况下计算会很快, 但是在昂贵的计算下会造成不必要的性能开销

function TodoList({ todos, tab, theme }) {
  const visibleTodos = filterTodos(todos, tab);
  // ...
}


// 使用 useMemo 包裹, 第一次计算的结果被缓存起来, 第二次渲染时候如果组件没有变化 则跳过这个 filterTodos 函数的执行
import { useMemo } from 'react';

function TodoList({ todos, tab }) {
  const visibleTodos = useMemo(
    () => filterTodos(todos, tab),
    [todos, tab]
  );
  // ...
}

```


bu'que'dang