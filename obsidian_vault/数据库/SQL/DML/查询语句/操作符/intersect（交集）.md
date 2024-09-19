简介：intersect操作符实现取多个表的交集记录，可用来检验记录

语法：
select <columnname1>,<columnname2>
from <tablename1>
[where condition]
intersect 
	select <columnname3>,<columnname4> 
	from <tablename2>
	where [condition]


注：intersect操作符的使用必须保证两张表的搜索记录数量相同