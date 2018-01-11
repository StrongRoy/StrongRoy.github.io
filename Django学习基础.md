前段基础
python基础
数据库基础

常用的web框架
Full-stack Frameworks（全栈框架、重量级框架）
Django web2py TurboGears Pylons

Non-stack Frameworks（非全栈框架、轻量级框架）
tornado、flask、Bootle web.py、Pyramid。
详见：
https:/wiki.python.org/moin/WebFrameworks

选择框架
内容呈现框架
app接口
	可以选择轻量框架

django：大且全
flask： 小且精

django	：
		urls:路径与视图函数的映射关系
		views：逻辑处理
		models:做数据相关的操作
		template:模板语法--》将数据巧妙的插入模板中

django tornado flash bottle

#django开发环境搭建
##环境说明
python 
django 
mysql
pymysql
pycharm
##安装过程
1. 安装python3.6.3 64位下载地址：
 	https://www.python.org/ftp/python/3.6.3/python-3.6.3-amd64.exe
![](https://i.imgur.com/qfaSBPi.png)
![](https://i.imgur.com/O2XyRcv.png)
2. 更新pip版本 更新命令 python  -m pip install -upgrade pip 
因为在插件的时候会出现一些错误 因为我的机器已经更新过了。
![](https://i.imgur.com/qWVU6aF.png)
3. 使用pip安装 virtualenv 命令 pip install virtualenv    
作用：创建多个开发环境  把各个环境独立开
![](https://i.imgur.com/HXiwzya.png)
4. virtualenv django_basic_django
![](https://i.imgur.com/7iG7aW9.png)
5. 使用虚拟环境 命令行前面出现(...)表示使用到该虚拟环境
![](https://i.imgur.com/Pu9M82h.png)
6. 在虚拟环境中安装django 命令 pip install django
![](https://i.imgur.com/rmiYIuJ.png)
7.  在虚拟环境中安装pymysql 命令：pip install pymysql
![](https://i.imgur.com/pMlf4li.png)
8.  deactivate 退出虚拟环境

![](https://i.imgur.com/tdTZsme.png)
9. 在项目文件夹下创建项目
django-admin.py startproject hello_django
django-admin.py startapp hello
![](https://i.imgur.com/IT3KCTL.png)
#django-admin.py && manage.py
django-admin.py是django的一个用于管理任务的命令行工具，
 manage.py是对django-admin.py的简单包装 每个django project 里面都会包含一个  manage.py
#语法：
>
	django-admin.py <subcommand> [options]
	 manage.py <subcommand> [options]
	subcommand 是子命令
	options 是可选的
	常用的子命令
	startproject 创建一个项目
	startapp 创建一个app
	runserver 运行开发服务器
	shell 进入django shell
	dbshell 进入django dbshell
	check  检查django项目的完整性
	flush 清空数据库
	compilemessages 编译语言文件
	makemigrations 生产数据库同步脚本
	migrate 同步数据库
	showmigrations 查看生产的数据库脚本
	sqlflush  查看生成情况数据库的脚本
	slqmigrate  查看数据库同步的sql语句
	dumpdata 导出数据
	loaddata 导入数据
	diffsettings 查看你的配置和django默认配置的不同之处
##manage.py 特有的一些子命令
	createsupperuser  创建超级管理员 
	changepassword 修改密码
	clearsessions 清除session
## 将项目导入到pycharm
	将虚拟环境加载到pycharm中
![](https://i.imgur.com/7iDU3pu.png)
![](https://i.imgur.com/n3KxZy1.png)
![](https://i.imgur.com/JYVMWnk.png)
![](https://i.imgur.com/oxG0qJT.png)
将hello_django加载到pycharm
![](https://i.imgur.com/pmC80ID.png)
运行hello_django项目
![](https://i.imgur.com/DKBNfvK.png)





