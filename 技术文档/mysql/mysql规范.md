#mysql规范


##表设计
1. 数据表名与表字段使用全小写英文字母，单词之间采用下划线 (_) 作为分隔符，避免使用 MySQL 关键字（如desc 、 null 、 count 与 order 等 ）；数据库表及字段在设计时应添加与保留注释（即 COMMENT ）内容
1.  表名必须有功能模块为前缀，后面接复数名词作为表名
  bi_article、log_articel，user_info、base_system
9.	表字符集选择UTF8
1.  数据库表默认使用utf8_unicode_ci作为排序规则。

1.  如无备注，则表中的第一个id字段一定是主键且为自动增长
建表时将数据字典中的字段中文名和属性备注写入数据表的备注中(“PK、自动增长”不用写)
3.	如无说明，建表时一律采用innodb引擎
4.	库名、表名、字段名必须使用小写字母，“_”分割
5.	存储精确浮点数必须使用DECIMAL替代FLOAT和DOUBLE
6.	建议使用UNSIGNED存储非负数值
8.	尽可能不使用TEXT、BLOB类型
10.	使用VARCHAR存储变长字符串

##索引
1.	非唯一索引必须按照“idx_字段名称_字段名称[_字段名]”进行命名。
2.	唯一索引必须按照“uniq_字段名称_字段名称[_字段名]”进行命名。
3.	索引名称必须使用小写。
4.	索引中的字段数建议不超过3个。
5.	单张表的索引数量控制在5个以内。
6.	不建议使用组合主键，如果有这种情况，重新定义一个自增主键。
7.	唯一键不和主键重复。
8.	索引字段的顺序需要考虑字段值去重之后的个数，个数多的放在前面。
9.	使用EXPLAIN判断SQL语句是否合理使用索引，尽量避免extra列出现：Using File Sort，Using Temporary。
10.	UPDATE、DELETE语句需要根据WHERE条件添加索引。
11.	不建议使用%前缀模糊查询，例如LIKE “%weibo”。
12.	对长度过长的VARCHAR字段建立索引时，添加crc32或者MD5 Hash字段，对Hash字段建立索引。
13.	合理创建联合索引（避免冗余），(a,b,c) 相当于 (a) 、(a,b) 、(a,b,c)。
14.	合理利用覆盖索引。
##sql语句
1.	SQL语句中IN包含的值不应过多。
2.	UPDATE、DELETE语句不使用LIMIT。
3.	WHERE条件中必须使用合适的类型，避免MySQL进行隐式类型转化。
4.	SELECT语句只获取需要的字段。
5.	SELECT、INSERT语句必须显式的指明字段名称，不使用SELECT *，不使用INSERT INTO table()。
6.	使 用SELECT column_name1, column_name2 FROM table WHERE [condition]而不是SELECT column_name1 FROM table WHERE [condition]和SELECT column_name2 FROM table WHERE [condition]。
7.	WHERE条件中的非等值条件（IN、BETWEEN、<、<=、>、>=）会导致后面的条件使用不了索引。
8.	避免在SQL语句进行数学运算或者函数运算，容易将业务逻辑和DB耦合在一起。
9.	INSERT语句使用batch提交（INSERT INTO table VALUES(),(),()……），values的个数不应过多。
10.	避免使用存储过程、触发器、函数等，容易将业务逻辑和DB耦合在一起，并且MySQL的存储过程、触发器、函数中存在一定的bug。
11.	避免使用JOIN。
12.	使用合理的SQL语句减少与数据库的交互次数。
13.	不使用ORDER BY RAND()，使用其他方法替换。
14.	建议使用合理的分页方式以提高分页的效率。
15.	统计表中记录数时使用COUNT(*)，而不是COUNT(primary_key)和COUNT(1)。
16.	在 SQL 语句的编写中，凡是 SQL 语句的关键字一律大写，如：SELECT、ORDER BY、 GROUP BY、 FROM、 WHERE、 UPDATE、 INSERT INTO、 SET、 BEGIN、 END 等。




##操作说明
