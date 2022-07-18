## 创建image backend
### server.py
```python 
from flask import Flask, render_template
from flask_cors import CORS # need to mention
import json

app = Flask(__name__)
CORS(app)

@app.route('/book')
def json_file():
    file = open('./book.json')
    json_data=json.load(file)
    return json_data

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### Dockerfile

```shell
# asdfasdf
FROM python:3.7
COPY . /app
WORKDIR /app
RUN ["pip3", "install", "-r", "requirements.txt"]
EXPOSE 5000
CMD ["python3", "server.py"]
```


### book.json

```json
{
    "title": "小洪学习笔记-标题",
    "description": "小洪学习笔记-描述",
    "link": "youyongba.github.io/doc/html"
}

```

### requirements.txt

```shell
flash==1.0.3
flask-cors==3.0.8
```

### 命令


| 说明 |  命令  |
| :-- | --  |
|生成image|docker build . --tag web-app-backend |
|启动container |docker run -p 4000:5000 web-app-backend |

> -p 4000:5000
- 4000为本地端口，5000是container
