----------    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[UPYUN](https://www.upyun.com/index.html) 在五月一日前夕推出了 cdn 的动态作图功能，简单的说，静态 ```CDN 空间```终于也能像```图片空间```那样进行图片处理了。    
####CDN 空间的图片处理
>CDN 空间的图片处理功能属新推出功能，该功能起初是适应于存储类型的```图片空间```；他的推出对急于使用云分发，且数据量特别大，需要图片处理的用户来说，```可以不用将图片传到UPYUN```。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CDN 空间只使用又拍云的独立云分发服务，如果还不了解 CDN 空间和图片空间文件空间的区别，可以[参考CDN类型空间的创建][1]。图片处理功能也就是开放了图片类型空间的自定义版本， [参考自定义版本的创建][2]。我们再简单介绍一下 CDN 空间的自定义版本的创建。    

1.创建自定义版本
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我们会发现，CDN 的动态作图功能开放以后，CDN 空间的左侧菜单栏里面的自定义版本现在成为了```可操作状态```。现在，我们点击```自定义版本```来使用一下这个 CDN 空间的新功能。    

![创建自定义版本](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/makePicCDN.png)

- **①** 创建一个自定义版本，当访问图片时调用该自定义版本，又拍根据设置计算并生成一张符合设置参数的图片。
- **②** 间隔符号，间隔符是调用自定义版本的标识，是固定的不可修改的，又拍提供3个间隔符供选择，分别是感叹号`!`中线`-`下划线`_`，注：```间隔符不能出现在路径和文件名中```。
- **③** 创建图片信息版本，图片信息也就是EXIF信息，和调用自定义版本一样，调用返回图片尺寸及类型的json。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下面我们创建一个200X300的自定义版本，限制宽高为`200px x 300px`，**不添加水印，输出格式默认**。

![创建自定义版本](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/createPicCDN.jpg)
      
2.图片处理
    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;刚才我们创建了一个 `200X300` 的自定义版本，那么我们设置间隔符号为 `!` 接下来我们使用使用图片处理
例如我们独立分发的存储下有个 cat.jpg，图片文件尺寸为：`width: 728px`，`height: 343px`

```
http://upyun-blog-cdn.b0.upaiyun.com/upyunBlog/cat.jpg
```
&nbsp;&nbsp;&nbsp;&nbsp;![创建自定义版本](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/cat.jpg)

现在修改访问地址为

```
http://upyun-blog-cdn.b0.upaiyun.com/upyunBlog/cat.jpg!200X300
```

![创建自定义版本](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/cat.jpg!200X300)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;现在看到图片变为`width: 200px`，`height: 134px`。CDN 空间也能成功的处理图像了。总之，CDN 动态作图功能能根据需要在空间设置各种类型的自定义版本，这不再是图片空间的专利，也将大大的方便我们的使用。   
 
----------    
如有疑惑或者建议，欢迎评论。        
如果你希望有更直接的互动，欢迎加QQ群：```230558018```        
  
【[UPYUN](https://www.upyun.com) © 2014 署名-非商业性使用-禁止演绎】

[1]:http://blog.segmentfault.com/yunshu_blog/1190000000461736
[2]:http://blog.segmentfault.com/yunshu_blog/1190000000461736