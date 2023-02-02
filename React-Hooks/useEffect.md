
## usage

```jsx
useEffect( cb, [dep] )

// cb 回调函数    [dep] 依赖项数组
```



## 模拟生命周期

### componentDidMount
```js
useEffect( () => {
	console.log('页面挂载时调用');
}, [])


// 第二个参数是空数组, 只会在页面挂载的时候执行, 执行次数 1 
```

### component