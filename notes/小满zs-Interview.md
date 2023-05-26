## 自我介绍

> 自我介绍应表达清晰简洁， 介绍自身背景的同时突出自身的优势
> 不应太短也不应太长， 就是暖场热身，让气氛活跃起来
> 同时让面试官有空看下你的简历，准备接下来的提问

面试官你好， 我的名字叫`xxx`,  `20XX`年毕业于`xx大学` ， 专业是 `xxxx`，绩点是`xxx` ，在校获得`xxx` 证书 (学渣自觉跳过，避免暴露弱点)， 有`xxx`年的前端经验，使用的技术栈有`xxx` ， 毕业后在`xxx`工作 ， 期间负责过`xxx`业务， 担任`xx`的角色，期望的职位和薪资是 `xxxx` 和 `xxx`, 我的自我介绍完毕

## 计算机底层原理

### CPU 执行原理 & 冯诺依曼体系结构

**CPU的执行原理基于冯诺依曼体系结构（Von Neumann architecture），该体系结构是现代计算机体系结构的基础** 

> 冯诺依曼体系

1. 存储器（Memory）：用于存储指令和数据。存储器被划分为不同的地址，每个地址存储一个字节（或多个字节）的数据。指令和数据在存储器中被顺序存放。
2. 中央处理器（Central Processing Unit）：由控制单元（Control Unit）和算术逻辑单元（Arithmetic Logic Unit）组成。控制单元负责解析和执行指令，控制数据的流动，并与其他系统组件进行交互。算术逻辑单元执行算术和逻辑运算。
3. 输入/输出（I/O）子系统：用于与外部设备进行数据交互，包括键盘、鼠标、显示器、硬盘等。数据通过输入/输出控制器传输到和从中央处理器。
4. 数据通路（Data Path）：连接中央处理器、存储器和输入/输出子系统的通信路径。数据通路用于传输指令和数据，以及执行算术和逻辑运算

> CPU的执行过程如下：

1. 指令获取（Instruction Fetch）：控制单元从存储器中获取下一条指令，并将其存储在指令寄存器中。 
2. 指令解码（Instruction Decode）：控制单元解析指令，确定指令类型和所需操作。
3. 操作数获取（Operand Fetch）：根据指令中的地址信息，控制单元从存储器中获取操作数（数据）。
4. 执行（Execution）：算术逻辑单元执行指令指定的操作，如加法、乘法、逻辑运算等。
5. 存储结果（Result Store）：将执行结果存储到指定的存储器位置或寄存器中。

以上过程循环执行，直到程序执行完毕

> CPU的核心部件包括以下几个主要组件：

1. 控制单元（Control Unit）：控制单元负责解析和执行指令，协调和控制CPU内部各个部件的操作。它从存储器中获取指令，并根据指令的类型和操作确定下一步的动作。控制单元还负责处理中断和异常情况。
2. 算术逻辑单元（Arithmetic Logic Unit，ALU）：ALU执行计算机中的算术和逻辑运算。它可以执行诸如加法、减法、乘法、除法、位运算和逻辑运算（如与、或、非等）等基本操作。ALU的设计决定了CPU的运算能力。
3. 寄存器（Registers）：寄存器是CPU内部的高速存储器，用于存储和操作指令和数据。CPU中有多种类型的寄存器，包括程序计数器（Program Counter，PC）、指令寄存器（Instruction Register，IR）、通用寄存器（General Purpose Registers）等。这些寄存器用于存储临时数据、中间结果和控制信息。
4. 数据通路（Data Path）：数据通路是连接控制单元、ALU和寄存器之间的路径。它负责数据的传输和处理，将数据从寄存器取出送入ALU进行运算，并将结果存回寄存器。

这些核心部件共同协作，实现了指令的解析、数据的处理和结果的存储，从而完成计算机程序的执行。除了上述核心部件外，还有一些辅助部件，如缓存、总线接口和时钟等，用于提高CPU的性能和功能。

### 介绍一下dll 文件

> dll 是 Windows 系统中广泛使用的可执行文件格式，它是一种共享库（shared library）的实现，用于存储和提供可被多个程序共享的代码、数据和资源。

类似前端中的组件库概念， 可以被多个程序共享使用，这样不同的程序可以调用同一个DLL文件中的函数和方法， 避免代码重复编写和占用过多的存储空间

### js底层数据结构如何存储在V8里面

- 原始数据类型存储在栈中
- 引用数据类型存储在堆中

### AOT 和 JIT 的区别

- AOT 执行前先将代码编译成机器码
- JIT   边执行边编译

有些编程语言像 Java 可以既支持 AOT 也支持 JIT , 


## H5新特性

### localStorage
> localStorage 

- localStorage API
- localStorage 实现原理
- localStorage 存在哪儿
- localStorage 跨域

### PWA
> PWA 全称是 Progressive Web Application, 渐进式web应用

- PWA优点
- Service Workers
- PWA和 hybrid 的不同

### Canvas
>Canvas是 画布

- Canvas 常用API

### WebSocket
> WebSocket是协议， 

- webSocket 的用法
- 手动实现ws协议
- SSE 和 ws 的区别

### WebWorker
> WebWorker 是

- webWorker 用法
- webWorker实现原理

## 计算机网络

### 区分强网弱网

### 浏览器输入一个url 发生了什么 
- DNS解析顺序 
- 追问OSI 七层网络模型 
- TCP三次握手 
- http https 区别 
- http1 2 3 区别 
- 强缓存 协商缓存  last-modify    ETag

### TCP 跟 UDP 的区别

### TCP 的 超时重传协议 滑动窗口思想

### Ajax fetch navigator.sendBeacon 三个的区别


## 浏览器相关

### HTML 的字符实体是什么

- 空格 &nbsp

### SEO
> Searching Engine Optimize 搜索引擎优化



### BFC
> Block Format Context 块级格式化上下文

### 回流与重绘 以及优化方案
> 回流指的是元素颜色等发生变化， 浏览器重新渲染


> 重绘指的是页面元素大小发生变化， 浏览器重新计算元素分布，


性能代价开销 重绘 >>> 回流

### webComponents & 微前端 & emp 模块联邦

> Web Components是


> 微前端是

微前端的实现方案有: 
- iFrame
- 阿里的乾坤  Qiankun  from Alibaba
- 腾讯的无界 Wujie from Tencent
- etc...

### css盒模型 和 怪异盒模型区别 以及统一策略

> 怪异盒模型  宽度不包括 padding 和  border


### FPS 帧率 requestIdleCallback performance

### async  defer

### 讲一下 GLSL Shader 实现亮度(Brightness)、对比度(Contrast) 和边缘检测(Edge Detection) 是如何实现的回答的时候忘记了对比度的算法实现没答上来，讲了下明度 Luminance 的调节；亮度Brightness是RGB+亮度系数；边缘检测和图像锐化是使用 Convolution Kernel 卷积核加深中心像素与周围像素的色彩差值梯度，使边缘更加突出

### 计算机图形绘制原理

### WebAssembly 工作原理 如何编译成wasm

### webRTC 架构 如何 实现推流 拉流

### 垃圾回收 内存泄漏 堆栈

## CSS 相关

### CSS伪类

### 为什么哔哩哔哩用vmin 不用 vh

### CSS变量

### CSS动画 / 关键帧
> 如果需要手动写动画，你认为最小时间间隔是多久，为什么？ 答：多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60*1000ms＝16.7ms

### bem架构

### less scss 解决了什么问题

### postCss 是干嘛的 是否用过 是否写过插件

### 是否用过tailwindCss 是否用过unoCss


## 基础实施相关 （部署/ 构建/ 发版本）

### 什么是灰度


### 动态扩容 动态缩容 横向扩容 怎么做

### nginx 四层LB负载均衡 nginx七层LSB 负载均衡怎么做 nginx多机房异地容灾怎么做

### nginx源码中的unix域是怎么做的 做什么的

### nginx lua插件怎么写

### 网关怎么做 网关熔断怎么做 网关分流怎么做 网关加密怎么做


### Npm 是什么 package-lock.json 是做什么的 npm 缓存原理

### pnpm 实现原理 以及 monorepo 架构

### 如何发布 npm 包 有没有发过 自己的 npm包 周下载量多少

### webpack vite rollup esbuild swc gulp

### Webpack 脱口而出的配置 webpack 分包 webpack 打包优化 webpack打包原理 以及 HMR 原理

### Vite原理 中间件原理 是否写过vite插件

### rollup 和 webpack的区别

### esBuild 常用命令 以及 为什么这么快

esBuild 使用 Go 语言开发， Go 语言是静态编译的语言， 比JS 这种边解释边执行的脚本语言执行速度要快得多， 其次Go语言天生支持高并发任务，如协程等， 而JS是单线程语言，


## JS相关

### typeOf null 是什么 原因是什么

### 比较两个对象是否相等

### 判断是不是数组

### 说说常用的es6

### proxy Reflect 为什么要配合 proxy劫持 函数 劫持for in

### 迭代器 生成器 for of 以及 Iterator 以及数组解构原理 和对象解构原理（深入V8引擎）

### Class 用法 super原理 继承 如何定义私有属性

### AMD CMD UMD CJS ESM IIFE 的区别

### Promise 静态方法 以及 all 实现原理 有限状态机

### map set weakMap weakSet

### 微任务 宏任务 同步 异步 async await

### 装饰器 以及 装饰器解决了什么问题

### ArrayBuffer 如何使用 以及跟webGl 的关系

### 深拷贝 防抖 节流

### 聊聊 断点续传怎么做（前后端）

### 实现深拷贝的几种方法 追问 对象群嵌套15层 我想用14层的一个属性 最优解决方案 引出 Immutable js 追问 Immutable js 实现原理 字典 位分区 及 树压缩算法

### 什么是纯函数 什么是副作用函数


## 框架相关

> Vue
###  Vue2 3 区别

### Diff算法 追问 最长递增子序列算法 以及 二分查找 和 贪心算法

### 响应式原理 追问 为什么使用位运算

### Vue源码调度机制 以及nextTick执行机制

### Vue3 新增2个内置组件 介绍

### Vue3 keep-alive LRU 算法以及原理介绍

### Vue-router 原理 hash 和 history 以及 对应微前端 以及monorepo 架构

### Pinia vuex 设计模式 以及实现原理 为什么刷新数据丢失 以及解决方案

> React 

- RSC是什么？为什么React Core Team 要推动RSC ？
- React Fiber
- React diff 算法
- 并发渲染


## 服务端相关

### nodejs 

是否用过一些库 如 express koa nest 追问用的什么数据库 以及高速缓存 如 redis ，用的什么ORM框架，如果熟悉express 追问 中间件原理，熟悉nest 追问 ioc控制反转 DI 依赖注入 设计模式 以及MVC 架构 和MVVM 区别 继续追问nest rxjs 库用法 以及原理 继续追问nest 微服务 gRPC MQ 以及网关 。

聊聊nodejs 的 vm虚拟机 以及PAI 以及 底层libuv openSSL

聊聊nodejs 子线程 进程守卫怎么做

### database
聊聊数据库 mysql 底层数据结构 为什么使用B+ 树，继续追问 mysql事务以及四大特性 追问悲观锁和乐观锁

### redis

聊聊redis redis是单线程还是多线程 以及底层原理







