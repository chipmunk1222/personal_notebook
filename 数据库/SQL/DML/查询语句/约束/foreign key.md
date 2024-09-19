约束条件：foreign key用来指向该表或其他表的primary key或unique key，被指的为父表，指向的为子表，

初始化：
create table <tablename>(
<columnname1> <datetype1>,
<columnname2> <datetype2> ,
constraint [<constraintname>] foreign key(<columnname>)
references<parent_tablename>(<parent_columnname>）
[on delete <deleteaction>]
[on update<updateaction>]
)

关键词：
no action：默认，无行动
set default：设为默认值
set null：设为空值
cascade：删除对应记录


修改：
alter table <tablename>
add [constraint <constraintname>] foreign key(<columnname1>)
references <parent_tablename>(<parent_columnname>)
[on delete<deleteaction>]
[on update<updateaction>]


删除：
alter table <tablename>
drop constraint<constraintname>