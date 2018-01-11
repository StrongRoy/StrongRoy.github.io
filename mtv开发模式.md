mtv开发模式
#从著名的MVC模式开始说起

	所谓的MVC就是把Web应用分为模型（M）控制器（C）和视图（V）三层，他们之间以一种插件式的、松耦合的房还是
	连接在一起，模型负责业务对象与数据库的映射(ORM)，视图负责与用户的交互页面(页面)，控制器接受用户输入条
	用模型和视图完成用户的请求，其示意图如下所示:
![](https://i.imgur.com/1rhnBgc.png)

**django的MTV模式的本质和MVC是一样的，也是为了各组件间保持松耦合关系，只是定义有些不同，django的mtv分别是**：

1. M 带包模型(Model) 负责业务对象和数据库的关系映射(ORM)
2. T 代表模板(Template) 负责如何把页面展示给用户(html)
3. V 代表视图 （View） 负责业务逻辑 并在适当时候调用Mode和Template
4. 出了以上三层外，还需要一个URL分发器、他的作用是讲一个个URL的页面请求分发给不同的View处理，
##View在调用相关的Mode和Template，MTV的相应模式如下所示：
![](https://i.imgur.com/dVo58R0.png)

1. web服务器(中间件)收到一个http请求
2. Django在URLconf里查找对应的视图（view）函数来处理http请求
3. 视图函数调用相应的数据模型来存储数据、调用相应的模板向用户展示页面
4. 视图函数处理结束后返回一个http的相应给web服务器
5. web 服务器将响应发送给客户端

**这种设计模式关键的优势在与各种组都是松耦合的额，这样，每个有django驱动的web应用都有**
着明确的目的，并且可独立更改而不影响其他的部分。
比如，开发者更改一个应用程序的URL而不用影响到这个程序底层的实现。设计师可以更改HTML页面
的样式而不用接触python代码
数据库管理员可以重新命名数据库表并且只需要更改模型，无需从一大堆文件中进行查找和替换。

##落实到实处 django的MTV模式相对应的python文件如下：
![](https://i.imgur.com/KU0Mpwt.png)

#urls.py详解
##URl分发器 （路由配置文件）
URL配置（URLconf）就像django所支持网站的目录。它在本质是URL模式以及要为改URL
模式调用的视图函数之间的映射表。你就是这种方式告诉django，对于这个URL嗲用这段代码，
对于那个URL调用那段代码，URL的加载时从配置文件中开始。

##1. urlpatterns 的两种形式
没有前缀的情况，使用的列表（推荐方式）
urlpatterns = [
    url(r'^hello/$', views.hello),
]
有前缀的情况，使用patterns`过时的方法`方法
> 
	from django.conf.urls import url,patterns
	from hello import views
	urlpatterns = patterns('',url(r'^hello/$', views.hello))
	或
	from django.conf.urls import patterns
	urlpatterns = patterns('hello',url(r'^hello/$', 'views.hello'),)

##2. URL模式
>
	urlpatterns =[
		url(正则表方式，view函数，参数，别名，前缀)
	]

参数说明：

- 一个正则表达式字符串
- 一个可调用对象，通常为一个视图函数或一个指定视图函数路径的字符串。
- 可选的要传递给视图函数的默认参数（字典形式）
- 一个可选的name参数
- 路径前缀
 
##3 URL 分解器 include函数
通常一个URL分解器对应一个URL配置模块，他可以包含多个url模式，
也可以包含多个其他URL分解器，通过这种包含结构设计，实现django对URL的层级解析。

URL分解器是django实现app与项目解耦的关键，通常include方法操作的url配置模块，最终
会被解释成URL分解器

##预留的问题，为什么admin模块引入的时候没有使用include
url(r'^admin/', admin.site.urls),
##URL常见写法示例 正则表达式
>
	url(r'^test/\d{2}/$',views.test)
	url(r'^test/(?P<id>\d{2})/$',views.test)     ===》 test(id)
	url(r'^test2/(?P<id>\d{2})/(?P<key>\w+)/$',views.test) ===> test(id,key)
关于正则表达式的使用可以参考 建议爬虫实战中的正则表达式
























