----------

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;上一篇文章我们已经详细的了解过了 upyun 后台的三个空间的特点和用处。如果还想详细了解的可以点击[这里](http://blog.segmentfault.com/yunshu_blog/1190000000461736)回顾一下。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天我们来仔细的探寻一下空间的各个角落，去详细的了解一下我们可以在空间后台用到哪一些功能。包括```域名绑定```、```防盗链```、```流量分析```、```日志查询```、```缓存刷新```等等。我们先来了解前面两个功能。    
####一. 域名绑定    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;有些同学可能想，既然又拍云已经提供了一个三级默认域名，那```绑定域名的作用```体现在哪里呢？ 绑定域名除了更好记外，还能和迁入又拍云之前的老系统兼容，比如说原来的图片文件使用的是 img.upyun.com，切过来以后程序就不用再去修改了。 或者自己的网页中也只出现自己的网站域名了。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先我们来看一遍绑定域名的步骤：在左侧菜单栏选择```通用```，然后点击```域名绑定```，然后在页面的右上角点击```添加域名绑定```。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt addHost](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/addHost.png)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;添加完域名以后需要等待又拍云的审核。因为国情的因素，绑定的到空间的域名必须是在```工信部备过案```的。否则又拍云是不会审核通过的。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;又拍云的工作人员审核通过以后，我们就可以去域名服务商那里将绑定到空间的二级域名进行 cname 解析了。具体的方式如下：    

    在DNS解析管理中，把CNAME解析到{空间名}.b0.aicdn.com
    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;稍等个几分钟，等到域名解析生效以后，我们的```外链```就可以使用绑定的域名来代替默认域名来使用啦。    

####二. 防盗链    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;是的，放在云上我们最担心的是什么，绝对是自己的文件被盗用，为他人做嫁衣裳。所以为了避免这种情况的发生，又拍云也提供了强大的防盗链功能，基本上覆盖了各类防盗链方式。让我们一个个来了解他们。    

+ IP 禁用    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```IP 禁用```：在防盗链中启用 IP 禁用意味着我们可以借助这个防盗链来阻止我们添加的 IP 来访问空间的图片。点击编辑以后，跳出来如下的界面。一行一个 IP，并且支持通配符，比如10.11.12.* 将禁止 10.11.12.0～10.11.12.255 的IP访问。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt addHost](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/IPSecurity.png)    

+ 域名防盗链    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;域名防盗链分```域名白名单```和```域名黑名单```。我们只能选择启用其中的一种。*白名单*状态下只允许列表中的域名能引用外链文件。举个例子，主站为 upyunblog.com 我们设置只能这个域名访问的时候 需要设置的域名如下：    
    

```   
    upyunblog.com    
    *.upyunblog.com
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这样就能将该顶级域名下所有的二三级域名都包括进去了。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;同理，*黑名单*中的域名将被阻止引用外链。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt addHost](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/hostList.png)    

+ 客户端白名单    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;客户端白名单，也简称为 ```UA 防盗链``` 依据就是 ```User Agent```字段。浏览器访问[http://ua123.net/](http://ua123.net/)看到的字段就是了。UA 防盗链通常用在手机 APP 或者一些可自定义 User Agent 的应用，比如播放器。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;添加客户端白名单的方式也和前面差不多，同样支持通配符。    

+ Token 防盗链    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Token 防盗链在所有的防盗链中设置稍微复杂一点点，需要在程序中传递若干参数来生成一个 Token。然后外链必须要带上这个 Token 才能在规定的时间内访问文件。 现在我们开始为我们的文件空间```upyun-blog-file```制作 Token 防盗链。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先，我们在 Token 防盗链界面开启 Token 防盗链，并且设置我们的密钥为：```upyun```然后点击保存。    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/Token.png)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在这个界面中我们可以在```签名方式说明```中获得如何生成 Token 签名的方法。并且在```代码实例```中看到 PHP 语言的例子和 java语言 的例子。现在我们用简单整洁的 Python 来举个例子。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先我们看一下需要生成几个参数，然后一个个生成他们。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.```key```&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<=====它就是我们刚刚在空间填写的密钥：upyun。            
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.```etime```&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<=====它就是我们设定的 Token防盗链的过期时间。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3.```uri```&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<=====它就是我们要使用 Token 加密的文件远程路径。    
    
```    
    import datetime
    import time
    import hashlib
    
    if __name__ == '__main__':
        key = 'upyun'
        #获取当前 Unix 时间，并且设定过期时间为900秒
        etime = int(time.mktime(datetime.datetime.now().timetuple())) + 900
        uri =  /upyunBlogFile/miao.jpeg
        #生成 MD5。
        tokensign = hashlib.new('md5', key + '&' + str(etime) + '&' + uri).hexdigest()
        #截取32位MD5的中间八位，拼接生成 token
        token = '?_upt=' + tokensign[12:20] + str(etime)
    
```    
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;简单的 token 制作就完成了。访问的时候在原外链的基础上加上 token 就能对外链进行加密了。比如我们刚刚就依据这个代码行程了一个带着 token 的外链：[http://upyun-blog-file.b0.upaiyun.com/upyunBlogFile/miao.jpeg?_upt=c86f66e11397488759](http://upyun-blog-file.b0.upaiyun.com/upyunBlogFile/miao.jpeg?_upt=c86f66e11397488759) 。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;没有带 token 的外链，或者超过了有效期的token链接都会返回```http code：403```，达到防盗链的目的。   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此外，token 防盗链还可以防止下载，特别适合网站的音视频文件的保护。用法为将 token 放入 ```Cookie``` 中。  

+ 自定义提示图    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这个功能让我们自定义当服务器返回的状态码为```403```，```404```，```405```的时候的提示图。只要在这个页面上传一张自定义图就行。
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/404.png)    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;好了，今天我们看完了这两个功能，特别是防盗链功能，对我们的网站和应用还是密切相关的。    

####三. 接下来讲什么呢？    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;接下来我们会继续详细的分析空间的一些细节，包括```缓存刷新```，```流量统计```以及```日志分析```等等。    


----------    
如有疑惑或者建议，欢迎评论。        
如果你希望有更直接的互动，欢迎加QQ群：```230558018```        

[-NEXT-](#)    
【[UPYUN](https://www.upyun.com) © 2014 署名-非商业性使用-禁止演绎】