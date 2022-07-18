# harbor使用
> 以osx系统为例，其它系统可以用find / -name "daemon.json" 搜索这个配置文件



## 编辑
```shell
 vi ~/.docker/daemon.json
```

## 添加配置文件
```json
{
  "builder" : {
    "gc" : {
      "enabled" : true,
      "defaultKeepStorage" : "20GB"
    }
  },
  "registry-mirrors": ["https://q2gr04ke.mirror.aliyuncs.com"], //镜像加速源。这里是阿里的
  "insecure-registries": [
    "http://youyong.ba:8088"
  ], //不安全的registries。自己的私有仓库也填在里边
  "experimental" : false,
  "features" : {
    "buildkit" : true
  }
}

```

## 在Harbor界面上点击新建项目，新建一个项目仓库
> 如：xiaohong




## 登录自己的仓库
 docker login youyong.ba:8088

## 推送image到私有仓库

```shell
docker build . --tag pyramid:v1.0.0
docker push youyong.ba:8088/xiaohong/pyramid:v1.0.0
```

## 从私有仓库拉去image

```shell
docker pull youyong.ba:8088/xiaohong/pyramid:v1.0.0
```