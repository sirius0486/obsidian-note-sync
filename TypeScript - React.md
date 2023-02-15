
## tuples
> 元组其实就是一个数组, 但元组运行数不同元素有不同的类型

要定义一个元组，要指定数组中每个元素的类型
```ts
// define our tuple
let ourTuple: [number, boolean, string];

// initialize correctly  
ourTuple = [5, false, 'Coding God was here'];
```


### object 类型
```ts
Interface Iaddress  {
	streetId: 23
	Road: 23
}

const userInfo : { name:string, age:number, address:Iaddress } = {

}

```

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


但两者在某些情况下有区别
1. 接口使用继承，类型别名则使用交集

比如拓展类型上, `inerface` 通过 `extend` 关键字拓展 , type 通过 & 符号拓展

```ts
// 定义一个类型为动物，字段为名字
    interface Animal {
        name:string
    }
    // 定义一个类型猴子，字段为吃香蕉
    // 且继承动物类型
    interface Monkey extends Animal {
        eatBanana:boolean
    }

    let m : Monkey = {
        name:'吉吉国王',
        eatBanana:true
    }
//这样在 Monkey 类型中也有了name字段
```

而在 **type** 中，我们需要通过 & 符号来扩展我们的字段

```ts
 // 定义一个类型为动物，字[[英语单词- develop]]段为名字
    type Animal = {
        name:string
    }
     // 定义一个类型猴子，字段为吃香蕉
    //  并用 & 进行扩展
    type Monkey = {
        eatBanana:boolean
    } & Animal

    let m : Monkey = {
        name:'吉吉国王',
        eatBanana:true
    }
```

interface 只可以定义对象类型, 类型别名除了定义对象类型外 还可以



## jsx


## tsx

### react hooks in typescirpt

### useState
```tsx

```

### useEffect
```tsx

```
### useMemo
```tsx

```
### useCallback
```tsx

```
### useRef
```tsx

```
### useReducer
```tsx

```
