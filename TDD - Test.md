
## Jest

## React-testing-library

### Q & A

#### Question: ReferenceError: document is not defined

> 参考 [https://github.com/testing-library/react-testing-library/issues/422](https://github.com/testing-library/react-testing-library/issues/422)

`React Testing Library needs a DOM to operate. Change your jest config `testEnvironment` to `jsdom` and you'll be set.`

React Testing Libray 需要一个 DOM 来操作 , 

> [!info] > 解决办法: `pnpm add -D @testing-library/jest-dom`


#### Question: ReactJS and Typescript : refers to a value, but is being used as a type here (TS2749)

> [!info] > 解决办法:  更改文件后缀 `ts`   为 `.tsx`

### Question: Property 'toHaveTextContent' does not exist on type Assertion`<HTMLElemen>

> [!info] > 解决办法 : 暂未解决






## Vitest


### toMatchInlineSnapshot()

```tsx
import { describe,test,expect  } from 'vitest';
import { loadUserData} from '../hooks/loadUserData'


describe( "loadUsesr data", () => {

  test('should load user data as expected', async () => {
      const user = await loadUserData('antfu7');

      expect(user).toEqual({
          "coolness": 100,
          "name": "Anthony",
          "projects":  [
            "vitest",
            "vite",
          ],
          "username": "antfu7",
          "favoriteFood": "sushi",
        })
  });

  test('should sets coolness level appropiatley', async () => {

    const keqing = await loadUserData('keqing77');
    const anthony = await loadUserData('antfu7'); 

    expect(keqing.coolness).toBe(1);
    expect(anthony.coolness).toBe(100);
  });

  test('should throws an error for nonexistent users', () => {

    expect(async () => await loadUserData('faker')).rejects.toThrowError('no user found') ;
  });

  test('should load user data use snapshot', async () => {
    const user = await loadUserData('antfu7');

    expect(user).toMatchSnapshot()

  })

  test('should load user data use InlineSnapshot', async () => {
    const user = await loadUserData('antfu7');

    expect(user).toMatchInlineSnapshot(`
      {
        "coolness": 100,
        "favoriteFood": "sushi",
        "name": "Anthony",
        "projects": [
          "vitest",
          "vite",
        ],
        "username": "antfu7",
      }
    `);

  })

})

```

## note

### jsdom

> **jsdom** 是一个库，用于在单元测试时，模拟 dom 环境，从而将被测试的元素渲染出来，方便对 UI 进行测试

**vitest** 支持使用`jsdom`或 `happy-dom`这两个库来模拟 dom 环境


### testing-library-react

> Vitest 基于 Testing-Library 提供了测试、断言等 API 、jsdom 提供了模拟 dom 环境的能力


## vitest

`test`还有一个别称`it`，在 vitest 中使用`it`等同于使用`test`，我估计大概是因为`jest`中，创建测试用例的方法叫做`it`，这里为了降低上手成本也兼容了`jest`的语法。


对于 React 组件来说，外部输入就是`props`，内部状态就是`stat`




## 踩坑记录


### 'test' does not exist in type 'UserConfigExport'

```ts
文件顶部增加注释
/// <reference types="vitest" />
/// <reference types="vite/client" />
```

### Invalid Chai Property : toBeInTheDocument

> Property 'toBeInTheDocument' does not exist on type  `Assertion<any>`

`vitest` 默认没有` toBeInTheDocument` 方法， `toBeInTheDocument` 是 testing library 中的断言方法，vitest 默认不包含，因此我们需要配置一下初始化文件，继承 testing library 断言库，新建一个 `vitest-setup.ts `文件

```ts
import { vi, expect, afterEach } from "vitest";
import { cleanup } from "@testing-library/react";
import matchers, {
  TestingLibraryMatchers,
} from "@testing-library/jest-dom/matchers";

declare global {
  namespace Vi {
    interface JestAssertion<T = any>
      extends jest.Matchers<void, T>,
        TestingLibraryMatchers<T, void> {}
  }
}
// 继承 testing-library 的扩展 except
expect.extend(matchers);
// 全局设置清理函数，避免每个测试文件手动清理
afterEach(() => {
  cleanup();
});
```

`cleanup()` 是为了在每次 `render` 后清理 react dom 树，若不清理可能会导致内存泄漏和非“幂等”测试（这可能导致测试中难以调试的错误），详情请看[官方文档](https://link.juejin.cn/?target=https%3A%2F%2Ftesting-library.com%2Fdocs%2Freact-testing-library%2Fapi%23cleanup "https://testing-library.com/docs/react-testing-library/api#cleanup")

然后在 vitest.config.ts 中设置 setupFiles 文件路径

```ts
export default defineConfig({
  plugins: [react()],
  test: {
    environment: "jsdom",
 +   setupFiles: "./vitest-setup.ts",
  },
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "."),
    },
  },
});
```

