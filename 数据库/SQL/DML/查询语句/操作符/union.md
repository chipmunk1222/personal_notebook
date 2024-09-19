简介：union操作符用来删除多张表中的重复记录，并返回所有非重复记录

语法：
select <columnname>
from <tablename1>
[where]
union
	select <columnname>
	from<tablename2>
	[where]

注：union操作符必须保证字段数相同

