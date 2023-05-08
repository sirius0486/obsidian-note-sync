
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



## 参考链接

- [TypeScript Advanced Types for Next.js | Bits and Pieces](https://blog.bitsrc.io/typescript-advanced-types-for-next-js-examples-and-best-practices-in-2023-a3a3946a353e)
