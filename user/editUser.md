# 用户接口

## 获取编辑用户
### 接口地址

> get

- https://api.xxx.com/user/edit

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

#### 成功
```javascript
{
    "status": true,
    "msg": "成功",
}
```
#### 失败
```javascript
{
    "status": false,
    "msg": "少传一个字段",
}
```
