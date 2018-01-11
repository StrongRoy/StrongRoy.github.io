http请求中产生的两个核心对象

![](https://i.imgur.com/iVzpRiG.png)

http请求:  HttpRequest
http响应:   HttpResponse
所在位置 django.http

1. httpRequest属性：

	-  HttpRequest.path
		请求页面的全路径，不包含域名---完整的请求路径，不包括域
		例: "/music/bands/the_beatles/"。
<hr>
	-  HttpRequest.method
	请求中使用的HTTP方法的字符串表示。全大写表示。例如

		if request.method == 'GET':
		    do_something()
		elif request.method == 'POST':
		    do_something_else()
<hr>
	- HttpRequest.GET

		GET请求对象，包含HTTP GET参数的类字典对象，详细查看 QueryDict文档
<hr> 
	- HttpRequest.POST
		
		POST请求对象，包含HTTP GET参数的类字典对象，详细查看 QueryDict文档，
		
		服务器收到空的post请求的情况也是可能发生的，也就是说，表单from通过http post
		方法提交请求，单是表单中可以没有数据。因此，不能使用御酒 if request.POST来判断
		是否使用HTTP POST方法，应该使用if request.method == "POST" （参见本表的method
		属性）。
		注意: POST不包含file-upload（文件上传）信息，请看 FILES
<hr>
	-  HttpRequest.REQUEST  django 1.8之后被废弃了

		为了方便，该属性是POST和GET属性的集合体，但是有特殊性，先
		找到POST属性，然后在查找GET属性。借鉴PHP`s$_REQUEST。
		
		例如，如果GET={"name":"john"}和POST={"age":'34'},册 REQUEST['name']
		的值为"jhon",REQUEST["age"]的值是'34'.
		
		强烈建议使用GET and POST,因为这两个属性更加显示化，写出来的代码更易于
		理解
<hr>
	-  HttpRequest.COOKIES

		包含所有cookies的标准 python字典对象，keys 和values都是字符串 参见12章 有关于
		cookies更详细的讲解
<hr>
	-  HttpRequest.FILES

		包含所有上传文件的类字典对象。FILES中每个KEY都是<input type="file" name=""/>
		标签中的name属性的值，FILES中每个value同事也是一个标准的python字典对象，包
		含下面三个Keys：
			1. filename 上传文件名，用python字符串表示
			2. content-type 上传文件的Content type
			3. content 上传文件的原始内容
		注意： 只有在请求方法是POST，并且请求页面中<from>有enctype="multipart/frm-data"
		属性时FILES才拥有数据。否则FILES是一个空字典
<hr>
	- HttpRequest.META

		包含所有可用HTTP头部信息的字典。例如：
			1. CONTENT_LENGTH
			2. CONTENT_TYPE
			3. QUERY_STRING:未解析的原始查询字符串
			4. REMOTE_ADDR:客户端主机名
			5. SERVER_NAME:服务器主机名
			6. SERVER_PORT :服务器端口
		META中写着头加上前缀HTTP_ KEY 例如：
			1. HTTP_ACCEPT_ENCODING
			2. HTTP_ACCEPT_LANGUAGE
			3. HTTP_POST 客户发送的HTTP主机头信息
			4. HTTP_REFERER:referring页面
			5. HTTP_USER_AGENT:客户端的user-agent字符串
			6. HTTP_X_BENDER:X-Bender头部信息
<hr>
	- HttpRequest.user

		是from django.contrib.auth.models.User对象，代表当前登录的用户，如果访问用户当前没有
		登录，user将被初始化为from django.contrib.auth.models.AnonymousUser的实例。
		你可以通过user的is_authenticated()方法来辨别用户是否登录
		if request.user.is_authenticated():
			 do something for logged-in users
		else:
			 do something for anonymous users
		只有激活django中的 A	uthenticationMiddleware时该属性才可用
<hr>
	- HttpRequest.session

		唯一可读写的属性，代表当前回话的字典对象，只有激活django中的
		session支持是该属性才可用
<hr>
	-raw_post_data

		原始HTTP POST数据，未解析过。改机处理时会有用。
<hr>
	- HtppRequest对象的方法部分
		1. get_full_path()
		返回包含查询字符串的请求路径。例如，
		"/music/bands/the_beatles/？print=true"。
		2. QueryDict对象
		get()   如果key对应多个value，get()返回最后一个value。
		在httprequest对象中，GET和POST属性时 django.http.QueryDict类的实例。

## HttpResponse  
对于Httprequest对象来说 django自动创建，但是 httpresponse对象必须
**我们自己创建 每个View方法必须返回一个HTTPResponse对象。**
HTTPResponse类在django.http.HttpResponse.

# 构造HtppResponse:
response = HttpResponse("Here's the text of the Web page.")

response = HttpResponse("Text only,please.",mimetype="text/plain")
## HtppResponse的子类 部分
- HttpResponseRedirect

	构造函数接受单个参数：重定向到URL。可以是全URL(e.g.,'http://search.yahoo.com/')
	或者相对URL(e.g.,'/seach/').注意折返回HTTP状态码302
- HttpResponsePermanentRedirect

	同HttpResponseRedirect一样，但它返回永久重定向（HTTP状态代码301）而不是“找到”重定
	向（状态代码302）。
- HttpResponseNotModified

	构造函数不接受任何参数，也不会在此响应中添加任何内容。用于指定自用户最后一次请求
	（状态代码304）以来页面尚未被修改。

- HttpResponseBadRequest

	HttpResponse使用的就是使用400状态码。
- HttpResponseNotFound
 
	返回404状态码
- JsonResponse

	 返回Json字符串

详见：
[https://docs.djangoproject.com/en/1.11/ref/request-response/](https://docs.djangoproject.com/en/1.11/ref/request-response/ "请求和响应对象")

- httpresponse对象上扩展的常用方法

render rander_to_response 
 redirect  跳转的方法
更多详见：
[https://docs.djangoproject.com/en/1.11/topics/http/shortcuts/](https://docs.djangoproject.com/en/1.11/topics/http/shortcuts/ "Django shortcut functions")

#三.   常用的其他方法

	locals() 可以直接将函数中所有变量全部传递给模板



		
		   