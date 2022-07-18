# 创建image frontend

## server.py

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=3000)
```

## Dockerfile
```shell
FROM python:3.7
COPY . /app
WORKDIR /app
RUN ["pip3", "install", "-r", "requirements.txt"]
EXPOSE 3000
ENTRYPOINT ["python3", "server.py"]

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
        fetch('http://localhost:4000/book')
            .then(response => response.json())
            .then(data => {document.querySelector('#content-info').innerText = data.title})
    </script>
</body>
</html>
```

## requirements.txt
```shell
flash==1.0.3
flask-cors==3.0.8
```


## 命令

| 说明 |  命令  |
| :-- | --  |
|生成image|docker build . --tag web-app-frontend |
|启动container |docker run -p 3000:3000 web-app-frontend |

