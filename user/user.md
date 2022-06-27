# 用户接口

## 获取用户列表
### 接口地址

> get


- https://api.xxx.com/user/user

### header

```javascript
{
    "Authorization": "Bearer xxx"
}
```

### 参数

字段 | 类型  | 说明
:--- | :--- | :---
userid | Number | 用户id

```javascript 
{
    "userid": 1
}
```

### 响应

字段 | 类型  | 说明
:--- | :--- | :---
user | String | 用户名
avatar | String | 用户头像

```javascript
{
    "status": true,
    "msg": "成功",
    "data": [{
        "avatar": "https://img.xxx.com/xxx.png",
        "user": "小洪"
    },{
        "avatar": "https://img.xxx.com/xxx.png",
        "user": "小洪1"
    }]
}
```
