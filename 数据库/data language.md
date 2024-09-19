relation: the tables that in database
attribute: the header of a column in a relation
tube:数据表的列

创建数据表
==“create table  if not exists mytable1 ("==
=="id int primary key not null, "==
=="name text not null)”==


关系代数：
![[Pasted image 20231013121118.png]]
条件筛查
where:==select * from instructor where salary > 2000;==
group by:==select * from instructor where salary > 2000 group by age;==——合并age 相同的列
having:==select * from instructor group by age having age = 2;==——保留age = 2
order by: age desc， name asc，...默认asc（desc）
嵌套聚合筛查

select count(agenum)  from
(
	select count(age)
	as agenum
	from student
	group by schools
)as countage
——相当于创建了新的表，查询结果contage为表名，agenum为列名，可以在外部使用，语法同一般表/列

列筛查
==select name，gender from instructor;==

笛卡尔乘积（获得条件下的所有组合）
==select * from instructor, course where instructor.name = course.teacher;==

自然连接（获得具有相同属性的列）
==select name, title from student natural join takes natural join course;==

指定条件链接（指定course 的属性筛找相同项）
==select name, title from takes join course using(course_id, course_name);==
等价于
==select name, title from takes, course where takes.course_id = course.course_id;==

外连接（左）（指定条件筛选合并两张表，student在左，）

==select * from student left outer join takes on student.name = takes.name;==

