语法：
select <columnname1>,<columnname2> 
from <tablename>
[where]
group by <columnname1>,<columnname2>
[having]

注：分组列必须在结果中出现

跨表分组查找
select <alias>.<columnname1>
from <tablename1> <alias1>,<tablename2><alias2>
where <alias1>.<columnname1> = <alias2>.<columnname2>
group by <alias1.columnname1>