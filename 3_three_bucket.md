----------


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在刚开始创建图片空间的时候我们发现又拍云的后台有三种空间：```文件类空间```，```图片类空间```和```CDN空间```。    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt three_bucket](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/createBucketWindow1.png)    

那么这三种空间都有那些相同点和不同点呢。让我们一个一个去了解。        
####一. 图片空间    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;所谓图片空间，顾名思义，那就是专门用来存储图片类型的文件空间。所以图片类型空间是**无法**上传非图片文件的。又拍云8年多的图片处理和存储经验，图片空间的特点是非常的鲜明的。现在，就让我们慢慢来揭开图片空间的神秘面纱。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;图片空间特性大致有以下几种：```自定义缩略图```、```水印```、```锐化图片```以及 ```GIF 格式图片转换成静态图片```等等。        

+ 自定义缩略图版本    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在空间后台左侧的菜单栏里面，我们选中```自定义版本```就到了图片空间特有的缩略图版本设置页面。    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/smallPic.png)         
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;自定义缩略图版本可以用来生成各种形式的缩略图。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;页面上方的间隔标志符连接```图片外链```和```缩略图版本名称```的标记。目前有三种符号分别是：```!```感叹号， ```_```下划线和 ```-```中划线。需要注意的是，文件路径中**千万**不能存在和间隔标志符相同的字符串，否则访问这个文件会出现404的。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;现在我们开始创建一个缩略图版本。点击右上角的创建缩略图版本，我们就可以看到一个创建窗口。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt upyunpic2](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/smallPic2.png)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;方便辨识,我们取一个和缩略图大小相关的版本名称，确定以后就不能更改了。目前缩略图版本尚无法删除。缩略图方式有很多种，可以根据需要来指定缩略的方式。然后是填写限定的缩略图的尺寸大小。建议勾选锐化图片，因为当图片过小的时候，这个选项能让图片看上去更加的清晰。最后还有一个是 GIF 图片的相关选项。        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;第二项是```水印选项```，在这个里面，我们可以在图片中加入自己的水印。在这个选项里面我们可以上传水印，也可以确定水印在图片的显示位置。但是水印图片不能超过缩略图长宽的一半大小。举个例子，定义一个缩略图的大小为200px\*200px，那水印的大小不能超过100px\*100px。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;第三项是定义缩略图的```输出```。可以自定义选择 jpg，png，webp这种格式来输出。需要注意的是，png 格式保存的图片是不会改变原来的大小的。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在我们改动设置以后，可以实时的点击右侧的猫咪君来预览我们的改动，实时的查看是否符合我们的需求。最后，还有最重要的一点。又拍云的缩略图的生成是完全```不占用空间的容量```的。所以，上传完原图以后，我们可以尽情的依赖缩略图配置去完成各种各样需求。        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最后,我们配置好了缩略图版本，如何调用呢？没错，只要``` http://绑定域名/原图路径+间隔标志符+自定义版本名称```：[http://upyun-blog-pic.b0.upaiyun.com/upyun-python-sdk/tac.png!200px](http://upyun-blog-pic.b0.upaiyun.com/upyun-python-sdk/tac.png!200px)。这样我们就能看到缩略图了。        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyun-python-sdk/tac.png!200px)    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;图片空间除了缩略图版本，还有一个```图片信息版本```。图片信息版本的用法和缩略图版本的调用方式一样。我们来创建一个看一下。点击自定义版本界面的```创建图片信息版本```，我们看到的是这个界面：    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/exif.png)        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;同样，版本名称一旦创建以后也是无法修改的。除了图片的基本信息，exif 信息有两种显示方式，可以根据需要创建。返回的是 ```json``` 格式的数据。举个例子，我们上传到空间的倒立着的猫咪图片信息为：    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/exif1.png)        

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;图片类空间的特性基本如此。强大缩略图功能将会让图片在网站和 APP 的应用中更加的灵活和省心。    

####二. 文件类空间
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文件类空间是一个```没有文件类型限制```的空间。所以,任何小于100兆的静态文件都能上传到文件类型空间。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;文件类空间的创建和图片空间一样。指定空间的名字，一步一步的创建完成。文件类空间与图片类空间的区别是：文件类空间```没有缩略图版本```。        
####三. CDN空间    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CDN 空间和前两个空间有很大的不同。简单的说，CDN 目前只支持静态文件的加速，所以在接入 CDN 空间之前，源站必须要实行动静分离，否则动态数据是无法在CDN 空间访问的。成功接入CDN 服务以后，源站的文件会被缓存到又拍云的各个节点，缓存时间默认为```7```天。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;让我们在一步一步的设置中来了解 CDN 空间的优势。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;创建 CDN 空间的时候，首先是一个设置界面：    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/cdnOption2.png)        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;电信 IP 和联通 IP 栏是填写源站服务器的 IP 地址，如果是 BGP 机房，可以将两个栏都填写上，如果是单线机房，只要填写相应的线路就行。访问域名是能访问到源站文件的域名。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;信息确认填写正确以后就可以点击下一步：    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/cdnOption3.png)        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;然后下载一个大约为1M 的测试文件放在源站根目录下面。通过域名能正常访问以后。接下来开始进行回源测试。    
&nbsp;&nbsp;&nbsp;&nbsp;![Alt pic](http://upyun-blog-pic.b0.upaiyun.com/upyunBlog/cdnOption4.png)        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此时，又拍云的回源测试服务器会以并发访问的方式想源站请求测试文件，探测文件的下载速度，最后取平均下载速度为结果。如果下载速度小于150KB/s，则视为源站线路不达标。不会予以通过。所以在测试的时候，需要确保源站有```至少5M```的空闲带宽。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此外，回源测试目前不支持https 的测试方式。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果一切顺利的话，我们的 CDN 空间的设置就算完成了，这个时候源站的静态文件已经能享受到又拍云自建 CDN 的加速功能了。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;源站如果有文件的覆盖操作，是需要告诉 CDN 网络源站有文件更新的，我们提供了缓存刷新的 API 接口，在覆盖，或者删除了源站的文件以后，必需调用这个接口来刷新 CDN 节点的所有缓存。具体的操作，我们会在下一节中详细的了解。    
####四. 接下来讲什么呢？    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;接下来我们会详细的分析空间的一些细节，包括```缓存刷新```，```防盗链措施```，```域名绑定```，以及```日志分析```等等。    


----------    
如有疑惑或者建议，欢迎评论。        
如果你希望有更直接的互动，欢迎加QQ群：```230558018```        

[-NEXT-](#)    
【[UPYUN](https://www.upyun.com) © 2014 署名-非商业性使用-禁止演绎】