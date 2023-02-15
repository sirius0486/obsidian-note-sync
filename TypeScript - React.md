
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

## Optional Properties 
> 有些参数和属性是可选的, 则可以在后面加 ?

```ts
const car: { type: string, mileage?: number } = { // no error  
  type: "Toyota"  
};  
car.mileage = 2000;
```

## index signture
> 索引签名可用于没有定义属性列表的对象。

```ts
const nameAgeMap: { [index: string]: number } = {};
nameAgeMap.Jack = 25; // no error
nameAgeMap.Mark = "Fifty"; // Error: Type 'string' is not assignable to type 'number'.
```

> ts 中索引签名有 2 种 
1. 字符串索引
2. 数字索引
```ts

// 字符串索引


// 数字索引

```

## enum 
> 枚举类型 是一个特殊的类, 代表一组常量(不可变)
> 枚举类型只有 2 种类型,  number 和 string


```ts
// 不赋值的话 第一项从 0 开始 每项递增
// 相应的就是 数值类型
enum numberEnum {
	one,
	two,
	three
}

// 等价于
enum numberEnum {
	one = 0,
	two = 1,
	three = 2
}

// 这是一个 字符串类型 的 枚举类型
enum myEnum {
	myFirstConst = "first",
	mySecondConst = "second"
};
```

## type aliases

> 如果某种类型经常使用, 可以给该类型起个别名 , 这就是类型别名

```ts
type myType = {
  memberOne: string;
  memberTwo: number;
}

let favoriteNum: myType = {"my favorite number is ", 42}


// 也可以套娃
type CarYear = number  
type CarType = string  
type CarModel = string  
type Car = {  
  year: CarYear,  
  type: CarType,  
  model: CarModel  
}  
  
const carYear: CarYear = 2023 
const carType: CarType = "Toyota"  
const carModel: CarModel = "Corolla"  
const car: Car = {  
  year: carYear,  
  type: carType,  
  model: carModel  
};

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

```jsx
```

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
