#TRANSACTION

`事务由作为同一个单元的多条SQL语句组成，当一条语句执行失败时，整个单元会回滚, 即只有当事务中的所有语句全部成功执行时才说明事务成功执行;`

`在成功执行插入语句时，若无commit, 再次执行commit或BEGIN或start transaction时会首先将该链接中之前未commit的更改commit, 相当于执行了commit;`



