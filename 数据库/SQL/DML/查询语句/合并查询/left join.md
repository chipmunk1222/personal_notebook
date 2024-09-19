语法：
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>
from <tablename1>
left join <tablename2>
on <tablename1>.<columnname1>=<tablename2>.<columnname2>

注：左合并以第一个表为基础表，对相关数据合并后，继续列出未合并数据，并将不匹配的列中数据用NULL表示

