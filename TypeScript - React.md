
## jsx


## tsx

### react hooks in typescirpt

### useState
### useEffect
### useMemo
### useCallback
### useRef
### useReducer

## tuples
> 元组其实就是一个数组, 但元组运行数不同元素有不同的类型


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

> 如果某种类型经常使用, 可以给该类型起个别名 , 这就是类型别名

```ts
type myType = {
  memberOne: string;
  memberTwo: number;
}

let favoriteNum: myType = {"my favorite number is ", 42}
```


### 接口和类型别名的区别

1. 有两种方法去定义一个对象的形状: 接口 `interface` 和 类型别名 `type aliases`

 > 它们非常相似, 并且在大多数情况下是相同的


但是在某些情况下, 还是有略微区别

