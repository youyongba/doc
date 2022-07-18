# Docker搭建gitbook

## 查找镜像
```shell
docker search -s 3 gitbook
```

## 安装gitbook镜像
```shell
docker pull fellah/gitbook
```

## 获取gitbook静态html文件
> /yourpath下需要有README.md和SUMMARY.md文件。

```shell
docker run -v /yourpath:/srv/gitbook -v /yourpath/html:/srv/html fellah/gitbook gitbook build . /srv/html
```

## 安装nginx

```shell
docker pull nginx
docker run --name my-nginx -v /yourpath/html:/usr/share/nginx/html -d -p 8080:80 nginx
```