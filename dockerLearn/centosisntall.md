# centos7安装Docker详细步骤
## 安装前必读
> 在安装 Docker 之前，先说一下配置，我这里是Centos7 Linux 内核：官方建议 3.10 以上，3.8以上貌似也可。
注意：本文的命令使用的是 root 用户登录执行，不是 root 的话所有命令前面要加

### 查看当前的内核版本

```shell
uname -r
```



### 使用 root 权限更新 yum 包（生产环境中此步操作需慎重，看自己情况，学习的话随便搞）

```shell
yum -y update
```

### 卸载旧版本（如果之前安装过的话）

```shell
yum remove docker  docker-common docker-selinux docker-engine
```



## 安装Docker的详细步骤

### 安装需要的软件包， yum-util 提供yum-config-manager功能，另两个是devicemapper驱动依赖

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```


### 设置 yum 源
> 设置一个yum源，下面两个都可用

```shell
yum-config-manager --add-repo http://download.docker.com/linux/centos/docker-ce.repo（中央仓库）

yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo（阿里仓库）
```


### 选择docker版本并安装 
#### 查看可用版本有哪些

```shell
yum list docker-ce --showduplicates | sort -r
```


#### 选择一个版本并安装：yum install docker-ce-版本号

```shell
yum -y install docker-ce-18.03.1.ce
```


### 启动 Docker 并设置开机自启

```shell
systemctl start docker
systemctl enable docker
```


## 按装docker-compose

### 下载docker compose指定的版本

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```


### 赋予docker-compose二进制文件应用可执行权限
```shell
sudo chmod +x /usr/local/bin/docker-compose
```
### 创建链接

```shell
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```


### 最后通过查看版本检验是否安装完成

```shell
docker-compose --version
```


