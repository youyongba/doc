# Docker 搭建 easy-mock
> 以下是我验证的方法通过，不见得所有环境都起作用

## 新建目录

|命令| 说明 |
|:-- | :--- |
|mkdir -p data/db|数据库文件存放地址，根据需要修改为本地地址 |
|mkdir -p data/redis|redis 数据文件存放地址，根据需要修改为本地地址 |
|mkdir -p logs| 日志地址，根据需要修改为本地地址 |


## 新建docker-compose.yml

```yml
version: "3.3"
services:
  mongodb:
    image: mongo:3.4
    privileged: true
    volumes:
      - type: bind
        source: app/data/db # 数据库文件存放地址，根据需要修改为本地地址
        target: /data/db
  redis:
    image: redis:4.0.6
    privileged: true
    command: redis-server --appendonly yes
    volumes:
      - type: bind
        source: app/data/redis # redis 数据文件存放地址，根据需要修改为本地地址
        target: /data
  web:
    image: easymock/easymock:1.6.0
    privileged: true
    command: /bin/bash -c "npm start"
    links:
      - mongodb:mongodb
      - redis:redis
    ports:
      - 7300:7300
    volumes:
      - type: bind 
        source: app/logs # 日志地址，根据需要修改为本地地址
        target: /home/easy-mock/easy-mock/logs
      - type: bind
        source: ./production.json # 配置地址，请使用本地配置地址替换
        target: /home/easy-mock/easy-mock/config/production.json

```

## 新建production.json

```json
{
    "port": 7300,
    "host": "0.0.0.0",
    "pageSize": 30,
    "proxy": false,
    "db": "mongodb://mongodb/easy-mock",
    "unsplashClientId": "",
    "redis": {
      "keyPrefix": "[Easy Mock]",
      "port": 6379,
      "host": "redis",
      "password": "",
      "db": 0
    },
    "blackList": {
      "projects": [],
      "ips": []
    },
    "rateLimit": {
      "max": 1000,
      "duration": 1000
    },
    "jwt": {
      "expire": "14 days",
      "secret": "shared-secret"
    },
    "upload": {
      "types": [".jpg", ".jpeg", ".png", ".gif", ".json", ".yml", ".yaml"],
      "size": 5242880,
      "dir": "../public/upload",
      "expire": {
        "types": [".json", ".yml", ".yaml"],
        "day": -1
      }
    },
    "ldap": {
      "server": "",
      "bindDN": "",
      "password": "",
      "filter": {
        "base": "",
        "attributeName": ""
      }
    },
    "fe": {
      "copyright": "",
      "storageNamespace": "easy-mock_",
      "timeout": 25000,
      "publicPath": "/dist/"
    }
  }
```

## 命令

|命令| 说明|
|:--| :-- |
|docker-compose up|$\color{#FF3030}{red}$ 启动|
|docker-compose stop| 停止 |
|docker-compose start| 开始 |


