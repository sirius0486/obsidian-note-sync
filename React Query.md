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

	fetch('http://www.xxx.xxxx')
		.then( res => res.json() )
		.then( setData() )
		.catch( setError)
		.fianlly(  () => setIsLoading(false) );
})
```

## hooks

### useQuery
1.  `queryKey`
2.  `queryFn`
3. `refetchInterval`
4. `enabled` 


```tsx
import { useQuery } from "@tanstack/react-query"
import { getPost } from "./api/posts"
import { getUser } from "./api/users"

export default function Post({ id }) {
	const postQuery = useQuery({
	queryKey: ["posts", id],
	queryFn: () => getPost(id),

})

const userQuery = useQuery({
	queryKey: ["users", postQuery?.data?.userId],
	enabled: postQuery?.data?.userId != null,
	queryFn: () => getUser(postQuery.data.userId),
})

  

if (postQuery.status === "loading") return <h1>Loading...</h1>

if (postQuery.status === "error") {
	return <h1>{JSON.stringify(postQuery.error)}</h1>
}

return (
    <>
      <h1>
        {postQuery.data.title} <br />
        <small>
          {userQuery.isLoading
            ? "Loading User..."
            : userQuery.isError
            ? "Error Loading User"
            : userQuery.data.name}
        </small>
      </h1>
      <p>{postQuery.data.body}</p>
    </>
  )
} 
```

### useMutation

```jsx
 
```