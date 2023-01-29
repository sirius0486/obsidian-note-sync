## Hooks中 useEffect 模拟生命周期
```js
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
  
//模拟 componentWillUnmount
useEffect( ( ) => {
  return ( ) => {
    console.log('will unmount');
    //函数会在组件卸载前被调用
  }
}, [ ] );
```

## 链接
官方文档（beta）： https://beta.reactjs.org/
官方文档（beta）：https://www.freecodecamp.org/chinese/news/how-to-use-axios-with-react/
MDN：https://developer.mozilla.org/zh-CN/
现代 JavaScript 教程: https://zh.javascript.info/

### 条件判断
```js
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
```js
 const listItems = people.map(person =>
    <li>{person}</li>
  );
  return <ul>{listItems}</ul>;
```

### 发起Get请求
```js
useEffect(() => {
    axios.get(baseURL).then((response) => {
      setPost(response.data);
    });
  }, []);
```


### 发起Post请求
```js
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