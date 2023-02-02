```jsx
const [ ①state , ②dispatch ] = useState(③initData)
```

1. state，目的提供给 UI ，作为渲染视图的数据源。
2. dispatchAction 改变 state 的函数，可以理解为推动函数组件渲染的渲染函数。
3.  initData 有两种情况，
	- 第一种情况是非函数，将作为 state 初始化的值。
	- 第二种情况是函数，函数的返回值作为 useState 初始化的值。

