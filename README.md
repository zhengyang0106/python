# python

jisuanke_reptile_class.py这是一个用于爬取计蒜客的程序设计的代码

封装了两个类：

​			upLoad():主要用于获取本地cooick文件并添加到网页中，完成免密登录

​			downLoad():get_link()函数主要用于获取程序设计的课程名和链接。　get_text() 方法主要是用于爬取代码信息。

爬虫用到了webdriver库里面的８中元素查找中的方式５种，并且使用了switch_to.window（）切换窗口

图片：

 ![](http://zy0106picture.oss-cn-beijing.aliyuncs.com/2019.10.06/8d2c896f-91cf-40b2-b7fb-70f433cffa81.png)



![](http://zy0106picture.oss-cn-beijing.aliyuncs.com/2019.10.06/c84d5a30-d491-4b4a-9585-e8d6e47af8d0.png) 



 ![](http://zy0106picture.oss-cn-beijing.aliyuncs.com/2019.10.06/e1027c13-4975-439f-93de-51ffcf7a5aae.png) 





UpLoad_class.py : 因为在使用markdown写的文档插入的图片都是保存在本地，上传github后无法查看图片，所以编写该程序实现上次图片到阿里云，并返回markdown语法到粘贴板。

​	UpLoad()类主要用于实现阿里云的子用户的accesskey实现登录和判断上传文件是否是图片。主要运用了到oss2，uuid,  sys, os, pyperclip 类。

通过调用uuid的uuid4方法获取uuid,sys类进行传参,pyperclip类的copy把拼接好的markdown语法的url复制粘贴板，paste()方法直接获取剪切板内容，实现无参上传。引入os，主要是调用os.path.splitext()方法来直接划分文件后缀名。

 ![](http://zy0106picture.oss-cn-beijing.aliyuncs.com/2019.10.06/361b7bcd-89cf-4e69-8145-788346695d61.png) 

