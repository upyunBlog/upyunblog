----------

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;上一篇文章我们已经详细的了解过了 upyun 后台的三个空间的特点和用处。如果还想详细了解的可以点击[这里](http://blog.segmentfault.com/yunshu_blog/1190000000461736)回顾一下。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天我们来仔细的探寻一下空间的各个角落，去详细的了解一下我们可以在空间后台用到哪一些功能。包括```域名绑定```、```防盗链```、```流量分析```、```日志查询```、```缓存刷新```等等。    
####域名绑定    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;有些同学可能想，既然又拍云已经提供了一个三级默认域名，那```绑定域名的作用```体现在哪里呢？ 绑定域名除了更好记外，还能和迁入又拍云之前的老系统兼容，比如说原来的图片文件使用的是 img.upyun.com，切过来以后程序就不用再去修改了。 或者自己的网页中也只出现自己的网站域名了。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先我们来看一遍绑定域名的步骤：在左侧菜单栏选择```通用```，然后点击```域名绑定```，然后在页面的右上角点击```添加域名绑定```。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt addHost](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/addHost.png)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;添加完域名以后需要等待又拍云的审核。因为国情的因素，绑定的到空间的域名必须是在```工信部备过案```的。否则又拍云是不会审核通过的。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;又拍云的工作人员审核通过以后，我们就可以去域名服务商那里将绑定到空间的二级域名进行 cname 解析了。具体的方式如下：    

    在DNS解析管理中，把CNAME解析到{空间名}.b0.aicdn.com
    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;稍等个几分钟，等到域名解析生效以后，我们的```外链```就可以使用绑定的域名来代替默认域名来使用啦。    

####防盗链    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;是的，放在云上我们最担心的是什么，绝对是自己的文件被盗用，为他人做嫁衣裳。所以为了避免这种情况的发生，又拍云也提供了强大的防盗链功能，基本上覆盖了各类防盗链方式。让我们一个个来了解他们。    

+ IP 禁用    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;```IP 禁用```：在防盗链中启用 IP 禁用意味着我们可以借助这个防盗链来阻止我们添加的 IP 来访问空间的图片。点击编辑以后，跳出来如下的界面。一行一个 IP，并且支持通配符，比如10.11.12.* 将禁止 10.11.12.0～10.11.12.255 的IP访问。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt addHost](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/IP Security.png)    

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

