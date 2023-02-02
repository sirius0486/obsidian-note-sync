```tsx
const refContainer = useRef(initalValue)
```

useRef 函数接收一个初始值，并返回一个**可变的（mutable）** ref 对象，也就是我们的变量`refContainer`。这个对象上面会存在一个属性——`current`，它的默认值就是`initalValue`。这里有个比较重要的点就是useRef 创建返回的对象是可变的，并且它会在组件的整个生命周期中都存在，这也就以为着无论你在何时何地访问这个对象，它的值永远都是最新的值。

> useState 创建出来的值是不可变的（immutable），每一次 render 都是新的值，而 useRef 创建出来的对象始终都是最开始的那个对象，其属性 `current`可以被赋值。

  
