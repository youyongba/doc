# docker 使用
> 为了解决编码工具版本没有下各兼容，有些开源很好用的工具运行在不同版本编码工具。所以引入docker解决。

## 下载

- https://docker.com/get-docker/

## 常用命令

| 说明 |  命令  |
| :-- | --  |
| 查看版本 | docker --version |
| 查看镜像 | docker image  ls |
| 从官方源上抓一个镜像 | docker image pull hello-world |
| 运行 hello-world 容器 | docker container run hello-world |
| 运行 unbuntu bash container | docker container run -it ubuntu bash |
| 查看启动了几个容器 | docker container ls |
| 如果想关掉 container (跟上id, 不用输全) | docker container kill  xxxx |


## 创建自己的image

### hello.py

```python
print('hello world')

```

### Dockerfile

```shell
# 将 image 文件继承与官方的3.7版本的Python
FROM python:3.7
# 将当前目录下的所有文件 （除了 .dockerignore 排除的路径） . 都拷贝进 image 文件的 /app 目录。
COPY . /app
# 指定接下来的工作路程径为  /app
WORKDIR /app
# 在 /app 目录下， 运行 python 文件
CMD  python3 hello.py
```

### .dockerignore
```shell
__pycache__
env
```

### 运行命领

| 说明 |  命令  |
| :-- | --  |
| 构建image| docker image build -t python3-app . |
| 运行 python3-app container | docker container run python3-app | 
