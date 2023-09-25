---
highlight: atom-one-dark
theme: condensed-night-purple
---
> 原文链接 🔗 [The React Ecosystem in 2023](https://www.builder.io/blog/react-js-in-2023)


![ReactEcosystem2023.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/00b75249fca247e0a0b3e3dbebf2f93a~tplv-k3u1fbpfcp-watermark.image?)

# 生态一览

`React` 诞生至今已经走过10个年头, 自从`Facebook`（现Meta）在**2013年5月**宣布开源以来，生态系统蓬勃发展， 同时不断推出新的进步和创新， 如首创的 `JSX语法`已经被许多同类`JavaScript`框架所采纳， 无论是 `Virtual Dom` 还是 `Hooks` 亦或是最近React团队在大力推动的`RSC(React Server Components)`， React带来的思想一直在引领整个Web社区， 作为全世界使用最为广泛的前端框架，本文一同探讨2023年React的生态发展。

## 启动React

如果你想搭建一个React项目， 那么有下面几种方法

### Vite
自从基于 `Webpack`搭建官方脚手架 `CRA(Create React App)` 被社区越来越唾弃后， `React`官方也开始投降 `Vite`的怀抱， 你可以在[React官方文档](https://react.dev/) 里面找到 `一个` 指向[Vite](https://vitejs.dev/guide/) 的超链接🤣

> `Vite`的 `npm 周下载量` 已经超过`500万`，比 `Vue3` 周下载量400万+ 还要高出百万数量级，许多前端框架也采用`Vite`作为构建工具，如 `Astro`,`Nuxt3`等等，可见**天下苦Webpack久已**

### Next.js
> `TurboPack`， 比`Vite` **快十倍的**构建工具

`Next.js 13版本` 将捆绑 `TurboPack`作为应用的构建工具， `TurboPack`采用 `Rust`语言编写， 构建速度据官方宣传比`Vite`快十倍！（其实是0.01和0.09的区别，后面尤大发推测试表示这种宣传很容易误导真正的性能差距）

[Next.js](https://nextjs.org/) 可以说是 `React` 终极进化之路了，如果想推荐别人学习React，那么可以直接推荐学习`Next.js` ,  在`RSC`推出后， React团队和Vercel也是开展了非常深入的合作，`Next.js`是建立在`React`之上的框架,也称 `Meta Framework`(元框架， 基于框架的框架) `Next.js`提供了一组强大的功能，包括**自动代码分割、服务器端渲染、静态站点生成**等等。对于需要服务器端渲染和SEO优化的复杂应用程序来说，`Next.js`非常适合使用。



> 总结， 如果你想写传统客户端的中小应用，那么使用Vite构建你的React应用，如果你需要SSR等对SEO进行优化，或者不想自己从头搭建一个脚手架，那么选择 Next.js

## 路由

路由是现代 Web 应用程序的重要组成部分，有许多优秀的路由库可处理复杂的路由逻辑并创建动态单页应用程序（SPA）。

### React Router

React 中最受欢迎的路由库之一是[React Router](https://reactrouter.com/en/main)。`React Router`提供了一种简单和声明性的方式来处理你的React应用程序中的路由，因此你可以定义路由并根据当前URL呈现不同的组件。以下是一个示例代码片段，设置根路径和/about路径，并分别呈现不同内容：

```tsx
const router = createBrowserRouter([
  {
    path: "/",
    element: (
      <div>
        <h1>Hello World</h1>
        <Link to="about">About Us</Link>
      </div>
    ),
  },
  {
    path: "about",
    element: <div>About</div>,
  },
]);
```

### TanStack Router

[TanStack Router](https://tanstack.com/router/v1)是一个新晋的路由库， 相比 [React Router](https://reactrouter.com/en/main)，支持更多的特性， 可以在这看到关于[两者的比较](https://tanstack.com/router/v1/docs/comparison)

### Next.js

如果你正在使用 `Next.js`，你不需要选择一个路由库，因为 `Next.js` 已经[内置路由 - 基于文件目录](https://nextjs.org/docs/app/building-your-application/routing). 简单来说就是 `Next.js` 基于文件目录创建对应的路由， 根据每个目录下的 `page.tsx` 跳转相应的页面， 因此不需要依赖额外的路由库

> 如果你需要一个`包含SSR和/或SSG` 的完整框架路由器，可以使用 `Next.js`。`React Router`适用于没有框架的`SPA`。

## 状态管理(客户端)

React的状态管理库多的眼花缭乱，已经无力抉择了... 同样因为`React在2020年12月底`  推出的`RSC - React Server Components` ， React 将原来所有的客户端组件根据依赖划分成了
- 客户端组件 (依赖状态， 需要使用State,props, hooks等传统组件)
- 服务端组件 (依赖数据源，数据库、GraphQL端点或 fs 文件系统 等)

因此状态管理也有对应划分依据， `RSC`不是传统的`SSR`， 如果你想深入探讨`RSC` , Dan 写了一系列的文章推广 [RSC From Scratch. Part 1: Server Components](https://github.com/reactwg/server-components/discussions/5)

### Redux Toolkit(RTK)

你不会是唯一一个觉得 `Redux` 难用的人， 因为官方也觉得 [React-Redux](https://react-redux.js.org/) 难用，所以推出了 [Redux Toolkit(RTK)](https://redux-toolkit.js.org/) 来简化 `Redux`的操作， 尽管 Redux作者之一 `Dan` 曾经写过一篇文章 [you-might-not-need-redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367) 吐槽很多人在滥用 `Redux` ，`Redux` 依然占据React状态管理库的半壁江山，`Redux 的 npm下载量依然大于其他状态管理库之和`， **但是社区的趋势正在逐渐抛弃 `Redux`选择拥抱更为简洁的其他状态管理库**

这是一段使用`RTK管理状态`的代码片段:

```tsx
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```

### Zustand

最受社区拥簇的 `React 状态管理库` 非 [Zustand](https://zustand-demo.pmnd.rs/) 莫属，[Zustand](https://zustand-demo.pmnd.rs/) 是 React 的另一个状态管理库，为您的应用程序提供了清晰且轻量级的解决方案来管理状态。Zustand提供了一种内置机制来订阅状态变化，因此您可以轻松地将UI与数据保持同步。对于希望使用轻量级且易于使用的状态管理解决方案而不需要像Redux这样更大型库的开发人员来说，它是一个很好的选择。以下是使用Zustand进行简单增量计数器的代码片段：

```tsx
import { create } from 'zustand'

const useStore = create((set) => ({
  count: 1,
  inc: () => set((state) => ({ count: state.count + 1 })),
}))

function Counter() {
  const { count, inc } = useStore()

  return (
    <div>
      <span>{count}</span>
      <button onClick={inc}>one up</button>
    </div>
  )
}
```

[Zustand](https://zustand-demo.pmnd.rs/) 为状态管理提供了一种**轻量级且简单易用**的解决方案, 不用再被`Redux`一连串的模版代码和哲学折磨得死去活来了，Redux bye bye ~


> 值得一提的是`Zustand`的作者还有另外2个很流行的状态管理库， 就是[Jotai](https://jotai.org/) 和 [valtio](https://github.com/pmndrs/valtio)

## 状态管理(服务端)

服务器状态管理是指管理存储在服务器上并由客户端应用程序远程访问的数据。这些数据可以包括用户身份验证详细信息、数据库记录和其他后端数据。为了在React应用程序中管理服务器状态，有几个库可供使用。

### TanStack Query(React-Query)

最受欢迎的是 [TanStack Query](https://tanstack.com/query/latest)(`React-Query`)， 它为 React 应用程序提供了一种直观而强大的管理服务器状态的方式。`它提供了一个缓存层，自动管理数据状态，并根据需要获取和更新数据`。该库还提供了许多内置功能，例如`自动重新获取`、`轮询和分页`，使得处理复杂数据集变得容易。以下是一个示例代码片段，在函数组件中查询 API 并处理返回的响应：

```tsx
function GitHubStats() {
  const { isLoading, error, data, isFetching } = useQuery({
    queryKey: ["repoData"],
    queryFn: () =>
      axios
        .get("https://api.github.com/repos/gopinav/react-query-tutorials")
        .then((res) => res.data),
  });

  if (isLoading) return "Loading...";

  if (error) return "An error has occurred: " + error.message;

  return (
    <div>
      <h1>{data.name}</h1>
      <p>{data.description}</p>
      <strong>👀 {data.subscribers_count}</strong>{" "}
      <strong>✨ {data.stargazers_count}</strong>{" "}
      <strong>🍴 {data.forks_count}</strong>
      <div>{isFetching ? "Updating..." : ""}</div>
    </div>
  );
}
```


### SWR
> 来自国人[shuding](https://github.com/shuding) 的作品， 目前主要由 `Vercel` 团队成员维护

[SWR](https://swr.vercel.app/) 是React应用程序中管理服务器状态的另一个流行库。名称“SWR”来自于[HTTP RFC 5861](https://tools.ietf.org/html/rfc5861)所推广的一种缓存失效策略`stale-while-revalidate`。与TanStack Query相比，SWR确实有一些功能限制。



### Apollo Client

[Apollo Client](https://www.apollographql.com/docs/react/)是React应用程序中管理服务器状态的另一个流行库，特别适合使用`GraphQL API`

> 补充
> - 如果您正在使用Redux Toolkit进行客户端状态管理，则[Redux Toolkit Query](https://redux-toolkit.js.org/rtk-query/overview)是无缝管理服务器状态的绝佳选择。
> - 如果你构建的API是 `REST API`，那么选择**Tanstack Query**
> - 如果是 `GraphQL` ， 则选择 **Apollo Client** 


## 表格

处理表单可能是一项繁琐且容易出错的任务，但现在有许多优秀的React表单处理库可供选择。其中一些最受欢迎的选项包括`Formik`和`React Hook Form`。这些库使得处理表单验证、提交和错误处理更加容易。

### Formik

虽然 [Formik](https://formik.org/) 提供了直观的API来管理表单状态、验证输入和提交数据，但该库目前并未得到积极维护

### React Hook Form

[React Hook Form](https://react-hook-form.com/) 应该是你在 `2023 年处理表单的首选库`。它轻量、快速且易于使用。React Hook Form 利用 React hooks 的强大功能来管理表单状态和验证规则。它还提供了一个灵活的 API 来构建表单，并允许您轻松集成其他库，如 [Yup](https://github.com/jquense/yup) 和 [Zod](https://zod.dev/) 进行验证。

与 `Formik` 不同，`React Hook Form` 不需要大量样板代码，并且可以显著减少处理表单数据所需的代码量。此外，由于组件不会为字段值中的每个更改重新渲染，因此 React Hook Form 具有出色的性能。

以下是一个示例代码片段，演示了如何使用 `react hook form` 接受用户的名字和姓氏：

```tsx
import { useForm } from "react-hook-form";

export default function App() {
  const { register, handleSubmit, watch, formState: { errors } } = useForm();
  const onSubmit = data => console.log(data);

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input {...register("firstName")} />
      
      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("lastName", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.lastName && <span>This field is required</span>}
      
      <button>Submit</button>
    </form>
  );
}
```


## 测试框架

`测试`是构建高质量`React应用程序`的重要组成部分。在测试React应用程序时，可以考虑两个优秀的选项：[Vitest](https://vitest.dev/) 和 [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) 进行单元测试`(unit test)`，以及 [Playwright](https://playwright.dev/) 或者 [Cypress](https://www.cypress.io/) 进行端到端测试`(e2e test)`。

### Vitest

[Vitest](https://vitest.dev/) 是一个由Vite驱动的极速单元测试框架。在测试React应用程序的上下文中，它是一个测试运行器，可以找到测试、运行测试、确定测试是否通过或失败，并以人类可读的方式报告结果。

> 相比 [Jest](https://jestjs.io/) ， [Vitest](https://vitest.dev/) 的开发体验更良好，观看 `Vitest作者 Anthony Fu`的一段 [Vitest演示视频](https://www.bilibili.com/video/BV1kD4y1T7Ug/?vd_source=e9c5e2aa24951421eff7112778ab4b57)， 你会了解 Vitest 相比 Jest 的优势


### React Testing Library

[React Testing Library](https://testing-library.com/docs/react-testing-library/intro/) 是一种JavaScript测试实用工具，为React组件`提供虚拟DOM`进行测试。使用自动化测试时，没有实际的DOM可供使用。React Testing Library提供了一个虚拟DOM，我们可以使用它来交互并验证react组件的行为。

### Playwright & Cypress

[Playwright](https://playwright.dev/) 和 [Cypress](https://www.cypress.io/) 是提供可靠且强大的方式来测试您的React应用程序功能端到端的库。您可以编写`模拟真实用户与应用程序交互（包括点击、键盘输入和表单提交）`的测试。它们还具有出色的文档和活跃的社区。

> 你甚至可以用 Playwright 写爬虫 🤣

## 样式

### Tailwind

[Tailwind CSS](https://tailwindcss.com/) 是一个实用优先的原子类 CSS 框架，提供了一组预定义类来构建 UI 组件。使用 Tailwind CSS，您可以快速创建复杂的布局和自定义样式，而无需从头编写 CSS。它拥有出色的文档和活跃的社区，使其成为开发人员创建现代响应式 UI 的首选。

```tsx
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
  Button
</button>
```

### Styled Components

[Styled Components](https://styled-components.com/)是一个流行的库，用于使用 `CSS-in-JS` 样式化 React 组件。它允许您`直接在 JavaScript 代码中编写 CSS`，从而轻松创建针对单个组件进行作用域限定的动态样式。`Styled Components` 还具有出色的主题支持，使您可以快速切换应用程序的不同样式。

```tsx
import styled from 'styled-components';

const Button = styled.button`
  background-color: #3f51b5;
  color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #303f9f;
  }
`;

export default Button;
```

### Emotion

[Emotion](https://emotion.sh/docs/introduction) 是另一个CSS-in-JS库，为React组件提供了强大的API来进行样式设置。它具有高性能，并允许您使用各种语法 `（包括CSS、Sass和Less` 定义样式。

### CSS Modules

[CSS Modules](https://github.com/css-modules/css-modules) 是React中流行的样式处理方法，它允许您编写`模块化的CSS代码`，并将`其作用域限定在各个组件内部`。使用`CSS Modules` ，您可以编写**仅适用于特定组件的CSS类，避免命名冲突并确保样式正确封装**。在CSS模块方法中，您需要创建一个单独的CSS文件（例如`Button.module.css`），其中包含以下内容：

```tsx
// Button.jsx
import styles from './Button.module.css';

const Button = () => (
  <button className={styles.button}>
    Button
  </button>
);

export default Button;
```
```css
/* Button.module.css */
.button {
  background-color: #3f51b5;
  color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}

.button:hover {
  background-color: #303f9f;
}
```


### UI 库

UI组件库对于React开发人员来说可以节省大量时间，现在有许多优秀的选择。其中一些最受欢迎的选项包括：

-   [Material UI](https://mui.com/)
-   [Mantine UI](https://ui.mantine.dev/)
-   [Ant Design](https://ant.design/)
-   [Chakra UI](https://chakra-ui.com/)

还有一些基于`Tailwind`构建的UI库

-   [ShadCN](https://ui.shadcn.com/)
-   [Daisy UI](https://daisyui.com/)
-   [Headless UI](https://headlessui.com/)

个人比较推荐 [ShadCN](https://ui.shadcn.com/) 这个库，它其实不是一个库，而是预先定义好的不同组件的`代码片段`， 所以你完全可以自定义组件的样式， 同时它是目前唯一支持RSC比较好的UI库， 从`Next.js`官方提供的许多Template来说， 都依赖了这个UI库或者它的底层 `RadixUI`

## 动画库

### Framer Motion & Reacrt Spring

[React Spring](https://www.react-spring.dev/) 和 [Framer Motion](https://www.framer.com/motion/) 动画是创建引人入胜、交互式用户界面的强大工具，而且有许多出色的React动画库可供选择。其中一些最受欢迎的选项包括[React Spring](https://www.react-spring.dev/) 和 [Framer Motion](https://www.framer.com/motion/) 。这些库使得使用最少的代码轻松创建平滑、响应式的动画成为可能。

以下是一个使用 [Framer Motion](https://www.framer.com/motion/) 的示例代码片段。Motion核心组件是`motion component`，可以将其视为普通HTML或SVG元素，但带有超强动画功能。通过在 animate 属性上设置值即可简单地对 motion component 进行动画处理。

```tsx
import { motion } from "framer-motion";

export default function App() {
  return (
    <motion.div
      className="box"
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
    />
  );
}
```


## 数据可视化


数据可视化是许多React应用程序的重要组成部分，特别是那些依赖于复杂数据集的应用。一些流行的 React 数据可视化库包括：
-   [Victory](https://formidable.com/open-source/victory/)
-   [React Chartjs](https://react-chartjs-2.js.org/)
-   [Recharts](https://recharts.org/en-US).

## 表格

在 React 中实现表格可能是一个具有挑战性的组件，但是有许多优秀的表格库可供选择。一些流行的选项包括:
-   [TanStack Table](https://tanstack.com/table/v8)
-   [React Data Grid](https://github.com/adazzle/react-data-grid)

这些库使得创建强大且可定制化的表格变得容易，具备排序、过滤和分页等功能。

## i18n 国际化支持

`国际化（ Internationalization - i18n)` 对于许多应用程序尤其是那些面向全球受众的应用程序来说都是一个重要考虑因素。像 [i18next](https://react.i18next.com/) 和 [React-Intl](https://formatjs.io/docs/react-intl/) 这样的库可以帮助将您的应用程序翻译成多种语言并处理本地化。推荐的选择包括：

-   [i18next](https://react.i18next.com/)
-   [React-Intl](https://formatjs.io/docs/react-intl/)


## Dev Tools

-   [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
-   [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
-   [React Hook Form DevTools](https://react-hook-form.com/dev-tools)
-   [TanStack Query DevTools](https://tanstack.com/query/v4/docs/react/devtools).

## 类型检查

虽然`React`源码是使用`Flow`， 但是我相信大多数人开发React应用添加类型检查首选都是`TypeScript`

> 个人顺道分享一些觉得质量不错的 `TypeScript` 学习 & 练习 资源
- [handbook](https://www.typescriptlang.org/docs/handbook/intro.html)  TS 官方手册
- [type-challenges]() TS 类型体操
- [Type-Level TypeScript](https://type-level-typescript.com/) 通过做题来学TS
- [TypeScript on Exercism](https://exercism.org/tracks/typescript) 类似 LeetCode 做题学 TS
- [learn.microsoft.com](https://learn.microsoft.com/zh-cn/training/browse/?terms=typescript) 微软官方出品的TS教程


## 文档生成器

文档是任何软件项目的重要组成部分。对于创建文档应用程序，[Docusaurus](https://docusaurus.io/) 是一个非常好的选择。当然，您也可以使用 [Next.js]() 和类似 [Nextra](https://nextra.site/) 的库。

### Docusaurus

Meta React相关的开源项目几乎所有文档都是用 [Docusaurus](https://docusaurus.io/) 生成的， 包括 React官方文档

### Nextra

[Nextra](https://nextra.site/) 同样出自国人[shuding](https://github.com/shuding/nextra) 之手 ,  基于 Next.js 基础开发的文档生成器 

### Astro
> 得益于 [islands architecture- 孤岛架构](https://docs.astro.build/en/concepts/islands/)  ， [Astro](https://astro.build/) 能做到 `0 JavaScript`， 这极大提升了网站的加载速度 

如果你的内容绝大多数是静态内容， 那么使用 [Astro](https://astro.build/) + React 也不失为一种组合

## 原生移动应用

### React Native

[React Native](https://reactnative.dev/) 已成为使用React构建本地移动应用程序的越来越流行的选择。 React Native允许开发人员使用React和本机组件创建跨平台移动应用程序。

国内RN市场份额不大 ， 如果做APP大概面临以下几种选择 
- 追求极致性能和用户体验， `原生IOS + Android`
- 或者性能稍微差点的 [Flutter](https://flutter.dev/)
- 小程序， [React Native](https://reactnative.dev/) 未能从中分一杯羹

## 很棒的第三方库

除了上面列出的库和工具之外，还有许多其他适用于React开发人员的优秀库可供选择。一些流行的选项包括：

-   [**dnd kit**](https://dndkit.com/) 用于 拖放/拽 功能
-   [**react-slick**](https://react-slick.neostack.com/) 用于 构建幻灯片
-   [**react-dropzone**](https://react-dropzone.js.org/) 用于文件上传


