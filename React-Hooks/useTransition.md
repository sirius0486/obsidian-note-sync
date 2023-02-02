- 比如一

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