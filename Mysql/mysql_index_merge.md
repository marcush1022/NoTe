#INDEX MERGE

#何时使用INDEX MERGE
where查询的字段中可能有多个条件（或JOIN）涉及多个字段，这些字段之间有AND, OR, 则就可能使用index merge, index merge其实就是：`对多个索引分别进行条件扫描，然后将他们各自的结果进行合并（intersect/union）`;

mysql 5.1之后采用了index merge，可以对多个索引分别进行条件扫描；

合并的方式：
同一个表的多个范围扫描可以对结果进行合并，合并的方式可以为：UNION, INTERSECT, 以及他们的组合（先进行内部intersect, 然后外面进行union）;

#UNION
union用于合并多个SELECT的结果集，union的语句必须有相同的列，列必须有相似的数据类型，SELECT的字段顺序必须相同；
SELECT col1(s) FROM table1;
UNION
SELECT col1(s) FROM table2;
默认union选择不重复的值，若需要重复的值使用UNION ALL;

#INTERSECTION
与UNION类似，UNION类似于OR, 只要一个值存在于第一个表或第二个表，就会被选出；INTERSECTION类似于AND, 只有存在于第一个表和第二个表才会选出;
UNION是并集，INTERSECTION是交集;
[SQL1]
INTERSECION
[SQL2]



