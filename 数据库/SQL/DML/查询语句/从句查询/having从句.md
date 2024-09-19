语法：
select <columnname1>,<columnname2>
from <tablename>
[where]
group by <columnname1>
having count(<columnname1>)>1
[order]

注：having 从句用于过滤group by从句的结果，不可单独出现