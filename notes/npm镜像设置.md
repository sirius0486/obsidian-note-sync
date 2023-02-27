
1. 使用官方镜像
```sh
 npm config set registry https://registry.npmjs.org
```

2. 使用淘宝镜像
```sh
npm config set registry https://registry.npm.taobao.org
```


3. 查看当前镜像
```sh
npm config get registry
```

4. 清除npm缓存
```sh
npm cache clean --force
```

5. 更新 package dependcy 版本
```sh
npm i -g npm-check-updates
ncu -u
npm install
```


## npm, yarn 和 pnpm 的区别

> pnpm 优势最大且已经广泛被社区接纳 , 但 npm 是官方维护且不断吸收其他包管理的优点 

### npm
只要你安装了 `Node.js` , 那么你就有安装 `npm` 

安装速度会比 yarn 和 pnpm 慢一点(很多😅) , 且会占用更多的磁盘空间 (重复安装同一个依赖库)


### yarn

`Yarn` 相较于 `npm` 要新一点, 由Facebook开发。 通过  `npm i -g yarn` 全局安装 yarn

会比 `npm` 快一点 ，并且使用一个扁平的`node_modules`目录 (将嵌套依赖拍平)，避免了**软件包的重复**



### pnpm

PNPM是另一个较新的软件包管理器，声称比NPM和Yarn更快、更有效。它使用硬链接和符号链接，在磁盘上只保存一个版本的软件包，这就减少了磁盘的使用和安装时间12。它还支持NPM和Yarn的大部分功能。