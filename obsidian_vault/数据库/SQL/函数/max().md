简介：用以返回最大的记录，可适用于数字，字符，日期等类型

语法：
select max(<columnname>) 
from <tablename>
[where]
[group by]

注：max（)不能直接用在where从句中，需要先写子查询，用于组中时，返回每组的最大值