# 相关代码已经修改调试成功----2017-3-28 #

**实现：淘宝网上对“零食”搜索后前100页，一些相关字段信息的爬取**

# 笔记： #

一、大型商城爬虫项目难点

	1. 屏蔽数据的获取-------抓包
	2. 信息的提取--------优先xpath，其次re，正则表达式
	3. 各种反爬手段--------验证码[一般是交给打码平台处理]，用户代理，Ip代理，取消cookie记录
	4. 数据的合理储存--------写进数据库
	5. 爬取效率的问题--------同时运行多个爬虫


二、散点知识

     1.response.body.decode('utf-8','ignore')   #在response中 response.body是二进制，需要转换;igonre是忽略不能转码的字符
     2.同理urllib.urlopen().read().decode('utf-8','ignore') 在平时的编程中要注意

三、连接mysql数据库

	import pymysql
	db=pymysql.connect("host","user","password","dbname",charset="utf8") 
	cx=db.cursor()  #创建游标
	sql='.....'
	cx.execute(sql)  #执行sql语句
	db.commit()  #提交，不然无法保存数据
	cx.close()   #关闭游标
	db.close()   #关闭连接


获取查询的数据

	# -*- coding:utf-8 -*-
	import pymysql
	conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='', db='tkq1')
	cursor = conn.cursor()
	cursor.execute("select * from tb7")

	# 获取剩余结果的第一行数据
	row_1 = cursor.fetchone()
	print row_1
	# 获取剩余结果前n行数据
	# row_2 = cursor.fetchmany(3)
	
	# 获取剩余结果所有数据
	# row_3 = cursor.fetchall()
	
	conn.commit()
	cursor.close()
	conn.close()

详细的pymysql操作：[http://www.jb51.net/article/92516.htm](http://www.jb51.net/article/92516.htm)

----------
如果本项目对你有用请给我一颗star，万分感谢。
