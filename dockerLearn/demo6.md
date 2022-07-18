## Docker Registry demo

### 命领
| 说明 |  命令  |
| :-- | --  |
|开启本地容器 命令 | docker run -d -p 5000:5000 --name registry registry:2 |
|查看容器是否开启| docker ps |
|复制一个|docker tag ubuntu localhost:5000/my-ubuntu|
|push到本地仓库|docker push localhost:5000/my-ubuntu|
|删除localhost:5000/my-ubuntu|docker rmi localhost:5000/my-ubuntu|
|从本地拉取|docker pull localhost:5000/my-ubuntu|
|停止仓库| docker container stop store |
|将仓库删掉|docker container rm store |



****

## docker Hub
### docker hub 官网址址（官方源）

- https://hub.docker.com

### 操作流程
1. 注册/登录
1. 客户端登录
1. 在hub.docker.com创建 源
1. 本地运行命令 docker tag localhost:5000/my-ubuntu qihong1222/my-private-repo
    - qihong1222/my-private-repo是远程仓库的名称
1. docker images （查看一下是否备份）
1. docker push qihong1222/my-private-repo
1. docker rmi qihong122/my-private-repo
1. docker pull qihong1222/my-private-repo
