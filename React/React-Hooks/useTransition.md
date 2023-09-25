- 比如一个需求是 根据输入框内容搜索对应图片, 使用 `useTransition` 可以给事件分出不同优先级
- 输入框立即更新输入的内容是 **高优先级**
- 根据输入内容返回对应图片是 **低优先级**

```jsx
function App() {
  const [name, setName] = useState("")
  const [list, setList] = useState(largeList)
  const [isPending, startTransition] = useTransition()

  function handleChange(e) {
    setName(e.target.value)
    startTransition(() => {
      setList(largeList.filter(item => item.name.includes(e.target.value)))
    })
  }

  return <>
    <input type="text" value={name} onChange={handleChange} />
    {isPending ? (
      <div>Loading...</div>
    ) : (
      list.map(item => <ListComponent key={item.id} item={item} />)
    )}
  </>
}
```