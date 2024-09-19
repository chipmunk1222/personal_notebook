语法：
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>
from <tablename1>
full join <tablename2>
on <tablename1>.<columnname1>=<tablename2>.<columnname2>

注：全合并将两个表中不匹配的数据全保留，并且先列出第一个表的所有记录