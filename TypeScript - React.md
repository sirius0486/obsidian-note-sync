
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

## interface

> 接口定义`对象的形状`, 和类型别名很相似, 但仅用于对象类型

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

>[!tip] 拓展接口其实是创建一个新的接口, 只不过实在原来的接口上增加新的属性或方法

```ts
interface Rectangle {
	height: number,
	width: number,
}

interface ColorRectangle extends Rectangle {
	color: string
}

const colorRectangle : ColorRectangle = {
	height: 100,
	width: 100,
	color: 'red'
}
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

## union type
> 联合类型, 如果一个值有多种类型, 则可以使用联合类型

```ts
const printStatusCode (code: number | string ) {
	console.log(`My status code is ${code}.`)
}
printStatusCode(404);
printStatusCode('404');
```

> 调用值为联合类型的方法时 , 只能调用公有的方法, 否则会报错

```ts
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code.toUpperCase()}.`) // error: Property 'toUpperCase' does not exist ontype 'string | number'.
  Property 'toUpperCase' does not exist on type 'number'
}

// toUpperCase 只存在于 string 类型, number 类型没有

```

### Casting

>  Casting is the process of overriding a type.
> 有的时候我们需要转换类型,  casting 就是重写一个类型的过程

转换类型我们有 3 种 方法: 
1. 通过 ` as `
2. 通过 ` <> `
3. 强制类型转换 Force casting


```ts
// casting with  as  
let x: unknown = 'hello';
console.log((x as string).length);

// casting with <>
let x: unknown = 'hello';  
console.log((<string>x).length);

// warning!!! <. 在 tsx 中是不起作用的


// force casting
let x = 'hello';

console.log(((x as unknown) as number).length); // x is not actually a number so this will return undefined

```

## generics

> 泛型允许创建 "类型变量"，可以用来创建类、函数和类型别名，不需要明确定义它们使用的类型。 泛型可以提高保证类型安全的同时提高函数的复用性

```ts

function createPair<S, T>(v1: S, v2: T): [S, T] {  
  return [v1, v2];  
}  
console.log(createPair<string, number>('hello', 42)); // ['hello', 42]



function createLoggedPair<S extends string | number, T extends string | number>(v1: S, v2: T): [S, T] {  
  console.log(`creating pair: v1='${v1}', v2='${v2}'`);  
  return [v1, v2];  
}

```

## Partial
`Partial` changes all the properties in an object to be optional.
Partial 可以使得一个对象里的所有属性变为可选属性

```ts
interface Point {
	x: number,
	y: number,
}

// `Partial` 使得  x 和 y 变为可选属性
let pointPart: Partial<Point> = {}; 
pointPart.x = 10;

```

## Record
> Record 可以简单地定义一个对象类型

```ts
// Record<string, number>等同于 { [key: string]: number }

const nameAgeMap: Record<string, number> = {
  'Alice': 21,
  'Bob': 25
};
```

## tsx
得益于 `React` 的广泛使用度 , `TypeScript` 也支持  `jsx` , 所以也有 `typeScript` 版的 jsx

## react hooks in typescirpt

### useState
```tsx
// 基本类型
 const [counter, setCounter] = useState<number>(0)

// 引用类型
 // type UserInfo =  string:[]
 interface UserInfo  {
	 name: string,
	 age: number
 }

const [userInfo, setUserInfo] = useState<UserInfo>(['汤姆'])

```

### useMemo
```tsx
const memoizeValue = useMemo<string> ( () => {
	computeExpressValue(a,b)
	
}, [a , b] )
```
### useCallback
```tsx
type CallbackType = (...args: string[]) => void

const memoizedCallback = React.useCallback<CallbackType>(() => {
    doSomething(a, b);
  }, [a, b]);
```
### useRef
```tsx
import React from "react";

export const App: React.FC = () => {
  const myRef = useRef<HTMLElement | null>(null)

  return (
    <main className="App" ref={myRef}>
      <h1>My title</h1>
    </main>
  );

```
### useReducer
```tsx
import * as React from "react";

enum ActionType {
  INCREMENT_COUNTER = "INCREMENT_COUNTER",
  DECREMENT_COUNTER = "DECREMENT_COUNTER"
}

interface IReducer {
  type: ActionType;
  count: number;
}

interface ICounter {
  result: number;
}

const initialState: ICounter = {
  result: 0
};

const countValue: number = 1;

const reducer: React.Reducer<ICounter, IReducer> = (state, action) => {
  switch (action.type) {
    case ActionType.INCREMENT_COUNTER:
      return { result: state.result + action.count };
    case ActionType.DECREMENT_COUNTER:
      return { result: state.result - action.count };
    default:
      return state;
  }
};

export default function App() {
  const [state, dispatch] = React.useReducer<React.Reducer<ICounter, IReducer>>(
    reducer,
    initialState
  );

  return (
    <div className="App">
      <h1>Result: {state.result}</h1>
      <button
        onClick={() =>
          dispatch({ type: ActionType.INCREMENT_COUNTER, count: countValue })
        }> +
      </button>
      <button
        onClick={() =>
          dispatch({ type: ActionType.DECREMENT_COUNTER, count: countValue })
        }> -
      </button>
    </div>
  );
}
```


## React.FC

>[!error] 错误的写法 !


```tsx
function RoundButton(): React.FC {
	return <div>"hello world"</div>;
}
```

>[!tip] 正确的写法

```tsx
const RoundButton: React.FC = () => {
  return <div>"hello world"</div>;
}
```

在第一种情况下，你说的是函数返回什么，但在第二种情况下，你说的是函数是什么。

第二种情况是正确的。`React.FC` 是一个函数类型。你的第二个块说你的函数是 `React.FC`，这意味着它接受 `props`



## 泛型 generics

> 泛型可以看做是**类型变量** , 变量可以有不同的值, 泛型可以有不同的类型

为什么需要泛型 ?  因为在很多情况下, 我们希望一个函数的类型是动态的, 就是函数返回与其实参相同的类型

React 中 TSX 使用 **箭头函数** 和 **泛型** 识别有问题


```ts
// a JavaScript object
const user = {
  name: 'John',
  status: 'online',
};

// and its TypeScript type
type User = {
  name: string;
  status: string;
};


// 可以看到 JavaScript 关心的是变量的值

// TypeScript 关心的是变量的类型
```

`<>`  的语法最开始会比较奇怪, 但很快就可以适应

```ts
// generic type definition
type User<StatusOptions> = {
  name: string;
  status: StatusOptions;
};

// 在这里 
StatusOptions is called a "type variable" and User is said to be a "generic type".

StatusOptions 在这里被叫做 类型变量  ,  User 是 泛型

```


### 泛型的使用

```ts
function loggingIdentity<Type>(arg: Type): Type {
 
	console.log(arg.length);
	//Property 'length' does not exist on type 'Type'.
  
  return arg;
}

在这里 打印 arg.length 会报错,  因为 Type 可以代表任何类型, 如果使用该函数却传入一个 number 类型, 那么就会报错, number 并没有 .length 这个属性


我们实际上是想让这个函数在Type的数组上工作，而不是直接在Type上工作。既然我们在处理数组，那么.length成员应该是可用的。我们可以像创建其他类型的数组那样来描述它。

function loggingIdentity<Type>(arg: Type[] ): Type[] {

	console.log( arg.length )
	return arg;
}

你可以把loggingIdentity的类型理解为 "通用函数loggingIdentity接收一个类型参数Type和一个参数arg，参数arg是一个Type数组，并返回一个Type数组。"如果我们传入一个数字数组，我们会得到一个数字数组，因为Type会绑定到数字。这允许我们使用我们的通用类型变量Type作为我们正在处理的类型的一部分，而不是整个类型，给我们更大的灵活性。

function loggingIdentity<Type>(arg: Array<Type>): Array<Type> {
  
  console.log(arg.length); 
  // Array has a .length, so no more error
  
  return arg;
}

```

### 泛型接口

```ts
// example 1

interface IProcessor<T> { 
    result:T;
    process(a: T, b: T) => T;
}

// example 2
interface KeyPair<T, U> {
    key: T;
    value: U;
}

let kv1: KeyPair<number, string> = { key:1, value:"Steve" }; // OK
let kv2: KeyPair<number, number> = { key:1, value:12345 }; // OK


// example 3
const GenericList = <T extends unknown> ({
	data,
	renderItem.
	keyExtractor
}: Props<T>) => {
	return (
		<div>
			{data.map((item) => (
				<div key={keyExtractor(item)} className="item" >
					{renderItem(item)}
				</div >
			))}
		</div>
	);
};

export default GenericList;
```


### 泛型约束

```ts
在我们的loggingIdentity例子中，我们希望能够访问arg的.length属性，但是编译器无法证明每个类型都有一个.length属性，所以它警告我们不能做这个假设

function loggingIdentity<T> (arg:T) : T {

	console.log(arg.length);
	//Property 'length' does not exist on type 'Type'.
  return arg;
}

我们希望限制这个函数与任何和所有类型一起工作，而不是与任何和所有同时具有.length属性的类型一起工作。只要这个类型有这个成员，我们就允许它，但它必须至少有这个成员。要做到这一点，我们必须把我们的要求作为一个约束条件列在Type可以是什么。

我们将创建一个接口来描述我们的约束条件。在这里，我们将创建一个接口，它有一个单一的.length属性，然后我们将使用这个接口和extends关键字来表示我们的约束条件

interface Lengthwise {
	length: number;
}

function loggingIdentity<Type extend Lengthwise>(arg: Type): Type {
	  
	  console.log(arg.length); 
	  // Now we know it has a .length property, so no more error
	  return arg;
}

现在泛型函数被限制了, 所以它将不在对任何和所有的类型起作用

loggingIdentity(3);

Argument of type 'number' is not assignable to parameter of type 'Lengthwise'.
类型为'number'的参数不能赋值给类型为'Lengthwise'的参数。

Instead, we need to pass in values whose type has all the required properties:
相反，我们需要传入其类型具有所有所需属性的值。

loggingIdentity({ length: 10, value: 3 });

```


在通用约束条件中使用类型参数


```ts
function getProperty<Type, Key extends keyof Type>(obj: Type, key: Key) {
  return obj[key];
}
 
let x = { a: 1, b: 2, c: 3, d: 4 };
 
getProperty(x, "a");
getProperty(x, "m");  // error !

Argument of type '"m"' is not assignable to parameter of type '"a" | "b" | "c" | "d"'.

类型为 "m "的参数不能分配给类型为 "a"|"b"|"c"|"d "的参数。

```
