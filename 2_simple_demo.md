###上传第一张图片 

####一. 现在我们拥有什么？
&nbsp;&nbsp;&nbsp;&nbsp;做完了基本的注册和创建空间，终于要开始使用 upyun 了，我们现在手头上拥有什么了呢？    

+ 一个名字叫 upyunblog 的```图片空间```
+ 一个授予 upyunblog 的```操作员```    

&nbsp;&nbsp;&nbsp;&nbsp;是的，接下来，我们就要开始使用这个空间为我们的网站和应用注入强力的驱动了。

####二. 上传图片    
&nbsp;&nbsp;&nbsp;&nbsp;图片空间只能存储『图片文件』，首先我们要在图片空间中上传我们需要的图片。    
&nbsp;&nbsp;&nbsp;&nbsp;upyun 提供了两大种上传方式， 一种是```FTP```方式上传，一种是 ```API 接口```方式上传。    

+ API接口上传    
&nbsp;&nbsp;&nbsp;&nbsp;我们选择简单易懂的 Python 语言来完成我们的第一个上传操作。当然，还可以在又拍云的【[开发资源](http://wiki.upyun.com/index.php?title=%E5%BC%80%E5%8F%91%E8%B5%84%E6%BA%90)】中找到```API 文档```和各种语言的 SDK 例子，并且他们都是可以单独运行的。    
&nbsp;&nbsp;&nbsp;&nbsp; API 接口上传分为```标准 API 接口```上传和```表单 API 接口``` 上传。我们先来了解```标准 API 接口```上传。    
&nbsp;&nbsp;&nbsp;&nbsp;首先我们先来准备一下必要的参数：    

```
1.API 接口地址：
v1.api.upyun.com (电信)
v2.api.upyun.com (联通网通)
v3.api.upyun.com (移动铁通)
v0.api.upyun.com (自动判断）    <=======(我们习惯选择它)

2.空间名： upyun-blog-pic

3.用户(已授权)操作员：upyun

4.密码(已授权)：密码
```    

&nbsp;&nbsp;&nbsp;&nbsp;API 接口方式上传基于 http 协议。所以我们这里使用 put 方式上传文件到 upyun 的 API 接口。    
&nbsp;&nbsp;&nbsp;&nbsp;首先我们根据接口文档一个实现 http put 的 Python 方法    

```
def put(uri, value, checksum=False, headers=None):
    if headers is None:
        headers = {}
    headers['Mkdir'] = 'true'
    

```
