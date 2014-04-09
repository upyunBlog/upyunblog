&nbsp;&nbsp;&nbsp;&nbsp;云存储行业是一个新兴并且高速发展的事物，我们在为自己的网站和应用准备着手接入云存储服务的时候，是否会面对着云存储服务数量众多的帮助文档而不知道从何开始了解呢？所以我们急需要一些由浅入深的笔记，来更迅速的了解云存储的服务。
####一. 注册
&nbsp;&nbsp;&nbsp;&nbsp;在让 upyun 成为强力的后盾之前，我们需要注册一个```云存储帐号```。 注册帐号很简单，只要访问[www.upyun.com](http://www.upyun.com)，然后猛击右上角的```免费使用```，我们就会跳转到下面这个简洁的注册页面。  
 ![Alt signup](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/signup.png)    
 &nbsp;&nbsp;&nbsp;&nbsp;这个页面再简单不过了，填写的时候了解一下以下几点就可以了。
 &nbsp;&nbsp;&nbsp;&nbsp;1. *号务必要填写正确，方便以后与 upyun 之间联系。    
 &nbsp;&nbsp;&nbsp;&nbsp;2. 企业和个人类型享受同样的服务。    
 &nbsp;&nbsp;&nbsp;&nbsp;3. 如果有任何条款疑问，可以参考【[又拍云存储服务条款](https://www.upyun.com/tos.html)】。
 
&nbsp;&nbsp;&nbsp;&nbsp;所有的信息都填写完毕并且确认无误以后，就可以猛击提交。 跳转到登录界面，输入刚刚填写的用户名和密码后，upyun 后台的大门就此打开。    
 
####二. 登录和验证    

&nbsp;&nbsp;&nbsp;&nbsp;在简洁至上的 upyun 登录界面输入```云存储帐号```和```登录密码```以后，进入后台我们首先看到的是验证手机号码的界面。    
![Alt Certification](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/certification.png)
 &nbsp;&nbsp;&nbsp;&nbsp;点击```发送验证码```， upyun 将会发送一条六位数字的验证码到手机上，然后验证通过就可以看见空间的真实面目了。    
 &nbsp;&nbsp;&nbsp;&nbsp;验证手机号码和邮箱都是必需的步骤，如果这个时候手机或者邮箱都收不到验证短信或邮件，也可以通过客服QQ： ```1346754578``` 或者电话：```0571-81020203 81020204```确认一下。

####三. 空间后台概览
&nbsp;&nbsp;&nbsp;&nbsp;验证完手机和邮箱以后，呈现在面前的就是 upyun 的后台，但是现在，它还没有任何数据。让我们分块大致看一下每一个部分都有什么用处。    
![Alt firstLogin](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/firstLogin.png)    
&nbsp;&nbsp;&nbsp;&nbsp;**左侧菜单栏**是常用的各类菜单选项，各类选项基本上都集中在左边这个雅黑色的地方。至于每个菜单项目都是什么，我们回头再详细的讲。     
&nbsp;&nbsp;&nbsp;&nbsp;**中间上方的数据表**是我们最关心的数据流量的地方，它会实时的显示空间的文件请求的流量以及带宽图。能非常直观的显示一天中的请求情况以及```峰值带宽```情况。    
&nbsp;&nbsp;&nbsp;&nbsp;**中间下方的表格**将会显示我们在空间创建的所有空间的信息，包括创建的空间的```空间的类型```，```空间的配额```，```防盗链```状态，还有```外链```和```表单```的开关状态。我们还没有创建空间，所以这儿现在一片空白。    
&nbsp;&nbsp;&nbsp;&nbsp;**右侧说明栏**是我们容易忽略的地方。```外链```方式告诉我们如何在程序中使用放在空间的图片；```FTP```说明告诉我们如何使用 FTP 的一些信息；```API```说明告诉我们通过 API 接口管理空间文件的一些基本信息。

####三. 创建一个图片空间    
&nbsp;&nbsp;&nbsp;&nbsp;要知道，空间可是我们用来放文件的地方，说了半天我们还不知道它具体是怎么回事。别急， 这就开始创建我们第一个```图片空间```。    
&nbsp;&nbsp;&nbsp;&nbsp;图片空间，顾名思义，这是一种只能存放图片类型文件的空间。图片空间不仅拥有国内先进的 cdn 网络加速，更拥有强大的图片后期处理能力。创建的步骤很简单，点击后台主页左上角的『选择空间』然后点击『创建空间』     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt createBucket](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/createBucket.png)    
&nbsp;&nbsp;&nbsp;&nbsp;这个时候我们会看见弹出来一个创建空间的窗口，在给空间起一个响亮的名字以后，我们先选择```空间类型```为『图片类』，空间配额我们通常方便随时扩容而留空。    
![Alt createBucket](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/createPICBucket.png)    
&nbsp;&nbsp;&nbsp;&nbsp;然后点击第二步我们到了授权```操作员```的步骤。    
![Alt createpicbucket2](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/createPICBucket2.png)    
&nbsp;&nbsp;&nbsp;&nbsp;```操作员```和```操作员密码```在云存储的使用中是两个非常重要的东西，掌握着操作员和操作员密码的开发者可以使用它们来操作空间的资源，每个空间可以有多个操作员来管理。我们在后面的程序中传递给 API 接口确定用户身份的参数中就需要它们出场了，以 Python 语言为例： 
   
	import upyun  
	      
	# ------------------ CONFIG ---------------------    
	BUCKETNAME = '空间名'    
	USERNAME = '操作员名'    
	PASSWORD = '操作员密码'    
	# -----------------------------------------------    

&nbsp;&nbsp;&nbsp;&nbsp;先不着急，我们现在只要先明白```操作员```和```操作员密码```是非常重要的两个东西就行了。    
&nbsp;&nbsp;&nbsp;&nbsp;设置完操作员以后我们点击下一步，来到了最后的空间创建完成页面。    
![Alt createPICBucket3](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/createPICBucket3.png)    
&nbsp;&nbsp;&nbsp;&nbsp;恭喜, 我们这就完成了第一个空间的创建。我们可以在空间看到空间的```默认域名```。还有操作员的简要说明。

####四. 接下来讲什么呢?

&nbsp;&nbsp;&nbsp;&nbsp;接下来我们将用这个创建的图片空间做一个快速简单的使用例子，在这之后，我们将详细的讲述 upyun 的细节和强大之处。    


----------
如有疑惑或者建议，欢迎评论。    
如果你希望有更直接的互动，欢迎加QQ群：``` 230558018 ```

[--NEXT--](http://blog.segmentfault.com/yunshu_blog/1190000000460216)

【[UPYUN](https://www.upyun.com) © 2014 署名-非商业性使用-禁止演绎】