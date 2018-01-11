用 Jinja2替换默认模板引擎

1. Jinja2介绍
	Jinja2是一个现代的，设计友好的，仿照django模板的python模板语言。它速度快，被广泛使用，并且提供了可选的沙箱模板执行环境保证安全。
2. 如果用Jinja2替换Django自带模板
	配置步骤
我们在启动的当前virtualenv中安装Jinja2， pip install Jinja2
3. 在Django中简单实用Jinja2


#自定义Manager

1. 基本概念
	Manager是django模型进行数据库查询操作的接口。django应用的每个模型都拥有至少一个管理器。
2. 简单使用默认Manager

3. 为什么要定制Manager
4. 编码定制

# 集成已有的数据库
获取数据库中的表 生成相应的model

python manage.py inspectdb >>polls/models.py

# 使用mongodb数据库
1. mongodb简介
	mongoDb是基于文档(Document)的NoSQL数据库。文档是MongoDB数据的基本单元，非常类似于关系数据库中的行(比行要复杂)
	- database | database | 数据库
	- table|collection |数据库表、集合
	- row |document |数据记录行、文档
	- column |field |数据字段、域
	- index | index |索引
	- primary key |primary key |主键，MongoDB自动将_id字段设置为主键
2. django如何集成mongodb
	最好的选择是mongoengine
	安装 mongoengine
	修改 setting.py
	建立与mongo服务器连接
	建立Document
3. 实际操作mongodb
	新增数据
	查询数据	
	更新数据
	删除数据

