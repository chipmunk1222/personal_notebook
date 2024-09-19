语法：
select <columnname> 
from <tablename>
where condition

where子查询
select <columnname1>
from <tablename1>
where <columnname2>=(select <columnname3>
					 from <tablename2>
					 where condition)