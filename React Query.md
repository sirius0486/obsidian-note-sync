> [!info] > React Query是一个 集 `api 缓存`  、插入数据自动刷新、分页和无限滚动、loading 等一体的 增强查询库

- 多个页面使用同一查询 api ,  切换页面不会不会重新请求该 api

## usage

```tsx

const postQuery = useQuery({
	queryKey: ["posts"],
	queryFn: getPosts,
})


// 传统写法
useEffect( () => {
	setIsLoading(true);

	fetch('http://www.xxx.x')
})
```

## hooks

### useQuery
1.  `queryKey`
2.  `queryFn`
3. `refetchInterval`
4. `enabled` 


```tsx

```

### useMutation

```jsx
 
```