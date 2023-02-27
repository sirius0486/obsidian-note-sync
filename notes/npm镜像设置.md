
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

> pnpm 优势更大, 但 npm 是官方维护

### npm
只要你安装了 `Node.js` , 那么你就有安装 `npm` 

安装速度会比 yarn 和 pnpm 慢一点(很多😅) , 且会占用更多的磁盘空间 (重复安装同一个依赖库)


### yarn



### pnpm