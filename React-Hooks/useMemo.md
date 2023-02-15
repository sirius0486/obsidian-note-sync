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

```jsx
import { useMemo } from 'react';

function TodoList({ todos, tab }) {
  const visibleTodos = useMemo(
    () => filterTodos(todos, tab),
    [todos, tab]
  );
  // ...
}
```
