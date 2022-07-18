# 创建image volume

## server.py
```python
from flask import Flask, render_template
import json

app = Flask(__name__)

@app.route('/book')
def json_file():
    file=open('volume_data/book.json')
    json_data=json.load(file)
    return json_data

@app.route('/')
def home():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=3000)

```

## Dockerfile

```sh
FROM python:3.7
COPY . /app
WORKDIR /app
RUN ["pip3", "install", "-r", "requirements.txt"]
EXPOSE 3000
CMD ["python3", "server.py"]


```


## templates/index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>简单的例子</title>
</head>
<body>
    <h1>标题</h1>
    <div id="content-info"></div>
    <script>
        fetch('http://localhost:3000/book')
            .then(response => response.json())
            .then(data => {document.querySelector('#content-info').innerText = data.title})
    </script>
</body>
</html>
```


## volume_data/book.json
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>简单的例子</title>
</head>
<body>
    <h1>标题</h1>
    <div id="content-info"></div>
    <script>
        fetch('http://localhost:3000/book')
            .then(response => response.json())
            .then(data => {document.querySelector('#content-info').innerText = data.title})
    </script>
</body>
</html>
```

## requirements.txt

```sh
flash==1.0.3
flask-cors==3.0.8

```

## 命令

| 说明 |  命令  |
| :-- | --  |
|生成image|docker build . --tag volume-app-frontend |
|启动container | docker run -p 3000:3000 volume-app-frontend |



### bindMount 方式命令

| 说明 |  命令  |
| :-- | --  |
|启动container | docker run -p 3000:3000 -v local_folder_path: /app/volume_data  volume-app-frontend |

> 用pwd 来查看当前所在的目录 替换 local_folder_path


## volume 方式命领

| 说明 |  命令  |
| :-- | --  |
|创建 volume | docker volume create book-data |
|查看创建的 volume|docker volume ls|
|查看 volume 存储信息 | docker volume inspect book-data|
| 启动container | docker run -p 3000:3000 -v book-data:/app/volume_data volume-app-frontend|
| 启动container 数据映射 | docker run -v book-data:/book-data -it ubuntu|

```json
[
    {
        "CreatedAt": "2022-06-20T15:51:02Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/book-data/_data",
        "Name": "book-data",
        "Options": {},
        "Scope": "local"
    }
]
```