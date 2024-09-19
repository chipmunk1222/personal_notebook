语法：
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>
from <tablename1> <alias1>
inner join <tablename2> <alias2>
on <tablename1>.<columnname1> = <tablename2>.<columnname2>

注：表1表2顺序不会影响查询结果

等效于where从句
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>
from <tablename1> <alias1>,<tablename2><alias2>
where <alias1>.<columnname1> = <alias2>.<columnname2>

多表内连接
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>，<tablename3>.<columnname(s)>
from <tablename1> <alias1>
inner join <tablename2> <alias2>
on <tablename1>.<columnname1> = <tablename2>.<columnname2>
inner join <tablename3> <alias3>
on <tablename2>.<columnname1> = <tablename3>.<columnname3>