#admin基本配置
django admin 是django自带的一个后台app，提供了后台的管理功能

#基础知识
##认识ModelAdmin
	管理界面的定制类，如需扩展特定的model界面需要从该类继承
##注册model类到admin的两种方式
1. 使用register的方法
2. 使用register的装饰器
##掌握一些常用的设置技巧
	list_display : 指定要显示的字段
	search_fields:指定搜索的字段
	list_filter:指定列表过滤器
	ordering: 指定排序字段
	fields\exclude: 指定编辑表单需要编辑\不需要编辑的字段
	fieldsets： 这是分组表单

[https://docs.djangoproject.com/en/1.11/ref/contrib/admin/](https://docs.djangoproject.com/en/1.11/ref/contrib/admin/)



