> [!success]
> Redux 学习资源 
> [Redux官方网站(英文)](https://react-redux.js.org/api/hooks)


## Provider

>[!tip] > Provider 实际上是利用了 react 的 contexts 机制 , 在顶层组件提供了 名为 store 的 全局上下文, 使得其他组件可以访问 (通过 hooks 和 Connect api , 推荐 hooks) 
> 需要用 `<Provider />` 包裹整个组件, 来使 store 在整个组件树可用

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'

import { Provider } from 'react-redux'
import store from './store'

import App from './App'

// As of React 18
const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(
  <Provider store={store}>
    <App />
  </Provider>
)

// Provider 的唯一作用 就是 传入 store 对象
```


## Hooks

> [!info] >怎么理解 hooks ?
> Hooks API给了 **函数组件** 使用本地组件状态的能力，执行副作用，以及更多。React还允许我们编写自定义钩子，让我们提取可重用的钩子，在React的内置钩子之上添加我们自己的行为。
> 
> React-redux 内置的 hooks 允许你的React组件订阅Redux商店和调度行动

### useSelector
- `useSelector` 从 ` store `  读取一个值并订阅更新 (使用一个 selector 函数)
- 可以对应于 `Connect` 的一个参数 `mapStateToProps`

### useDispatch
- `useDispatch` 返回 ` store ` 的调度方法(dispatch method )，让你调度行动 (dispatch actions)
- 这个钩子返回一个对Redux store的调度函数的引用。你可以根据需要使用它来调度行动。

### useStore
- `useStore` 返回一个 store 的引用, 理论上不应该经常被使用, 因为有 useSelector , 但某些情况会有用处, 比如 替换 reducer
- This hook returns a reference to the same Redux store that was passed in to the `<Provider>` component.

### useActions & useShallowEqualSelector()​
- 根据[Dan Abramov's suggestion](https://github.com/reduxjs/react-redux/issues/1252#issuecomment-488160930). Redux 新版本应致力于更简单的 Api , 所以这些 hooks 不建议使用,  因为造成了太多的概念开销和句法复杂性, 但目前还是保留在了现版本

## Connect
> [!info]  建议使用 hooks API 代替 Connect , 尽管目前依然可用 (不推荐)
> The connect() function connects a React component to a Redux store.

```js
function connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)

// Connect 是一个高阶函数 , 即调用一个函数返回另一个函数
// 有四个参数 都是可选 
```



## Demo
> [!success] 通过一个 demo 来理解 react-redux (经典计数器)

-   创建一个store文件夹
-   创建一个index.ts做为主入口
-   创建一个festures文件夹用来装所有的store
-   创建一个counterSlice.ts文件，并导出简单的加减方法


### index.tsx

1. 使用 `Provider` 组件包裹 顶层组件, 并传入 store 的 props

```ts
import React from 'react';
import { createRoot } from 'react-dom/client';
import { Provider } from 'react-redux';
import { store } from './app/store';
import App from './App';
import './index.css';

const container = document.getElementById('root')!;
const root = createRoot(container);

root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

### App.tsx

```ts
import { Counter } from './features/counter/Counter';

const App = () => <Counter />

export default App;
```

### store.tsx
```ts
import { configureStore, ThunkAction, Action } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice';

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export type AppDispatch = typeof store.dispatch;
export type RootState = ReturnType<typeof store.getState>;
export type AppThunk<ReturnType = void> = ThunkAction<
  ReturnType,
  RootState,
  unknown,
  Action<string>
>;

```

### hooks.tsx

```ts
// app/hooks.tsx

import { TypedUseSelectorHook, useDispatch, useSelector } from 'react-redux';
import type { RootState, AppDispatch } from './store';

// Use throughout your app instead of plain `useDispatch` and `useSelector`
export const useAppDispatch = () => useDispatch<AppDispatch>();
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;

```

### Couter.tsx

```ts
// features/counter

import React, { useState } from 'react';

import { useAppSelector, useAppDispatch } from '../../app/hooks';
import {
  decrement,
  increment,
  incrementByAmount,
  incrementAsync,
  incrementIfOdd,
  selectCount,
} from './counterSlice';
import styles from './Counter.module.css';

export function Counter() {
  const count = useAppSelector(selectCount);
  const dispatch = useAppDispatch();
  const [incrementAmount, setIncrementAmount] = useState('2');

  const incrementValue = Number(incrementAmount) || 0;

  return (
    <div>
      <div className={styles.row}>
        <button
          className={styles.button}
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          -
        </button>
        <span className={styles.value}>{count}</span>
        <button
          className={styles.button}
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          +
        </button>
      </div>
      <div className={styles.row}>
        <input
          className={styles.textbox}
          aria-label="Set increment amount"
          value={incrementAmount}
          onChange={(e) => setIncrementAmount(e.target.value)}
        />
        <button
          className={styles.button}
          onClick={() => dispatch(incrementByAmount(incrementValue))}
        >
          Add Amount
        </button>
        <button
          className={styles.asyncButton}
          onClick={() => dispatch(incrementAsync(incrementValue))}
        >
          Add Async
        </button>
        <button
          className={styles.button}
          onClick={() => dispatch(incrementIfOdd(incrementValue))}
        >
          Add If Odd
        </button>
      </div>
    </div>
  );
}

```


### counterSlice.ts

```ts

// features/counterSlice

import { createAsyncThunk, createSlice, PayloadAction } from '@reduxjs/toolkit';
import { RootState, AppThunk } from '../../app/store';
import { fetchCount } from './counterAPI';

export interface CounterState {
  value: number;
  status: 'idle' | 'loading' | 'failed';
}

const initialState: CounterState = {
  value: 0,
  status: 'idle',
};

// The function below is called a thunk and allows us to perform async logic. It
// can be dispatched like a regular action: `dispatch(incrementAsync(10))`. This
// will call the thunk with the `dispatch` function as the first argument. Async
// code can then be executed and other actions can be dispatched. Thunks are
// typically used to make async requests.
export const incrementAsync = createAsyncThunk(
  'counter/fetchCount',
  async (amount: number) => {
    const response = await fetchCount(amount);
    // The value we return becomes the `fulfilled` action payload
    return response.data;
  }
);

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  // The `reducers` field lets us define reducers and generate associated actions
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    // Use the PayloadAction type to declare the contents of `action.payload`
    incrementByAmount: (state, action: PayloadAction<number>) => {
      state.value += action.payload;
    },
  },
  // The `extraReducers` field lets the slice handle actions defined elsewhere,
  // including actions generated by createAsyncThunk or in other slices.
  extraReducers: (builder) => {
    builder
      .addCase(incrementAsync.pending, (state) => {
        state.status = 'loading';
      })
      .addCase(incrementAsync.fulfilled, (state, action) => {
        state.status = 'idle';
        state.value += action.payload;
      })
      .addCase(incrementAsync.rejected, (state) => {
        state.status = 'failed';
      });
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

// The function below is called a selector and allows us to select a value from
// the state. Selectors can also be defined inline where they're used instead of
// in the slice file. For example: `useSelector((state: RootState) => state.counter.value)`
export const selectCount = (state: RootState) => state.counter.value;

// We can also write thunks by hand, which may contain both sync and async logic.
// Here's an example of conditionally dispatching actions based on current state.
export const incrementIfOdd =
  (amount: number): AppThunk =>
  (dispatch, getState) => {
    const currentValue = selectCount(getState());
    if (currentValue % 2 === 1) {
      dispatch(incrementByAmount(amount));
    }
  };

export default counterSlice.reducer;

```

### Counter.module.css
```css
.row {

display: flex;

align-items: center;

justify-content: center;

}

  

.row > button {

margin-left: 4px;

margin-right: 8px;

}

  

.row:not(:last-child) {

margin-bottom: 16px;

}

  

.value {

font-size: 78px;

padding-left: 16px;

padding-right: 16px;

margin-top: 2px;

font-family: 'Courier New', Courier, monospace;

}

  

.button {

appearance: none;

background: none;

font-size: 32px;

padding-left: 12px;

padding-right: 12px;

outline: none;

border: 2px solid transparent;

color: rgb(112, 76, 182);

padding-bottom: 4px;

cursor: pointer;

background-color: rgba(112, 76, 182, 0.1);

border-radius: 2px;

transition: all 0.15s;

}

  

.textbox {

font-size: 32px;

padding: 2px;

width: 64px;

text-align: center;

margin-right: 4px;

}

  

.button:hover,

.button:focus {

border: 2px solid rgba(112, 76, 182, 0.4);

}

  

.button:active {

background-color: rgba(112, 76, 182, 0.2);

}

  

.asyncButton {

composes: button;

position: relative;

}

  

.asyncButton:after {

content: '';

background-color: rgba(112, 76, 182, 0.15);

display: block;

position: absolute;

width: 100%;

height: 100%;

left: 0;

top: 0;

opacity: 0;

transition: width 1s linear, opacity 0.5s ease 1s;

}

  

.asyncButton:active:after {

width: 0%;

opacity: 1;

transition: 0s;

}
```
