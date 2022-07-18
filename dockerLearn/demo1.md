## 创建image pyramid

### pyramid.py

```python
import sys
def print_pyramid(level: int):
    for i in range(level):
        new_line_str = ''
        new_line_str += ' ' * (level - 1 - i)
        new_line_str += '*' * ((i+1) * 2 - 1)
        print(new_line_str)

input_level = int(sys.argv[1])
print_pyramid(input_level)
```



### Dockerfile

```shell
FROM python:3.7
COPY ./pyramid.py /pyramid.py
ENTRYPOINT ["python3", "pyramid.py"]
CMD ["5"]
```

### .dockerignore
```shell
__pycache__
env
```

### 运行命领


| 说明 |  命令  |
| :-- | --  |
| 构建image| docker image build . --tag pyramid |
| 运行  pyramid container | docker run pyramid | 
| 运行  pyramid container (默认是5) | docker run pyramid 10 |

