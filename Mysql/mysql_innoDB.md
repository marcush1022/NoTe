#INNODB

Record-level-lock分为3种:
#LOCK_REC_NOT_GAP(Record Lock): 只是锁记录但是不锁记录之前的GAP，RC隔离级别一般使用该锁;

#LOCK_GAP(GAP Lock): 只锁住一段范围，不锁记录本身，通常表示两个索引记录之间，或索引上的第一条记录之前，或最后一条记录之后的锁, 一般在RR级别使用GAP Lock;

#LOCK_ORDINARY(Next-Key Lock): 包含记录本身及记录之前的GAP, Mysql默认使用RR隔离级别，Next-key正是用于解决RR隔离级别下的幻象读问题（幻象读：一个事务执行相同的查询会看到不同的记录）;

假设已有记录为1,2,3,6, 当使用SELECT...WHERE col < 5 FOR UPDATE, 若不在3, 6之间加GAP锁，另一个进程可能插入一条数据4, 下次执行SELECT...WHERE ... FOR UPDATE时会看到不同的结果;

因此在执行INSERT之前需要判断记录是否加锁;

#LOCK_S(共享锁): 共享锁的作用是在一个事务读取一条记录时，不希望其被其他的记录更改, 但是所有的读请求的共享锁是不冲突的;
InnoDB中使用请求共享锁的情况：
1. 普通查询在隔离级别为serializable时会给记录加共享锁（非事务读（auto-commit）在serializable级别下无需加锁）;
2. 类似SQL SELECT ... IN SHARE MODE会给记录加共享锁，其他线程可以并发查询但不能修改; 
3. 通常INSERT不加锁，但是如果插入或更新记录时检查到duplicate key, 对于普通的INSERT/UPDATE会加共享锁;

#LOCK_X(排他锁)：目的是防止一条记录被并发修改，UPDATE或DELETE或SELECT FOR UPDATE会给记录加排他锁

#通常事务锁在事务提交时被释放，除以下几种情况:
1. AUTO-INC锁在SQL结束时直接释放
2. 在RC隔离级别执行DML语句时，从引擎层返回到server的记录若不满足where条件, 立刻unlock;


