# 本地通过express启动http服务 通过ngroke生成外网地址访问（内网穿透服务工具）

## 准备工环

- [node.js官网，去这里下载](https://nodejs.org)
- [express-generator(node.js框架)下载](https://www.npmjs.com/package/express-generator)
- [官网下载 ngroke](https://ngrok.com/)




## 初始化
> 默认是3000端口

```shell
# 初始化
express -e project
# 按装依赖
cnpm install
```


## 内网穿透命令

```shell
./ngroke http 3000

```


