## usage

```jsx
const [ ①state , ②dispatch ] = useState(③initData)
```


1. state，目的提供给 UI ，作为渲染视图的数据源。
2. dispatchAction 改变 state 的函数，可以理解为推动函数组件渲染的渲染函数。
3.  initData 有两种情况，
	- 第一种情况是非函数，将作为 state 初始化的值。
	- 第二种情况是函数，函数的返回值作为 useState 初始化的值。

## example
```jsx
const [ number, setNumber ] = useState(1);

useEffect( ()=> {
	console.log(number); // 1
	changeNumber = async () => {
		await setNumber(10);
	}
	console.log(number); // 10
},[])

```


## Q&A

### useState为何选择数组解构而非对象解构

- 数组解构根据 index , 可以改名, 更加灵活
- 对象解构根据 key 的名称 , 需要根据 键名解构出来 
- 可知, 选择数组解构的原因是为了更好的`开发体验` (DX)

### setState 是同步还是异步 ?

> [!success] setState是异步的
> setState是一个异步方法，但在之前 `setState` 有时是同步更新的，而有时却是异步更新 , 这是因为在`setTimeout/setInterval`等定时器里逃脱了React对它的掌控，变成了同步方法

- 在 react 18 版本中修复了这个 问题,  `setState` 总是异步的
- ReactJs以异步方式设置其状态，因为这可能导致昂贵的操作。如果是同步的，可能会让浏览器没有反应。异步的 `setState` 调用是分批进行的，React使用的是合并更新, 以提供更好的用户体验和性能。

### setState在什么情况下表现为同步?

> [!info] 把 `setState` 放在 `定时器` 里就会同步更新。放在 `自定义事件函数` 里也会同步更新
> 这个问题已在` React 18 `被修复, `setState` 总是异步的 !!!

```jsx

// 这是一个 setState 同步执行的例子

clickUpdateCount () {
    this.setState({
      count: this.state.count + 1
    });
}
handleClick () {
    setTimeout(() => {
        this.clickUpdateCount();
        // 打印结果与 count 一致
        console.log(this.state.count);
    },0);
}

```

### 为什么不能在 setState 使用 async/ await ?

> The setState function also does not return a Promise. Using async/await or anything similar will not work.

- `setState` 函数不会返回一个 `Promise`  , 所以使用 `async / await `等类似手段并不会起作用