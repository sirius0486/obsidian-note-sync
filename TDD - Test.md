
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