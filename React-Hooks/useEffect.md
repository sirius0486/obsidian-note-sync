
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

### componentDidUpdate

没有第二个参数代表监听所有的属性更新

```js
useEffect(()=>{console.log('任意属性该改变')}) 
复制代码
```

监听多个属性的变化需要将属性作为数组传入第二个参数。

```js
useEffect(()=>{console.log('n变了')},[n,m]) 
```

  
### componentWillUnmount

```js
useEffect(()=>{ 
	const timer = setTimeout(()=>{ ... },1000) 
	
	return ()=>{
	   console.log('页面销毁了')
	   clearTimerout(timer)
	}
})

```