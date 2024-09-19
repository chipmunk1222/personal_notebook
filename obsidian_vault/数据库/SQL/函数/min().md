简介：用以返回最小的记录，可适用于数字，字符，日期等类型，等同于max（）

语法：
select min(<columnname>) 
from <tablename>
[where]
[group by]

注：min（)不能直接用在where从句中，需要先写子查询，