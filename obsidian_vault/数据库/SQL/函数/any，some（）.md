简介：any（）和some（）具有相同作用，必须用在比较操作符后，用来和存在的条件比较

语法：
select <columnname>
from <tablename>
where
<columnname> (operator) any( select <columnname> from <tablename> [where])

注：any（），some（）比较的类型必须一致，括号中必须是一个子查询