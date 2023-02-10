
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