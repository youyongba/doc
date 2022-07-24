# Express + Mongodb + Redis
## express 生成器 官方文档
- https://www.expressjs.com.cn/starter/generator.html

## 生成ejs板板的文件 express -e

```shell
express -e xxx #xxx为项目名称
```

## 修改package.json

```
{
  "name": "project",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "nodemon ./bin/www"  // node 换成 nodemon
  },
  "dependencies": {
    "cookie-parser": "~1.4.4",
    "debug": "~2.6.9",
    "ejs": "~2.6.1",
    "express": "~4.16.1",
    "http-errors": "~1.6.3",
    "morgan": "~1.9.1"
  }
}


```


## mongodb 数据库安装

### 官网下载
- https://www.mongodb.com/
- https://www.mongodb.com/try/download/community

### 安装
```shell
tar xvf mongodb-macos-x86_64-6.0.0.tgz
mv mongodb-macos-x86_64-6.0.0 mongodb
mkdir ~/bin
mv mongodb ~/bin
```

### 修改环境变量 编辑 .zshrc 文件

#### 命令
```shell
vi ~/.zshrc
```
#### 编辑
```shell
# 复制 这段话
export PATH=$HOME/bin:/usr/local/bin:/$HOME/bin/mongodb/bin:$PATH

source ~/.zshrc
```

#### 查看是否安装成功
```shell
mongod -version
```

#### 创建mongodb 数据文件夹data  日志文件夹
```shell
cd ~/bin/mongodb/
mkdir {data,log}
```

#### 运行

```shell
# 当前项目，在实践项目里不要在项目目录里搭建
mongod --fork --dbpath ~/bin/mongodb/data --logpath ~/bin/mongodb/log/test.log --logappend


```

##### 参数说明
| 参数名 | 说明 |
| :--- | ---: |
| --fork | 后台运行|
| --dbpath | 数据库数据存储录径 |
| --logpath | 日志存储录径 |
| --logappend | 指定它的方式是添加 而不是每次都重写 |







#### 通过浏览器检查是否启动
```shell
http://127.0.0.1:27017/
```


#### 关闭数据库
1. 运行中关闭
    ```shell
    ctrl+C
    ```

1. 使用数据库命令关闭
    ```shell
    mongod -f ~/bin/mongodb/data/db.conf
    ```

1. 登录数据库
    

    ```shell
    > use admin;
    > db.shutdownServer();
    ```

1. 使用mongodb命令关闭
    ```shell
    mongod  --shutdown  --dbpath ~/bin/mongodb/data/
    ```

#### 创建mongodb.conf

```shell
port=27017
dbpath=/Users/qihong/bin/mongodb/data
logpath=/Users/qihong/bin/mongodb/log/test.log
#使用追加的方式写日志
logappend=true
#以守护程序的方式启用，在后台运行
fork=true
#最大同时连接数
maxConns=100
#启用验证
#auth=true
#每次写入会记录一条操作日志（通过journal可以重新构造出写入的数据）
journal=true
#存储引擎有mmapv1、wiretiger、mongorocks，即使宕机，启动时wiredtiger会先将数据恢复到最近一次的checkpoint点，然后重放后续的journal日志来恢复
storageEngine=wiredTiger
#这样就可外部访问了，例如从win10中去连虚拟机中的MongoDB
bind_ip = 0.0.0.0
```

- 启动服务
    ```shell
    mongod -f ./mongodb.conf
    ```




#### mongodb客户端连接

```shell
mongo
```


#### 常用的用户操作

```shell
#创建超级管理员
use admin;
db.createUser({user:"root",pwd:"root2020!",roles:["root"]})
#修改自己密码
use admin
db.changeUserPassword("username", "xxx")
#查看用户信息
db.runCommand({usersInfo:"userName"})
#创建普通管理员
> use admin;
switched to db admin
> db.createUser({user:"admin",pwd:"root123456",roles:["userAdminAnyDatabase"]});
Successfully added user: { "user" : "admin", "roles" : [ "userAdminAnyDatabase" ] }
> exit
#创建普通用户，只对testdb进行读写
> use testdb;
switched to db testdb
> db.createUser({user:"syhdbtest",pwd:"syhdbtest!",roles:[{role:"readWrite",db:"syhmongodbtest"}]});
> exit
#不用重启服务直接进入
> use testdb;
switched to db testdb
> db.auth("test","test123");
1
> db.user.insert({name:"joy1",city:"zhengzhou",phone:"123456"});
WriteResult({ "nInserted" : 1 })
> db.user.find();
{ "_id" : ObjectId("5c4ad0325cdcfe8e8ad6257f"), "name" : "joy", "city" : "zhengzhou", "phone" : "123456" }
> exit
#正常关闭mongodb服务
> use admin;
> db.shutdownServer();
```

#### mongodb第三方客户端
- 下载地址
    - https://studio3t.com/download-thank-you/?OS=osx



#### 数据库表 users

```shell
use project
db.createCollection("users")
show collections
db.users.insertOne({name:'geekxia'})
db.users.find()

```


### express安装 mongodb

#### 址址

- npmjs.com/package/mongodb

#### express在项目里操作

1. 创建目录modal和index.js
    ```shell
    mkdir modal
    cd modal
    touch index.js
    ```

1. index.js
    ```javascript
    var MongoClient = require('mongodb').MongoClient

    var url = 'mongodb://localhost:27017'
    var dbName = 'project'

    function connect() {
        MongoClient.connect(url, function (err, client) {
            if (err) {
                console.log('连接数据库错误：',error);
            }
        })
    }
    ```





