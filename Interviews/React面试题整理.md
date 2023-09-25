> React JD

说实话，选一个能正常干活，不坑队友，挺难的。
我要求不高，没有八股文。
熟悉react18 next13 app router server and client component 和流式渲染，就行了。
面试俩月了，没有找到合适的。
hr 推过来的简历，不是小程序就是vue。
我的面试题没有八股文，由浅入深，考察熟悉技术栈，核心原则不因无知坑队友，不因骚操作坑队友就行了。然而很多人居然第一步答不上来。这个让我非常意外和震惊。很多人在抱怨卷的的同时，提高下业务能力也许会有一片新天地。
我举个例子，比如： 
1对于hooks 官方给出的使用限制是什么（这个答不上来直接pass，占40%左右，吃惊吧）
2 自定义组件和自定义hooks看上去只有返回值不同，为什么组件可以在循环和条件中使用，而hooks不行？
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

const fetchUser = cache(id:number) =>
	fetch(`http://localhost:3000/${id}.json?q=1`).then((res)=> res.json()
);

function LastName({id}:{id:number}) {
	const data = use(fetchUser(id));
	return <div>First: {data.first} </div>
}

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


### renderToString
