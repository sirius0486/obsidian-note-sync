`const cachedValue = useMemo(calculateValue, dependencies)`


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


