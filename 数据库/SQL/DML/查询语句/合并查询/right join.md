语法：
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>
from <tablename1>
right join <tablename2>
on <tablename1>.<columnname1>=<tablename2>.<columnname2>

注：右合并为左合并的逆操作，即将第二个表作为基础表，将第一个表并入