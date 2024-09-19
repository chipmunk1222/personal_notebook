简介：union all操作符用来返回两张表中的所有记录

语法：
select <columnname>
from <tablename1>
[where]
union all
	select <columnname>
	from<tablename2>
	[where]

注：union all操作符必须保证字段数相同
