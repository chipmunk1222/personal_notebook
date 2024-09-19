简介：except操作符用来减去第一张表中和第二张表的重复记录

语法：
select <columnname1>
from <tablename1>
[where]
except
select <columnname2>
from <columnname2>
[where]

注：except操作符只适用于有相同记录数的操作
