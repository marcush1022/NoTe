#golang函数可以多返回值

`return x, y`

#命名结果形参
#named result parameters
`go的结果形参可以命名, 像常规变量使用, 与传入的参数一样;`
`返回值形参在函数开始执行之后, 会初始化为与其类型相应的零值(zero value);`
`函数执行了没有形参的reutrn时, 将其当前值返回;`

#defer
函数推迟执行;
defer f.close()
该函数会在执行defer的函数`返回之前立即执行`, 可用于`解锁互斥或关闭读写文件`;
