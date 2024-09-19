简介：case从句实现功能相当于if，elseif

语法：
select <columnname1>,<columnname2>,<columnname3>
case
	 when <value1> then <res_value1>
	 when <value2> then <res_value2>
	 else <res_value3>
end
from<tablename>