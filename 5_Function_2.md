----------    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;上一篇文章我们详细的了解过了```域名绑定```的作用和各种方式的```防盗链```。如果还想继续回顾一下这方面的内容，可以点击[这里](http://blog.segmentfault.com/yunshu_blog/1190000000468896)，再了解一下。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;空间还有什么特定的功能没有发掘呢？当然是首页巨大的```流量统计实时曲线图```，```访问日志查询```，还有```缓存刷新```功能。    
####一. 流量统计    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一旦我们的空间投入使用，有用户通过访问网站请求了图片以后，又拍云会将实时的流量和带宽显示在空间的首页。    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/bucketPic.png)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这个实时的带宽和流量显示图，也能反映出网站在某个时段的访问量。更重要的是，高峰时期的访问给服务器带来的压力，现在已经完全由又拍云来承担了。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在图标的右上角我们还能查看最近七天，最近十五天，以及最近三十天的流量带宽图。    

####二. 访问日志    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;左侧菜单栏有一个```日志```。菜单，我们可以在这里看到我们非常关心的文件访问情况，清晰及时的日志分析对于网站，应用来说是非常重要的。我们可以在**日志分析**栏里面看到如下信息：   
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/log1.png)    
 
+ 热门文件：可以查看到空间被访问次数最多的文件。    
+ 热门引用页面：可以查看是哪些网站和域名引用空间中的文件。    
+ 热门客户端：可以查看到都有哪些 User Agent 来访问了空间的文件。    
+ 热门 IP：可以查看到都有什么 IP 来访问了空间的文件。    
+ 文件大小：可以查看到被请求的文件的大小。（如果请求文件的大小小于实际文件的大小，很有可能是文件尚未下载完全便断开了连接，常见于 apk 文件下载的时候用户方取消下载的情况）    
+ 资源状态：可以查看文件的被请求的 http 状态，常见的有200，404，等常见的状态码。    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;日志分析还有一个重要的作用就是，根据这些信息来判断自己的文件的访问情况，以及是否需要使用某种防盗链来保护流量。日志分析通常最快能看到昨天的日志，而日志下载则更加的及时.除了使用日志分析来查看文件访问的具体情况，也可以直接下载最原始的日志文件自行的进行日志分析。对于常用的开源日志分析软件，Google 君总不会对我们隐瞒。    

####三. 缓存刷新    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;又拍云的图片空间和文件空间的背后都有全国覆盖的自建 CDN 网络的支持，CDN 网络中缓存是非常重要的一个概念。如何准确及时的更新各个节点的缓存，也是 CDN 技术中一个重要的部分。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在对空间的文件进行覆盖，删除等变动操作的时候，又拍云会自动把这个文件的链接加入```缓存刷新队列```，然后缓存刷新服务器就会按照加入队列的时间顺序将全国各个节点的旧的缓存刷掉。等到终端再次访问这个文件的时候，就能从节点访问到最新修改的文件，从而达到了无论文件如何修改，都能访问到最新的文件状态。     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;但是既然这些修改和删除操作都能自动加入缓存刷新队列，那又拍云后台的缓存刷新工具有什么作用呢？    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一个文件在所有的节点刷新的时间大概在0~10分钟，如果出现超过这些时间但是被修改的文件还是没有更新，那么可能是自动加入刷新队列的时候出现了阻塞。这个时候，空间的这个工具的作用就来了，手动将文件加入刷新队列。需要注意的是，缓存刷新工具目前```只支持默认域名```。    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/purge.png)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;除了后台的手动刷新，目前又拍云还提供一个[缓存刷新的 API 接口](http://wiki.upyun.com/index.php?title=%E7%BC%93%E5%AD%98%E5%88%B7%E6%96%B0API%E6%8E%A5%E5%8F%A3)。可以直接通过程序来刷新指定的文件外链。     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;缓存刷新目前用的最多的地方应该是在```使用静态 CDN 空间的时候```：当源站的文件有变动（修改，删除等）操作的时候，需要主动调用缓存刷新 API 接口来告诉 CDN 网络源站文件有更新。否则我们在访问的时候还是会访问到各个节点的老的缓存。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下面我们用 Python 来根据缓存刷新 API 文档实现一个刷新程序。    


```

#!/usr/bin/env python
#-*-coding:utf-8-*-

import urllib
import hashlib
import datetime
import requests

#========config_begin======
BUCKETNAME = 'bucketname'
USERNAME = 'username'
PASSWORD = 'password'
purge = 'your_URL'
#========config_end========
```    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们在 Python 中使用了 requests 这个非常优秀的轮子, 所以 put 操作显得非常简单。当然不熟悉 Python 的同学只要了解到它是最后将我们的请求发送到 upyun 空间的模块就定了。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;然后我们需要传递的参数还是这些：```空间名```，```操作员名```，```操作员密码```，```需要刷新的 URL```。当然，真正集成到项目中去的时候，```需要刷新的 URL```这肯定是另一种传递方式。    
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们来看一下请求方法：

```
    POST /purge/ HTTP/1.1
    Host: purge.upyun.com
    Authorization: UpYun demo_bucket:demouser:62c428533830d84fd8bc77bf402512fc
    Date: Wed, 24 Aug 2011 07:33:47 GMT
    Content-Type: application/x-www-form-urlencoded
```    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;http 请求头里面我们需要传递的header 是```Authorization```，```Date```，```Content-Type```。所以我们的主要目标是组成这些字段。    

+ ```Date```：Date 需要一个 GMT 格式的时间，也就是（D, d M Y H:i:s \G\M\T）这种格式。    
+ ```Authorization```：UpYun ```空间名```:```操作员名```:```sign```    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;其中```sign```的制作方法为：sign = md5(需要刷新的URL + & + 空间名 + & + Date + & + md5(操作员密码))    
    
最后，我们根据这个规则将各个字段通过字符串拼接起来。用 Python 实现如下：

```
def httpdate_rfc1123(dt):
    """Return a string representation of a date according to RFC 1123
    (HTTP/1.1).

    The supplied date must be in UTC.
    """
    weekday = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"][dt.weekday()]
    month = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep",
             "Oct", "Nov", "Dec"][dt.month - 1]
    return "%s, %02d %s %04d %02d:%02d:%02d GMT" % \
        (weekday, dt.day, month, dt.year, dt.hour, dt.minute, dt.second)




date = httpdate_rfc1123(datetime.datetime.utcnow())
sign = hashlib.md5(purge+"&"+BUCKETNAME+"&" +
                       date + "&" + hashlib.md5(PASSWORD).hexdigest()).hexdigest()
```    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最后，我们将准备好的 参数传入 headers，然后通过 http post 到 api 接口，就可以了，具体的 Python 例子如下：
    
```
Header = {"Expect": "",
          "Authorization": 'UpYun '+BUCKETNAME+':'+USERNAME+':'+sign,
          "Date": date,
          "Content-Type": "application/x-www-form-urlencoded",
          }
post = urllib.urlencode({'purge': purge})
r = requests.post("http://purge.upyun.com/purge/", post, headers=Header)
print r.text

```    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最后我们可以根据 r.text 即 API 接口返回的内容来判断我们是否已经刷新成功。以下是 API 接口返回来的常见的信息，仅供参考：    

```   
   200：json格式的字符串{invalid_domain_of_url:不属于自己域名的url列表} 
   401：无认证头部信息（Authorization）（提示信息：Need Authorization Header）
   401：无认证头部信息（Date）（提示信息：Need Date Header）
   401：操作员不存在（提示信息：User is not exists）
   401：空间名不存在（提示信息：Bucket is not exists）
   401：请求时间超出30分钟（提示信息：Date offset error）
   401：签名错误（提示信息：Sign error）
   406：每分钟刷新URL个数超过600限制
      （提示信息：URL [url] 之后的数据未能加入刷新队列，原因：每分钟刷新数量已经超过限制。）

```    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这里有一个容易让人困惑的地方。那就是刷新成功后，返回的是一个{invalid_domain_url:[]}。这个内容很容易让人觉得是错误的信息。但是事实上，这是一个表示刷新成功的提示。首先，它返回的是200状态码，然后 ```invalid_domain_url:[]```列表为空的时候表示没有非法的刷新 URL。如果```invalid_domain_url:[]```里面出现了一个 URL，那就是在告诉我们传入了一个不属于我们空间的 URL。 
       
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;好了，到目前为止，我们也已经看过```流量统计``` ```日志分析``` ```缓存刷新```三大块内容了，如果有不清楚的地方那个，欢迎留言。    
####四. 接下来讲什么呢?    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;空间后台的菜单选项我们大致已经了解过了。接下来，我们将去非常详细的了解一下 upyun 的 API 接口。看看我们究竟能通过这些接口做哪些具体的事情。  
      
----------    
如有疑惑或者建议，欢迎评论。        
如果你希望有更直接的互动，欢迎加QQ群：```230558018```        

[-NEXT-](#)    
【[UPYUN](https://www.upyun.com) © 2014 署名-非商业性使用-禁止演绎】

