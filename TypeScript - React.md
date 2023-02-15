
## JSX



## interface
> 定义接口的形状

```ts

interface IUser {

}

interface LabeledValue {
  label: string;
}
 
function printLabel(labeledObj: LabeledValue) {
  console.log(labeledObj.label);
}
 
let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```

## type aliases

1. 有两种方法去定义一个对象的形状: 接口 `interface` 和 类型别名 `type aliases`
1. 它们非常相似, 并且在大多数情况下是相同的