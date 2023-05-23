## intro

![[WeChatWorkScreenshot_3bf77cdd-315b-4381-8ab6-e46a5bfd7bfd.png]]

fp-ts中一些关键特性和概念包括：

1. 类型安全：fp-ts利用TypeScript丰富的类型系统提供静态类型检查和推断，在编译时捕获可能出现的错误，确保更安全的代码。

2. 函数式数据类型：fp-ts提供像Option（用于处理可选值）、Either（用于处理错误或成功情况）和Task（用于处理异步计算）这样的函数式数据类型，允许开发人员以一种功能性方式处理常见场景。

3. 类型类层次结构：fp-ts引入了受Haskell类型类启发而来的类型类，以便对不同数据类型进行多态操作。类型类提供了定义可以跨多个类型共享通用行为和操作方法。

4. 函数组合器和实用工具：fp-ts提供了丰富的组合器和实用函数来组合和转换函数式代码。这些包括map、chain、pipe、fold、traverse等。

5. 不可变性和纯函数：fp-ts推广不可变性和使用纯函数，它们没有副作用，并始终为给定输入产生相同的输出。这使得代码更加可预测、易于测试并且更容易理解。

总体而言，fp-ts是一个强大的库，将函数式编程概念和技术带到TypeScript中，使开发人员能够编写更模块化、可重复使用且类型安全的代码。


## flow
> flow 指的是 “执行从左到右的函数组合” （performs left-to-right function composition）

flow对传递给它参数的函数有一些限制。第一个函数可以有任意数量的参数，其余函数必须只接受单个参数（即具有一元性）。

```ts
const clean = (s: string): string => s.trim();
const len = (s: string): number => s.length;
const double = (n: number): number => n * 2;

// 如果你需要按顺序调用上面这个函数   clean,len,double， 则你需要这么写
const result = double(len(clean(" some-string ")))

// 如果使用 fp-ts 的 flow ， 则可读性大幅提升, 将三个函数组合成一个函数，
// 它将每个函数的输出作为下一个函数的参数传递。您可以像这样调用它： =>
const cleanThenLenThenDouble = flow( clean, len, double); 
const result = cleanThenLenThenDouble(" some-string ")

```

## pipe
> pipe 指的是 “将表达式的值传递到函数管道中” (pipes the value of an exression into a pipeline of functions )

```ts
const clean = (s: string): string => s.trim();
const len = (s: string): number => s.length;
const double = (n: number): number => n * 2;

//  pipe 和 flow 的区别在于， pipe 将一个值(或表达式， 因为每个表达式都返回一个值) 作为第一个参数， 你可以像这样来调用它 :
const resultWithPipe = pipe(" some-string ", clean, len, double);

//初始值作为参数传递给第一个函数。该函数的输出然后作为下一个函数的参数传递，以相同的方式进行流程控制。


```

需要注意的一点是，传递给管道(pipe)的函数都必须是一元(unary)函数。
哪个更好？应该使用哪个？
flow更加“FP”，但在学习fp-ts时，我们发现pipe更容易理解，但它们执行类似功能并不重要。
在我们的代码中，大多数情况下会使用pipe而不是flow。使用pipe的好处是类型推断按预期工作，这意味着您无需显式添加管道内部函数的参数类型。但这并非总是flow所具备的。

## option
> `null` 和 `undefined` 是运行时错误的主要原因,  在 `fp-ts`  中我们使用 option 代替 null 和 undefined， 因为使用 `null` 会让人感到模糊不清 ， 到底是 “没有值” 还是 “空值” 


```ts

type Option<A> = None | Some<A>;

interface None {
	readonly _tag: "None";
}

interface Some<A> {
	readonly _tag: "Some";
	readonly value: A;
}

```

Option是一个“容器”，用于存储类型A的可选值。
- 如果存在类型A的值，则 `Option` 将是 `Some<A>` 的实例。
- 如果不存在类型A的值，则`Option`将是`None`的实例，但始终会有一个Option实例存在 - 这意味着我们不需要处理它为`null`或`undefined`。

另一种思考这个工作原理的方法是将其视为大小为0或1的数组。您总是会有一个数组，但有时它不包含任何值。

fp-ts中所有类型都是纯数据类型，而不是类，因此fp-ts提供了函数来帮助我们创建和操作这些实例。对于Option，您可以按如下方式导入这些函数：

```ts
import * as 0 frin "fp-ts/Option";

O.some(value: A) => Option<A>  // always a Some<A>
O.none => Option<A>   // always a None

O.fromPredicate(f: (value: A) => boolean) => (a: A) => Option<A>  // returns Some<A> if f returns true, None otherwise
O.fromNullable(value: A) => Option<A> // None if value is null or undefined, Some<A> otherwise

```

你可能会认为只是将 null 检查 替换成了 None 检查， 确实是这样的， 但也不完全是这样

`const map = <A, b>(f: (a: A) => B) => (opt： Option) => Option`

如果 opt 是 Some，则 map 将从 Some 中取出该值，将其分配给 a，然后运行给定的函数 f(a)，并返回一个新的 Some 与结果。 如果 opt 是 None，则 map 只返回 None，因为没有“value”可以应用于 f。 这意味着我们不需要检查 opt 是否是 Some 或 None，因为 map 已经替我们完成了这个任务。

```ts
const some = O.some(2);
const none = O.none;
const doubledSomeOption = O.map((n: number) => n * 2)(some);  // Some(4)
const doubleNoneOption = O.map( (n: number) => n * 2)(none);  // None

const double = (n: number): number => n * 2;
const doubleOption = O.map(double)(some); // Some(4)

const doubleOptionPipe = pipe(
	some,
	O.map(double)
); // Some(4)
```

## flatten

## chain

## getOrElse

## fold

## toNullable, toUndefined

## Either

### map

### mapLeft



## Links

https://www.rea-group.com/about-us/news-and-insights/blog/introduction-to-fp-ts-part-1/

https://web.microsoftstream.com/video/9813a6bc-3d5a-4295-950d-5caca073cc99?list=studio