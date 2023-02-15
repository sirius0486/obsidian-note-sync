
## JSX



## interface
> 定义接口的形状

```ts
interface IUser {
  name: string,
  age: number,
}


function createUser(user: IUser) {
  console.log(user.name);
}
 
const tom = { name: 'Tom jerry', age: "21" };
createUser(tom);
```

## type aliases

1. 有两种方法去定义一个对象的形状: 接口 `interface` 和 类型别名 `type aliases`
1. 它们非常相似, 并且在大多数情况下是相同的