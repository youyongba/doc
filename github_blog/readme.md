# github博客搭建
## 访问地址
- https://github.com/


## 演示

![](https://raw.githubusercontent.com/youyongba/youyongba.github.io/master/resources/images/githubblog.gif '微信扫码交流1')



## 下载vscode 编辑器非常重要
> 下面的网站下载
- https://code.visualstudio.com/

## 注册登录
> 略

## 开始搭建博客

1. 先创建一个Repositories

![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/WX20220623-103507%402x.png?versionId=CAEQHhiBgIDY1tO5jBgiIGQyMmI4NGZiYjQ0ZjQ2NjI4NTNmOTU5OWVhY2Q0OTli '微信扫码交流')


2. 然后给自己的Repositories取一个名字，注意：名称格式最好为：用户名.github.io

![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/2.png?versionId=CAEQHhiBgMDI0Ye6jBgiIGViNzUxM2RiMDdiMjRjMTE5ODAzN2E5YjgxNmYyYTI5 '创建Repositories')

3. 创建内容


![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/3.png?versionId=CAEQHhiBgICz25K6jBgiIDhjZjY0MWFkZGYzNjQzNTZiOTA0ZDJlODZmNWU2MWQ0 '创建内容')


```bash
echo "# youyongba.github.io" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch main
git remote add origin ssh://github.com/youyongba/youyongba.github.io.git
git push  origin main
```

4. 找到setting


![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/4.png?versionId=CAEQHhiBgMC75M26jBgiIDI0ZGQ1ZDE2Mjg1YzRlZDJhODhjZmJjZmNmNmQxMDNm '找到setting')

5. 找到Pages (在左侧栏)

![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/5.png?versionId=CAEQHhiBgMDssNq6jBgiIDUxYThiMDAxNzNlYzQ2OTA5ZDcxYjI2OTE2OTg4ZGRl '找到Pages')


6. 看到绿色（如果看到的是蓝色还在更新需要等待一会）


![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/6.png?versionId=CAEQHhiBgICP1uK6jBgiIGVjMDg1ZTkyZWNkYjRjY2VhYmY2MjNlYmRkMjY1NmVj '找到Pages')


7. 创建子页面
    - 除了以上第2步不需要变成，不需要xxx.github.io,只需要起被通的仓库名称就可以。
    - 第6步，在Source这个下边的选项将node改成master
    - 成功后会获得到一个地址 比如： https://youyongba.github.io/GitHubBlog/
8. 关联子页面
    - 用vscode 打开源文件


![](https://youyongba.oss-cn-beijing.aliyuncs.com/图片/7.png?versionId=CAEQHhiBgIDJ3ou7jBgiIDRmZTYzOTNmZGI4ZDRiM2FiMWVjYmJkZGM1NzIzYmYz '找到Pages')


## 资源文件（比如说图片）
> 存储一般大多数都是收费的，但是github有一个免费的方式。可以将图片存在里面。

- 可以在首页创建一个resources/images的文件夹，将图片放在里面，推送过去

-  如何访问图片

    https://github.com/youyongba/youyongba.github.io/blob/master/resources/images/githubblog.gif
    
    1. 将github.com --> raw.githubusercontent.com，在将blob删掉,会变成https://raw.githubusercontent.com/youyongba/youyongba.github.io/master/resources/images/githubblog.gif

---        
## 代码
### README.md
> 首页

```md
web开发笔记，用来记录自己的有效积累
* [介绍](README.md)

目录
* [github博客搭建](github_blog/readme.md)
```

### blog/README.md
> 子页面

```markdown
# github博客搭建
## 访问地址
 - https://github.com/

## 演示
![](https://raw.githubusercontent.com/youyongba/youyongba.github.io/master/resources/images/githubblog.gif '微信扫码交流1')

## 下载vscode 编辑器非常重要
> 下面的网站下载
 - https://code.visualstudio.com/
```






