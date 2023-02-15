
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


## Q&A

### 为什么不能直接在 useEffect 使用 async ?

先来看一个 `错误使用` 的例子 
```jsx
const [state, setState] = useState(0)

useEffect(async () => {
    await setState((state) => state + 1);
}, []);

```

> [!error] 上面例子错误在于 `async` 函数返回一个 `Promise`

- `useEffect` 第一个参数, 也就是 `callback` 函数 , 不应该返回一个 `Promise`
- 它应该 `什么都不返回`  或者 `一个函数`


### 如何在 useEffect 里面调用 异步函数 ?

> [!success] 正确的写法

**在 `useEffect` 内部定义 `async` 函数**
```tsx
 useEffect(() => {
   const fetchData = async()=> {
     const data = await getData()

     return data
   }
   fetchData()
 }, []);

```

**在 `useEffect` 外部定义 `async` 函数**
```tsx
  const [state, setState] = useState(0)

  const fetchData = useCallback(async()=> {
    const data = await getData();
    setState(data)
  }, [])

  useEffect(() => {
    fetchData()
  }, [fetchData]);

```

- 在这种情况下，我们需要将我们的异步函数包裹在 `useCallback` 中，将其与依赖数组进行映射。  
- **注意**--如果我们不使用 `useCallback` 钩子来包装这个函数，它将在每次更新时重新渲染，这将导致 `再次触发 useEffect钩子` 。



## Q & A 


### 为什么不默认 useMemo

> 有这样的计划, React.forget , 会自动给需要加优化的组件加上 useMemo, 但是似乎失败了

1.  `缓存是有成本的`，小的成本可能会累加过高。
2.  默认缓存无法保证足够的正确性。