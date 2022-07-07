# Docker 搭建 easy-mock
> 以下是我验证的方法通过，不见得所有环境都起作用

## 新建目录

|命令| 说明 |
|:-- | :--- |
|mkdir -p data/db|数据库文件存放地址，根据需要修改为本地地址 |
|mkdir -p data/redis|redis 数据文件存放地址，根据需要修改为本地地址 |
|mkdir -p logs| 日志地址，根据需要修改为本地地址 |


## docker-compose.yml

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

## 命令

|命令| 说明|
|:--| :-- |
|docker-compose up| 启动|
|docker-compose stop| 停止 |
|docker-compose start| 开始 |


