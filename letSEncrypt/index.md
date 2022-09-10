# Centos通过acme申请Let’s Encrypt通配符HTTPS证书-简单粗暴


## 准备资料
### 域名租用地址
- https://www.quyu.net/

### 云主机
- https://zanyun.hk/

## 为什么要用https

### 比如我想在同域下做多个应用
- https://m.24os.cn
- https://www.24os.cn
- https://admin.24os.cn
- https://api.24os.cn
- ...

### 还有很多
> 比如 gitlab、jenkins、jira、Easy-Mock等

### 有些功能不是https的做不了

- 小程序后端接口
- PWA（Progressive Web App）渐进式网页应用
- webRTC
- ...


## 参考网址

- https://blog.hlogc.com/2019/07/19/centos%E9%80%9A%E8%BF%87acme%E7%94%B3%E8%AF%B7lets-encrypt%E9%80%9A%E9%85%8D%E7%AC%A6https%E8%AF%81%E4%B9%A6-%E7%AE%80%E5%8D%95%E7%B2%97%E6%9A%B4/

## 扩容(中间出现了根分区满了需要扩容)
> 如果遇到根分区满了参考下面的网址
- https://www.cnblogs.com/Agnostida-Trilobita/p/11434943.html

## 运行命令

```shell
sudo certbot certonly -d 24os.cn -d *.24os.cn --manual --preferred-challenges dns --server https://acme-v02.api.letsencrypt.org/directory
```




## 测试txt记录是否解释成功

### 中间遇到些问题

- 原来dig命令属于bind-utils工具包。安装这个工具包后就可以使用dig了
- dig全称"domain information groper"，它是查询DNS的工具，显示DNS域名服务器的回应，主机地址信息

### 运行命令
> 检测是否生效
```shell
yum -y install bind-utils
dig _acme-challenge.24os.cn txt



[root@v1 ~]#dig _acme-challenge.24os.cn txt

; <<>> DiG 9.10.6 <<>> _acme-challenge.24os.cn txt
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7793
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;_acme-challenge.24os.cn.	IN	TXT

;; ANSWER SECTION:
_acme-challenge.24os.cn. 600	IN	TXT	"DN_fCYq2Kog2FW4jAc-f5H_vzBkNTyX9095KJhkIwms"
_acme-challenge.24os.cn. 600	IN	TXT	"5GIBihZj5uTcba2AMcxPLEHdC1VCU0kI5djXXYm4lwY"

;; Query time: 1797 msec
;; SERVER: 192.168.101.1#53(192.168.101.1)
;; WHEN: Fri Sep 09 22:54:30 CST 2022
;; MSG SIZE  rcvd: 164
```

#### 出现表示成功
```shell
;; ANSWER SECTION:
_acme-challenge.24os.cn. 600	IN	TXT	"DN_fCYq2Kog2FW4jAc-f5H_vzBkNTyX9095KJhkIwms"
_acme-challenge.24os.cn. 600	IN	TXT	"5GIBihZj5uTcba2AMcxPLEHdC1VCU0kI5djXXYm4lwY"
```

之后就下一步下一步就好了

## nginx 启动和停止
> 需要根据自己nginx按装和配置

```shell
cd  /usr/local/nginx/
./sbin/nginx -s stop
./sbin/nginx -s reload
./sbin/nginx -c ./conf/nginx.conf
```


### nginx 配置文件
```nginx
server {
    server_name xxx.com;
    listen 443 http2 ssl;
    ssl on;
    ssl_certificate /etc/cert/xxx.cn/fullchain.pem;
    ssl_certificate_key /etc/cert/xxx.cn/privkey.pem;
    ssl_trusted_certificate  /etc/cert/xxx.cn/chain.pem;

    location / {
      proxy_pass http://127.0.0.1:6666;
    }
}

```

### nodejs 应用

```javascript
//主站
var http = require('http');
http.createServer(function(req,res){
	res.write('<head><meta charset="utf-8"></meta></head>');
	res.write("=====主站https://www.24os.cn=====");
	res.end();
}).listen(8801)
```


```javascript
//M站
var http = require('http');
http.createServer(function(req,res){
        res.write('<head><meta charset="utf-8"></meta></head>');
        res.write("=====m站https://m.24os.cn=====");
        res.end();
}).listen(8802);

```


## 查找和关闭进程
```shell
ps -ef | grep node
kill -9 [进程id]
```