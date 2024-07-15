## Docker 基础
> Docker 是一种容器技术，相比虚拟机更加轻量化，将应用程序与程序之间的依赖打包在一个镜像里，通过在这个虚拟容器中运行这个镜像，就能达到在真实的物理机上运行的效果一样，可以说，有了 Docker，程序员可以避免一个下午只为配置开发环境打出一句 Hello World 的重复性劳动了，可以有效保证环境的一致！别再说代码跑不起来啦！

- 更高效利用系统资源 - 相比虚拟机更轻量
- 更快速的启动时间 - 秒级启动
- 一致的运行环境
- 持续交付和部署 - 通过 Dockerfile 进行镜像构建，快速部署
- 轻松维护和拓展 - 微服务架构

## Docker 常见命令

```bash
docker pull <images>:version


docker tag <image>:version <image2>:version

docker push <remoteUrl>


docker run -it -p 80:80 hello-world

docker login <域名>

```


## Dockerfile



## Docker 资源

- [Docker 快速入门](https://github.com/dunwu/linux-tutorial/blob/master/docs/docker/docker-quickstart.md)
- [Docker 最佳实践](https://github.com/dunwu/linux-tutorial/blob/master/docs/docker/docker-dockerfile.md)
- [Docker Cheat Sheet](https://github.com/dunwu/linux-tutorial/blob/master/docs/docker/docker-cheat-sheet.md)
- [Docker Cheat Sheet - zh-cn](https://github.com/wsargent/docker-cheat-sheet/tree/master/zh-cn)