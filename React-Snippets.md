
## Fragments

```tsx
// React Fragments
// 适合有多个平行元素的情况
// (JSX 只允许一个根元素)

import React from 'react'

function Example() {
	return (
		<>
			<h1>Hello, World! </h1>
			<p>This is a paragraph</p>
		</>
	)
}
```


## useEffect 执行副作用

```jsx
// React useEffect 执行副作用
function Example() {
  const [data, setData] = useState<string[]>([]);

  useEffect(() => {
    fetchData();
  }, []);

  const fetchData = async () => {
    const response = await fetch("api/data");
    const result = await response.json();
    setData(result);
  };

  return <div>{data ? `Data: ${JSON.stringify(data)}` : `Loading...`}</div>;
}

```


## React 子组件修改父组件状态 (传递函数 prop)

```jsx
function Parent() {
	const [count, setCount] = useState(0);

}
```