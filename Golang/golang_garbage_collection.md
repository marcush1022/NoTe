#Golang GC
1. 何时触发GC

(两种GC触发方式, `自动检测和用户主动调用`)
`在堆上分配的对象大于32kb时检测是否满足GC的条件, 是则进行GC;`
forceTrigger || memstats.heap_live>=memstats.gc_trigger
`forceTrigger是强制GC, 后面的是当前活动的对象大于设置的阈值, malloc和free时heap_live会一直更新`

2. GC的方法是`三色标记法`, 标记-清理(Mark and Sweep)算法

3. write barrier(写屏障)
`为什么需要写屏障, 因为GC算法与用户的程序同时执行, 用户程序会一直修改内存, 所以需要记录下来;`

触发机制
1. 申请内存时, 检查当前已分配的内存是否大于上次GC的内存的2倍, 若是则触发;
2. 监控线程发现上次的GC已经超过2分钟了, 触发;
