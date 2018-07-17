#INIT
`init函数用于包的初始化`
`golang的保留函数2个: init(可用于任何package)和main(只能用于package main)`;

1. init函数用于`程序执行前进行包的初始化操作`, 如初始化包里的变量等;
2. 每个包可以含有`多个(0~n个)init函数`;
3. 包的每个源文件也可以有`多个init函数`;
4. `同一个包中的init函数的执行顺序`go没有明确的定义(说明); ???
5. 不同包的init函数按照`包的导入的依赖关系`决定执行顺序;
6. init函数`不能被其他的函数调用`(显示调用会报错未定义), 而是在main函数执行之前自动调用;

#强烈建议在一个package中只写一个init函数

`golang程序的初始化和执行顺序：`
1. 若main函数导入了其他的package, 这些package会在编译时依次导入, `若一个package被多个package导入, 这个package只会导入一次`(如fmt);
2. 当一个package导入时, 若其还导入了其他的package, 其他的package首先导入, 进行变量常量的初始化, 然后执行init函数; 
3. 当所有的package导入完时, 进行main package的变量和常量的初始化, 然后执行main package中的init函数, 然后执行main函数;





