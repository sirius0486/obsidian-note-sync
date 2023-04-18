
## Fiber
Fiber nodes
链表 ， 加上指向 节点， 使得可以保存进度
concurrent mode , 并发模式


## experiemental
### use
- 无限循环问题
### cache

```ts
"use client";
import {use, cache} from "react";

```


### Server Side Components

服务器组件允许在客户端渲染组件树的一部分，在服务器端渲染一部分。在服务器端渲染的组件会以HTML流的形式发送。这种策略大大减少了发送到客户端的包。此外，这种架构允许你直接从组件代码中访问典型的服务器端功能（例如，数据库或文件系统）。

```tsx
import fs from 'react-fs';
import db from 'db.server';

function FileNote({ id }) {
  const note = JSON.parse(fs.readFile(`${id}.json`));
  return <NoteWithMarkdown note={note} />;
}

function DatabaseNote({ id }) {
  const note = db.notes.get(id);
  return <NoteWithMarkdown note={note} />;
}
```


- 对异步操作的友好支持
- 支持 使用 `async / await`