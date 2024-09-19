语法：
select <tablename1>.<columnname(s)>,<tablename2>.<columnname(s)>
from <tablename1> <alias1>
natrural [inner|left|right] join <tablename2> <alias2>


注：natural join会自动合并两张表中的相同字段，效果等效于选择的合并方法