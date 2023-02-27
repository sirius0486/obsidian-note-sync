
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

如果可以,  选择应该是  `pnpm > yarn > npm`

### npm
只要你安装了 `Node.js` , 那么你就有安装 `npm` 

安装速度会比 yarn 和 pnpm 慢一点(很多😅) , 且会占用更多的磁盘空间 (重复安装同一个依赖库)

### yarn

`Yarn` 相较于 `npm` 要新一点, 由Facebook开发。 通过  `npm i -g yarn` 全局安装 `yarn`

会比 `npm` 快一点 ，并且使用一个扁平的`node_modules`目录 (将嵌套依赖拍平)，避免了**软件包的重复**

### pnpm

> `pnpm`  的 p 是 performance(高性能) 的意思, 作者对 npm 和 yarn 的性能和磁盘占用感到不满意故开发,  如今已经被广大流行开源项目采用,  如 Vue 等,  通过 `npm i -g pnpm` 全局安装 `pnpm`

`pnpm` 比 `npm` 和 `yarn` 要 快得多 , 而且也更节省 磁盘空间 

`pnpm` 会将所有依赖统一存储在  `~/.pnpm-store` 目录下, 相同依赖会使用 `hardlink` (硬链接) 和 symlink(软链接) 来引用到当前项目, 从而解决依赖重复安装的问题,  安装依赖的时候 `pnpm` 会先检查 `store` 目录，如果依赖已经存在则会通过硬链接引用到你当前项目中，而不是重新安装依赖。


无论你在多少个项目中安装多少次依赖, 在你的磁盘上只会存在一个, 所以安装速度要快得多(同理磁盘占用)


