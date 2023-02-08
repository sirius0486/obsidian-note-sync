## intro

> [!info] useReducer 用于取代部分 redux 功能
> useReducer + useContexts 在大部分场景可以取代 redux

## usage
```tsx
const [ ①state , ②dispatch ] = useReducer(③reducer)
```
1. 更新之后的 state 值。
2. 派发更新的 dispatchAction 函数, 本质上和 useState 的 dispatchAction 是一样的。
3. 一个函数 reducer ，我们可以认为它就是一个 redux 中的 reducer , reducer的参数就是常规reducer里面的state和action, 返回改变后的state, 这里有一个需要注意的点就是：**如果返回的 state 和之前的 state ，内存指向相同，那么组件将不会更新。**

## example


```tsx
// App.tsx
import Counter from "./Counter";
import "./App.css";

function App() {

  return (
    <div className="App">
      <Counter />
    </div>
  );
}

export default App;


// Counter.tsx
import { useReducer } from "react";

const reducer = (state: any, action: any) => {
  if (action.type === "incremented_age") {
    return {
      age: state.age + 1,
    };
  }
  if (action.type === "decremented_age") {
    return {
      age: state.age - 1,
    };
  }
  if (action.type === "reset") {
    return {
      age: (state.age = 0),
    };
  }
  throw Error("Unknown action.");
};

export default function Counter() {
  const [state, dispatch] = useReducer(reducer, { age: 42 });

  return (
    <>
      <button
        onClick={() => {
          dispatch({ type: "incremented_age" });
        }}
      >
        Increment age
      </button>
      <button
        onClick={() => {
          dispatch({ type: "decremented_age" });
        }}
      >
        decremented age
      </button>
      <button
        onClick={() => {
          dispatch({ type: "reset" });
        }}
      >
        reset number
      </button>
      <p>Hello! You are {state.age}.</p>
    </>
  );
}

```