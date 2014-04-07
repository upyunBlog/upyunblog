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
&nbsp;&nbsp;&nbsp;&nbsp;首先我们可以去【[开发资源](http://wiki.upyun.com/index.php?title=%E5%BC%80%E5%8F%91%E8%B5%84%E6%BA%90)】中找到适合自己的 sdk 代码。任何一个sdk 下载下来我们都会发现有一个已经写好的供调用的接口方法，比如 upyun.py；upyun.php；upyun.java 等等。这样一来，我们就不用重复造轮子了。    
&nbsp;&nbsp;&nbsp;&nbsp;下面我们来看一个 Python 调用这个已经写好的 upyun.py的例子：    

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import upyun

# ------------------ CONFIG ---------------------
BUCKETNAME = '空间名字'
USERNAME = '操作员名'
PASSWORD = '操作员密码'
# -----------------------------------------------
```

&nbsp;&nbsp;&nbsp;&nbsp;在文件的开始我们先填写一下上传所必需的变量，那就是我们前面提到的很重要的```空间名```，```操作员名```，```操作员密码```。    
&nbsp;&nbsp;&nbsp;&nbsp;接下来，我们开始调用 upyun.py 里面的方法来上传图片：    

```
def run():
    
    up = upyun.UpYun(BUCKETNAME, USERNAME, PASSWORD, timeout=30,
                     endpoint=upyun.ED_AUTO)
    rootpath = '/upyun-python-sdk/'
    
    try:
        print "Uploading a new picture to upyun from a file"
        headers = {"x-gmkerl-rotate": "180"}
        with open('cat.png', 'rb') as f:
            res = up.put(footpath + 'tac.png', f,
                         checksum=False, headers=headers)
        print "OKED"
    
    except upyun.UpYunServiceException as se:
        print "failed\n"
        print "Except an UpYunServiceException ..."
        print "HTTP Status Code: " + str(se.status)
        print "Error Message:    " + se.msg + "\n"
        if se.err:
            print se.err
    except upyun.UpYunClientException as ce:
        print "failed\n"
        print "Except an UpYunClientException ..."
        print "Error Message: " + ce.msg + "\n"
        
        
if __name__ == '__main__':
    run()
    
```

&nbsp;&nbsp;&nbsp;&nbsp;怎么样，借助强大的 upyun.py 接口方法，上传是不是非常简单的一件事情？我们需要做的，只是传递一下相关的参数来告诉服务器这个图片的存放路径，是否旋转、裁剪等等就行了。下面我们简单的讲一下上面的参数。        

1.```rootpath```这个变量是指定文件上传到空间所在的目录。
2. ```headers```这个里面的[x-gmkerl-rotate](http://wiki.upyun.com/index.php?title=HTTP_REST_API%E6%8E%A5%E5%8F%A3#.E5.9B.BE.E7.89.87.E5.A4.84.E7.90.86.E6.8E.A5.E5.8F.A3) 指的是图片处理的参数，在图片上传的时候我们可以往 http headers 里面添加一些参数来告诉服务器如何处理上传的图片。
3.```endpoint```是上传的 API 接口地址。通常我们的上传 [API 接口地址](http://wiki.upyun.com/index.php?title=API%E4%BD%BF%E7%94%A8%E7%AE%80%E4%BB%8B)都是使用*v0.api.upyun.com*。     
4.```checksum``` 这个 checksum 布尔值是判断是否执行 MD5校验的参数，开启 MD5校验能检查服务器接收到文件和本地文件的数据是否一致。    

&nbsp;&nbsp;&nbsp;&nbsp;如果发现上传的时候 API 接口返回了错误， 这时我们就可以直接参考[错误信息表](http://wiki.upyun.com/index.php?title=HTTP_REST_API%E6%8E%A5%E5%8F%A3#.E6.A0.87.E5.87.86API.E9.94.99.E8.AF.AF.E4.BB.A3.E7.A0.81.E8.A1.A8)来查看大概是出现了什么错误。

&nbsp;&nbsp;&nbsp;&nbsp;然后我们来看一下如何查看我们已经上传的图片文件呢？很简单，我们可以通过 [FTP](http://wiki.upyun.com/index.php?title=FTP%E6%8E%A5%E5%8F%A3) 登录到空间直观的看一下我们上传的文件。    
![Alt bucketpic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/FTPpic.png)    
没错儿，我们能发现空间目录下面已经存在这个图片了。FTP 的登录方法为：   

``` 
1.FTP 工具：（比如 filezilla）    
2.FTP 地址为：v0.ftp.upyun.com    
3.FTP 的用户名为：「操作员名/空间名」（注意：「操作员名+/+空间名」都是要填写的）    
4.FTP 的操作员密码
```
&nbsp;&nbsp;&nbsp;&nbsp;还有一种方法是使用[外链](http://wiki.upyun.com/index.php?title=%E8%8E%B7%E5%8F%96%E6%96%87%E4%BB%B6%E5%A4%96%E9%93%BE%E5%9C%B0%E5%9D%80)方式来在浏览器中查看文件是否已经上传成功。    
>外链的是空间的```域名```(```默认域名```)加上远程文件路径行程的访问链接。    

比如我们刚刚上传的那张图片就可以试着访问一下：[http://upyun-blog-pic.b0.upaiyun.com/upyun-python-sdk/tac.png](http://upyun-blog-pic.b0.upaiyun.com/upyun-python-sdk/tac.png)就会看见下面的图片。没错，我们在程序中使用了旋转180度的参数，所以现在看上去就是倒立的喵星人了。    
![Alt tac.png](http://upyun-blog-pic.b0.upaiyun.com/upyun-python-sdk/tac.png)

+ FTP 方式上传。    
&nbsp;&nbsp;&nbsp;&nbsp;FTP 方式上传更简单，只要准备好一个 FTP 工具，就可以填写好我们上面说过的信息以后就可以直接单个或者批量上传文件了。

&nbsp;&nbsp;&nbsp;&nbsp;到目前为止，我们的一个快速的上传就完成了，接下来我们可以使用这个图片的外链插入到我们的网站或者 APP 应用中，全国和北美自建的 CDN 网络基础下，打开它可是非常的快速。    

####三. 接下来讲什么呢？    
&nbsp;&nbsp;&nbsp;&nbsp;接下来，我们将看一下文件空间、图片空间和 CDN 空间三者之间的差别和优势。    
<br />
--NEXT--

【[UPYUN](https://www.upyun.com) © 2014 署名-非商业性使用-禁止演绎】