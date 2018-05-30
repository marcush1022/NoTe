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

Extra: 关于mysql如何解析查询的额外信息, 最坏的例子是using filesort和using temporary, 即mysql根本不能使用索引, 查询较慢;

`extra返回值的含义:`
#using filesort: mysql需要额外的步骤来对返回的行进行排序;
#using temproary: mysql需要创建一个临时表来存储结果, 通常发生在使用order by的情况;
using index: 仅仅使用了索引中的信息而没有读取表来返回信息(发生在所有的请求列都是一个索引的部分时);
range: 使用索引来返回一个范围内的行, 比如使用>或<查找时;
#ALL: 进行完全扫描;
using where: 限制行;



