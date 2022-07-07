---
marp: true
# theme: gaia | uncover
theme: gaia
# class: invert | lead
# class: invert
paginate: true
size: 16:9
header: "GitHub博客搭建"

footer: "菜鸟小洪互联网开发学习笔记"
# backgroundColor: #f2f2f2
# backgroundImage: url(https://img0.baidu.com/it/u=3023406692,921591711&fm=253&fmt=auto&app=138&f=PNG?w=500&h=281)

backgroundImage: "linear-gradient(to bottom, #f2f2f2, #e5e5e5)"
color: #1a1a1a
style: |
    section header {
        font-size:30px;
        color:#e56045;
    }
    section footer {
        font-size:30px;
        color:#999;
    }
    section::after {
        font-weight: bold;
        text-shadow: 1px 1px 0 #fff;
        font-size:30px;
        color:#999;
    }

    section h1,section h2,section h3,section h4,section h5,section h6,section h7  {
        color:#e56045;
    }

    section table th,section table td {
        border-color:#ccc;
    }

    section table thead th {
        color: white;
        background: #e56045;
    }

    section table tbody td {
        color: #4d4d4d;
        background: white !important ;
    }
    section pre code {
        background: #4d4d4d;
        drop-shadow:0,15px,20px,rgba(0,0,0,.4)
    }
---
<!-- _class: lead -->
<!-- _header: "" -->
# GitHub博客搭建

> 主要目的是未来能够快速的办理出文档，做一个有效的积累，所以尝试这个博客系统，它是依附于GitHub上的一个免费的博客系统，我个人觉得挺实用，所以分享出来一起学习

---
<!-- _class: lead -->
## 演示
![drop-shadow:0,5px,10px,rgba(0,0,0,.4) width:900px](./imgs/1.gif '微信扫码交流1')

---
<!-- _class: lead -->
## 目录
1. 下载vscode 编辑器非常重要
1. 注册登录
1. 开始搭建博客
1. 资源文件（比如说图片,视频，音频）
1. 代码

---

## 访问地址
- https://github.com/
    > 这个不需要解释，直接用这个链接访问就可以

---



## 下载vscode 编辑器非常重要
> vscode目前是最好用的代码编辑器，所以建议使用vscode来编辑代码，并且开源免费的
- https://code.visualstudio.com/

---
<!-- _class: lead -->
## 开始搭建博客
- 先创建一个Repositories
- 然后给自己的Repositories取一个名字，注意：名称格式最好为：用户名.github.io
- 创建内容
- 找到setting
- 找到Pages (在左侧栏)
- 看到绿色（如果看到的是蓝色还在更新需要等待一会）
- 创建子页面
- 关联子页面
---

### 先创建一个Repositories
![bg 95% drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/WX20220623-103507%402x.png?versionId=CAEQHhiBgIDY1tO5jBgiIGQyMmI4NGZiYjQ0ZjQ2NjI4NTNmOTU5OWVhY2Q0OTli '先创建一个Repositories')

---

### 然后给自己的Repositories取一个名字，注意：名称格式最好为：用户名.github.io。首页


![drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/2.png?versionId=CAEQHhiBgMDI0Ye6jBgiIGViNzUxM2RiMDdiMjRjMTE5ODAzN2E5YjgxNmYyYTI5 '然后给自己的Repositories取一个名字，注意：名称格式最好为：用户名.github.io')

---


### 创建内容

![bg auto width:1000px drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/3.png?versionId=CAEQHhiBgICz25K6jBgiIDhjZjY0MWFkZGYzNjQzNTZiOTA0ZDJlODZmNWU2MWQ0 '创建内容')


---
#### 创建内容 我个人通常这样

```bash
echo "# youyongba.github.io" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:youyongba/youyongba.github.io.git
git push origin HEAD
```

---

### 找到setting

![bg auto width:1000px drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/4.png?versionId=CAEQHhiBgMC75M26jBgiIDI0ZGQ1ZDE2Mjg1YzRlZDJhODhjZmJjZmNmNmQxMDNm '找到setting')

---

### 找到Pages (在左侧栏)

![bg auto width:900px drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/5.png?versionId=CAEQHhiBgMDssNq6jBgiIDUxYThiMDAxNzNlYzQ2OTA5ZDcxYjI2OTE2OTg4ZGRl '找到Pages')

---


### 看到绿色（如果看到的是蓝色还在更新需要等待一会）


![bg auto width:1200px drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/6.png?versionId=CAEQHhiBgICP1uK6jBgiIGVjMDg1ZTkyZWNkYjRjY2VhYmY2MjNlYmRkMjY1NmVj '找到Pages')


---

### 创建子页面

- 除了以上第2步不需要变成，不需要xxx.github.io,只需要用普通的仓库名称就可以。
- 第6步，在Source这个下边的选项将node改成master
- 成功后会获得到一个地址 比如： https://youyongba.github.io/GitHubBlog/

---

### 关联子页面
> 用vscode 打开首页的源文件



---

![width:800px  drop-shadow:0,15px,20px,rgba(0,0,0,.4)](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/7.png?versionId=CAEQHhiBgIDJ3ou7jBgiIDRmZTYzOTNmZGI4ZDRiM2FiMWVjYmJkZGM1NzIzYmYz '找到Pages')

---

## 资源文件（比如说图片）

> 存储一般大多数都是收费的，但是github有一个免费的方式。可以将图片存在里面。

- 可以在首页创建一个resources/images的文件夹，将图片放在里面，推送过去




---

## 资源文件（比如说图片）
### 如何访问图片

- https://github.com/youyongba/youyongba.github.io/blob/master/resources/images/githubblog.gif
    
- 将github.com --> raw.githubusercontent.com，在将blob删掉,会变成 --> https://raw.githubusercontent.com/youyongba/youyongba.github.io/master/resources/images/githubblog.gif




---

## 代码
### README.md
> 首页

```markdown

web开发笔记，用来记录自己的有效积累
* [介绍](README.md)

目录
* [github博客搭建](github_blog/readme.md)

```

---

### blog/README.md
> 子页面需要另外建立一个普通仓库

```md
# github博客搭建
## 访问地址
 - https://github.com/

## 演示
![](https://raw.githubusercontent.com/youyongba/youyongba.github.io/master/resources/images/githubblog.gif '微信扫码交流1')

## 下载vscode 编辑器非常重要
> 下面的网站下载
 - https://code.visualstudio.com/

```


