缓存类型
Memcached 最有效 最快
Database caching
Filesystem caching
Local-memory caching
Dummy caching(for development)
Using a custom cache backend
缓存粒度分类
Per-site cache
Per-view cache
Template fragment caching
Low=level cache API

#缓存设置与使用---缓存示例一
CACHES={
	'default':{
			'BACKEND':'django.core.cache.backends.memcached.MemcachedCache',
			'LOCATION':'127.0.0.1:11211'
			}
		}
缓存设置与使用---缓存示例二
CACHES={
	'default':{
			'BACKEND':'django.core.cache.backends.memcached.MemcachedCache',
			'LOCATION':'unix:/tmp/memcached.sock',
			}
		}
缓存设置与使用---缓存示例三
CACHES={
	'default':{
			'BACKEND':'django.core.cache.backends.memcached.MemcachedCache',
			'LOCATION' : [
						'127.19.26.240:11211' ,
						'127.19.26.242:11211' ,
						]
			}
		}
缓存设置与使用---缓存示例四
CACHES={
	'default':{
			'BACKEND':'django.core.cache.backends.memcached.MemcachedCache',
			'LOCATION' : [
						'127.19.26.240:11211' ,
						'127.19.26.242:11212' ,
						'127.19.26.244:11213' ,
						]
			}
		}

#缓存设置与使用--访问缓存
from django.core.cache import caches
cache1=caches['myalias']
cache2=caches['myalias']
cache1 is cache2
True
#缓存设置与使用--使用缓存
from django.core.cache import caches
cache.set('my_key','hello,world',30)
cache.get('my_key')
'hello,world!'
cache.get('my_key')
None
cache.get('my_key','has expired')
'has expired'

###
Memcached简介
基于内存的框架  C语言编写 具有高性能 是分布式对象缓存系统，最初设计师通过减少数据库的负载，
以加速动态页面
LiveJournal
FaceBook
Wikipedia
Twitter
Youtube
Memcached指南故事

#Memcached安装
###ubuntu&Debian
sudo apt-get install libevent-dev
sudo apt-get install memcached
###redhat/fedora/Centos
sudo yum install libevent-devel
sudo yum install memcached

Memcached 配置
-p<num>  设置端口号(默认)

memcached 存取命令
###存储命令
set 不管key存在与否 强制进行set操作
add 必须在memcached中不存在相应key才能作用
replace 要求memcached中必须存在相应key才能作用
append 将数据追加到keu对应calue值的尾部（不允许超过限制，用于管理list）
cas (check and set) :另一个存储数据的操作，当你最后一次读取数据后，没有其他其他人修改数据时，才可以写成功。用于解决更新数据时的竞争。
###获取命令
get 获取一个key的或多个keys的值
gets 带CAS的get命令，会返回带CAS标识（唯一的64位数字）的value。
delete 删除存在的项
incr/decr 自增或自减 只接受正整数。如果key不存在，incr/decr失败
flush_all 清除memcached中所有项，主要采取将所有数据设置为过期的方式实现，
可指定过期时间。

#Python Client
##python-memcache
抛出异常少
负数的timeouts =》  返回成功 立即过期
支持压缩
纯python编写
安装方便
自定义设置少
##pylibmc
抛出异常多
负数的timeouts  =》 0
pylibmc自己实现的压缩 
python包装C/C++ API
安装简单
使用较复杂
建立连接支持很多可选项（如 non-blocking
请求，TCP no-delay 禁用）

#操作演示
##python-memcache
pip install python-memcached
##pylibmc
sudo apt-get install python-dev
sudo apt-get install libmemcached-dev
pip install pylimc
##启动memcached服务







