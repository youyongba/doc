# mkcert + nginx 搭建https

## 价值
> 不止以下内容需要https访问，在web领域几乎成了标配

- 小程序后端接口
- PWA（Progressive Web App）渐进式网页应用
- webRTC
- ...

## 环境
- MacBook OSX

## 所需资源
- brew
- vscode
- nginx
- mkcert

## mkcert 安装

```shell
brew install mkcert
# brew install nss
brew install nginx
```

## 生成根证书
> 通过“钥匙串访问.app”搜索mkcert，并信任证书。

```shell
mkcert -install
```

## 修改hosts



```shell
sudo vi /etc/hosts

```

### /etc/hosts 文件内容

```shell
127.0.0.1       xxx.com
127.0.0.1       www.xxx.com
127.0.0.1       app.xxx.com
```


## 生成个人证书

```shell
mkcert my.com localhost 127.0.0.1 xxx.com www.xxx.com app.xxx.com
```

- 证书文件在执行目录中，成功创建之后，会在该目录下生成如下两个文件
    - 证书 XXX.pem
    - 私钥 XXX-key.pem





## nginx 配置

```shell

/opt/homebrew/etc/nginx/nginx.conf #nginx配置文件
/opt/homebrew/etc/nginx/servers/app.conf #应用配置 需要新建app.conf 原则是任意的
/opt/homebrew/var/www    # 网站根目录

```


### /opt/homebrew/etc/nginx/nginx.conf 配置文件内容

```javascript

server {
        listen       443 ssl;
        server_name  xxx.com;

        #证书
        ssl_certificate /Users/qihong/conf/nginx/cert/my.com+5.pem;
        #私钥
        ssl_certificate_key /Users/qihong/conf/nginx/cert/my.com+5-key.pem;

#       ssl_certificate      cert.pem;
#       ssl_certificate_key  cert.key;

        ssl_session_cache    shared:SSL:1m;
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers  on;

        location / {
            root   html;
            index  index.html index.htm;
        }
    }
    include servers/*;

```



### app.conf 文件配置

```shell
server {
        listen 443;

        server_name app.xxx.com;

         location / {
                 proxy_pass http://127.0.0.1:6006;
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_redirect http:// $scheme://;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         }
}
```


### nginx 运行
```shell
brew services start nginx
```


## 局域网参考下面的文章，我不想演示了（也很简单）
> 一般是指测试服务器和预发服务器配置
- https://zhuanlan.zhihu.com/p/379501905