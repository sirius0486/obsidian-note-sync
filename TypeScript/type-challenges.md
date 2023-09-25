
## Advances Type

### DeepPartial

使得对象所有属性及其嵌套属性可选

```ts
type DeepPartial<T> = {
	[p in keyof T] ?: T[P] extends object ? DeepPartial<T[P]> : T[P];
}
```

使用该类型
```ts
interface User {
  name: string;
  address: {
    street: string;
    city: string;
  };
}

type DeepPartialUser = DeepPartial<User>;

// The DeepPartialUser type is equivalent to:
interface PartialUser {
  name?: string;
  address?: {
    street?: string;
    city?: string;
  };
}

const user: DeepPartialUser = {
  address: {
    street: "123 Main St.",
  },
};
```


### OptionalProps

你可以创建一个 OptionalProps 工具，使组件的某些属性变为可选，同时保持其余属性必需。当你有一个包含一些可选和一些必需属性的大型 props 接口时，这将非常有用。

```ts
type OptionalProps<T, K extends keyof T> = Omit<T, K> & Partial<Pick<T, K>>;
```


### Merge Types

有时候，您可能想要合并两个或更多类型以创建一个新的类型。您可以创建一个 MergeTypes 工具，它接受多个类型作为参数，并返回合并了所有输入类型属性的新类型。

```ts
type MergeTypes<T extends object[]> = T[number];
```

怎么使用 MergeTypes

```ts

interface User {
  name: string;
  email: string;
}

interface Address {
  street: string;
  city: string;
}

type UserInfo = MergeTypes<[User, Address]>;

// The UserInfo type is equivalent to:
interface UserInfoMerged {
  name: string;
  email: string;
  street: string;
  city: string;
}

const user: UserInfo = {
  name: "John Doe",
  email: "john.doe@example.com",
  street: "123 Main St.",
  city: "New York",
};

```


###  Promise Types

You can create a PromiseType utility that extracts the resolved type of a Promise. This can be useful when working with asynchronous code that returns promises.

```ts
type PromiseType<T extends Promise<any>> = T extends Promise<infer U> ? U : never;

```

我们可以这样使用  promiseType

```ts

```


### Readonly Types

```ts
type ReadonlyProps<T> = { readonly [P in keyof T]: T[P] };
```

我们可以这样使用  promiseType

```ts

```


## Exam

### MyPick


## References

- [TypeScript Advanced Types for Next.js | Bits and Pieces](https://blog.bitsrc.io/typescript-advanced-types-for-next-js-examples-and-best-practices-in-2023-a3a3946a353e)
