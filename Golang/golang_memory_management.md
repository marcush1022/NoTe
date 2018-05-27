#golang内存管理
`基于tcmalloc`

`golang三个基本概念 G, M, P`
 G: Goroutinue执行的上下文环境
 M: 操作系统进程
 P: Processer `进程调度的关键, 进程调度器`, 约等于CPU

`一个Goroutinue的运行需要G+M+P`

`具体分配到栈还是堆
  golang中的变量只要被引用就一直存活, 存储在栈上还是堆上由内部实现决定, 与语法没有关系.`

 编译器自动决定将变量分配在栈还是堆, 编译器会做`逃逸分析`, `当函数的局部变量的生命周期没有离开函数的作用范围, 则将其分配在
 栈上, 否则分配在堆`, 所以无需担心memory leak; 对于new的变量, 编译器同样会进行逃逸分析, 决定分配在堆还是栈, `并不一定是堆`;

`golang会将函数的局部变量分配到栈帧 (stack frame) 上, 如果不确定在函数返回后变量不被引用, 则编译器将其分配到堆上
  当局部变量较大时, 也应该将其分配到堆上.`

`如果一个变量被取地址, 则其有可能被分配到堆上.`

`需要对变量进行逃逸分析, 如果变量在函数return之后没有被引用, 则应当将其分配到栈上.`

#关键数据结构
`mcache`: per-P cache, 可认为是local cache. `每个G的运行需要绑定到P, mcache是每个P的cache, 这样做的好处是分配内存不需要加锁.`
`mcentral`: 全局cache, `mcache不够时向mcentral申请`.
`mheap`: 当mcentral也不够时, `通过mheap向操作系统申请`.
`可视为多级内存分配器`
mspan: `span在tcmalloc中是内存管理的基本单位`, 一般以链表的形式使用,


#内存分配的流程
1. `object size>32k`, 直接用mheap分配;
2. `object size<16k`, 用mcache中的小对象分配器tiny分配, (`tiny是一个指针, 指向开始地址`);
3. `object size>16k && object size<=32k`时, 使用macahe中的size class分配;
4. 当mcache空间不足时, 向mcentral申请;
5. mcentral空间不足时, 向mheap申请, 并切分;
6. mheap没有足够的span时, 向操作系统申请;

#内存申请
`用于内存分配`
`new, make`

`new只用于分配内存; make用于slice, map, channel的初始化, 不返回指针;`

1. new并不初始化内存, `只是将其置零, new(T)会为T类型的新项目分配置零的内存, 并返回其地址`, 一个*T类型的值;
  (GO术语: 其返回一个`指向新分配的类型为T的指针`, 这个指针指向的空间置为零值(zero value);)

2. make(T, args)与new(T)不同, 只用来创建`map, slice, channel`, 并返回一个初始化的(不是置零), 类型为T的值(不是*T);
  之所以不同是因为这`3个类型是引用数据类型, 使用前必须初始化`;
  例如slice是一个三元描述符, 包含一个`指向数据的指针, 长度, 容量`, `在这些属性初始化之前, slice都是nil`, make初始化这三项时为其准备可用的值;
  例: `make([]int, 10, 100)`分配一个长度为100的`数组`, 初始长度为10, 容量为100, `改slice引用含有前10个元素的数组`; `new([]int)`返回一个指向新分配的
  被置零的slice结构体的`指针`, 即`指向值为nil的slice指针`;
  `make不返回指针, 要使用指针, 则使用new`;
