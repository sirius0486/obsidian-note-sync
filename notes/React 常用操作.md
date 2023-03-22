## 链接
1. 官方文档（EN）： [https://react.dev/](https://react.dev/)
1. 官方文档（ZH）： [https://react.jscn.org/](https://react.jscn.org/)
3. MDN： https://developer.mozilla.org/zh-CN/
4. 现代 JavaScript 教程: https://zh.javascript.info/

## Hooks中 useEffect 模拟生命周期
```tsx
// 模拟 componentDidMount 
useEffect(() => {
      // Your Code ...
      // 函数会在页面挂载后调用
  }, [ ] );
  
// 模拟 componentDidUpdate 
useEffect(() => {
      // Your Code ...
      // 函数会在每次渲染后调用
 });
  
// 模拟 componentWillUnmount
useEffect( ( ) => {
  return ( ) => {
    console.log('will unmount');
    //函数会在组件卸载前被调用
  }
}, [ ] );
```

### 条件判断
```tsx
function Item({ name, isPacked }) {
  return (
    <li className="item">
      {isPacked ? (
        <del>
          {name + ' ✔'}
        </del>
      ) : (
        name
      )}
    </li>
  );
}
```
### 渲染列表
```tsx
 const listItems = people.map(person =>
    <li>{person}</li>
  );
  return <ul>{listItems}</ul>;
```

### 发起Get请求
```tsx
useEffect(() => {
    axios.get(baseURL).then((response) => {
      setPost(response.data);
    });
  }, []);
```


### 发起Post请求
```tsx
   axios
      .post(baseURL, {
        title: "Hello World!",
        body: "This is a new post."
      })
      .then((response) => {
        setPost(response.data);
      });
  }
  ```