## docker compose demo


### docker-compose.yml

```yml
version: "3.9"
services:
  backend:
    build: ./lession3_backend
    ports: 
      - "4000:5000"
    volumes:
      - ./lession3_backend:/app
  
  frontend:
    build: ./lession4_frontend
    ports:
      - "3000:3000"
```


### 命令


| 说明 |  命令  |
| :-- | --  |
|运行  compose 命令 | docker-compose up |
|停止  compose 命令 | docker-compose down |


## docker compose demo2 redis结合

### server.py

```python
from flask import Flask, render_template
import redis
import os
REDIS_HOST = os.environ.get('REDIS_HOST', '0.0.0.0')

app = Flask(__name__)
cache = redis.Redis(host = REDIS_HOST, port = 6379, db = 0)
cache.set('hits', 0)

@app.route('/')
def get_data():
    hit_num = cache.incr('hits')
    return f'I have been seen {hit_num} times.\n'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port = 5000)
```

### requirements.txt

```sh
flash==1.0.3
flask-cors==3.0.8
redis==4.3.3
```

### Dockerfile
```sh
FROM python:3.7
COPY . /app
WORKDIR /app
RUN ["pip3", "install", "-r", "requirements.txt"]
EXPOSE 5000
CMD ["python3", "server.py"]

```

### docker-compose.yml   （在上一级目录创建）

```yml
version: "3.9"
services:
  redis-server:
    image: "redis"

  backend:
    environment:
      - REDIS_HOST=redis-server
    build: ./backend
    ports:
      - "5000:5000"

```

### 命令
| 说明 |  命令  |
| :-- | --  |
|运行  compose 命令 | docker-compose up |
|停止  compose 命令 | docker-compose down |
