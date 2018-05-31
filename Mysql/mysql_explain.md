explain显示了mysql如何使用索引来处理select查询和链接表;

id:

select_type:

table: 显示数据是关于哪个表

type: 显示的是访问的类型, 从好到差依次是: 
system > const > eq_req > ref > fulltext > ref_or_null > index_merge > unique_subquery >index_subquery > 
range > index > ALL
一般查询至少需要达到range, 最好达到ref;

possible_keys: 可能应用于这张表中的索引, 为空表示无可能的索引;

key: 实际使用的索引，为空表示无可用索引, 可在select中使用USE INDEX(indexname)强制使用索引或IGNORE INDEX(indexname)强制
忽略索引;

key_len: 显示使用的索引的长度，不损失精确度的情况下索引越短越好;

ref: 显示索引的哪一列被使用，如果可能的话是一个常数;

rows: mysql认为必须检查的用来返回数据的行数;

Extra: 关于mysql如何解析查询的额外信息, 最坏的例子是`using filesort和using temporary`, 即`mysql根本不能使用索引`, 查询较慢;

`extra返回值的含义:`
#using filesort: mysql需要额外的步骤来对返回的行进行排序(不能由使用的索引直接完成排序, 不一定产生性能问题，但是在查询较频繁的情况下会有一定影响);
#using temproary: mysql需要创建一个临时表来存储结果, 通常发生在使用order by的情况;
using index: 仅仅使用了索引树中的信息而没有读取表来返回信息(发生在所有的请求列都是一个索引的部分时), 性能较高;
range: 使用索引来返回一个范围内的行, 比如使用>或<查找时;
#ALL: 进行完全扫描;
using where: where限制行(有where时);
using join buffer: 表示在获取连接条件时没有使用索引, 需要使用缓冲区来存储中间结果, 根据查询的具体情况可能需要添加索引来改进性能;
impossible where: 根据where没有复合条件的行;

`select_type返回值的含义:`
SIMPLE: 简单SELECT;
PRIMARY: 最外层SELECT;
UNION: UNION中的第二个或后面的SELECT语句;
SUBQUERY: 子查询的第一个SELECT;
DEPENDENT SUBQUERY: 子查询的第一个SELECT, 取决于外面的查询;

`type返回值的含义`
const: `表最多一个匹配行, 在查询开始时读取，因此是常数，查询速度较快, 因为只读取一次`;
#eq_ref???: 对于每个来自前一个表的行组合，从该表中读取一行, 仅次于const;
#ref???: 对于每个来自前一个表的行的组合，所有匹配索引值的行冲该表中读取;
index_merge: 表示使用了索引合并优化方法;
unique_subquery: 该类型替换了IN中的子查询, 是一个索引查找函数，比子查询更快;
index_subquery: 类似unique_subquery, 可替换IN子查询, 但只使用与以下形式: value IN (SELECT key_column FROM single_table WHERE some_expr);
range: 只查询指定范围的行，使用索引来选择行;
index: 该链接类型与ALL相同，不同的是是在索引树中查询，通常比ALL快;
ALL: 全表扫描, 最慢的连接类型;

#EXPLATIN优化

#利用索引获取有序数据
利用索引获取有序数据显示using index, 利用文件排序获取有序数据显示using filesort;

Mysql在查询时最多使用一个索引，因此当where使用了索引时，在排序时就不使用索引了;

order by使用索引的条件:
???

避免使用IN和NOT IN, 因为效率较低, 尽量使用EXISTS和NOT EXISTS代替，在查询确定有限集合时使用IN和NOT IN;


