约束条件：字段对应记录既不能为空，也不能重复，等同于not null+unique
一般情况下一张表只能有一个主键（多个不违法，但不推荐）

初始化：
create table <tablename>(
<columnname1> <datetype1>,
<columnname2> <datetype2> primary key,
)

修改：
alter table <tablename>
add [constraint <constraintname>] primary key(<columnname1>)


删除：
alter table <tablename>
drop constraint<constraintname>