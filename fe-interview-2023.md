## 未整理
https://github.com/message163/interview
https://blog.skk.moe/post/why-you-should-not-fetch-data-directly-in-use-effect/
https://juejin.cn/post/7210048692623114298?share_token=1d81ed19-2c07-42cb-af24-8e17a2ac5c07
dll文件 
webRTC 
fullter  v8  JIT 和 AOP引擎
前端埋点 SSE 单工通信
Navagate API  看网络信息 强网弱网
Interveral.observer 图片懒加载
vite 生产环境和开发环境差异
vue2 和 vue3  diff对比差异
sass @rule
webComponents 与 微前端
proxy / reflect 
es6 解构赋值的原理 ，  for of 原理
{} 没有 iterator ， 但是可以解构
灰度发布  css bem架构
网关怎么做 网关熔断怎么做 网关分流怎么做 网关加密怎么做

## 计算机原理

### AOT 和 JIT 的区别
> 程序有两种运行方式： 静态编译(AOP)  和 动态解释(JIT)

AOT的程序在执行前会全部被翻译成机器码， 如 C/C++, JAVA 等
JIT 的程序则是一边编译一边运行，如 JavaScript，Python等

值得一提的是， 有的语言既可以以JIT方式运行也可以以AOT方式运行， 像JAVA和Python，通常来说， AOT的执行效率要比JIT快得多，如果代码执行前需要先编译，那么我们都认为是属于AOT

## 前端基础

### localstorage

**localstorage API**
```js
localStorage.setItem('key', 'value');
var value = localStorage.getItem('key');
localStorage.removeItem('key');
localStorage.clear();

```

**localStorage 实现原理** 
它可以在浏览器端保存 key-value 对,  localStorage 的实现原理基于浏览器的数据存储机制。在浏览器中，每个域名都有一个相应的本地存储区域，而 localStorage 就是利用了这个本地存储区域实现的。当调用 localStorage 的 setItem 方法时，浏览器会将数据保存到本地存储区域，而调用 getItem 方法时则会从本地存储区域中读取数据。因为本地存储区域是基于域名实现的，所以同一域名下的不同页面可以共享 localStorage 中的数据

**localStorage 存在哪儿** 
本地电脑磁盘内， 不同浏览器存放的位置不同。

localStorage 存储在浏览器的本地存储区域中，具体实现可能因浏览器而异。在 Chrome 中，localStorage 数据保存在用户目录下的 Local Storage 文件夹中。在 Firefox 中，localStorage 数据保存在用户目录下的 webappsstore.sqlite 数据库文件中。在 Safari 和 Internet Explorer 中，localStorage 数据保存在单独的文件中。

**localStorage 跨域**


## 前端框架


## 工具链


## 计算机网络