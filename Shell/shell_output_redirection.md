`>/dev/null 2>&1`

`执行shell命令时,会默认打开3个文件,每个文件有对应的文件描述符`
1. 标准输入(standard input, `stdin`), 文件描述符: 0, 默认情况: 从键盘获得输入
2. 标准输出(standard output, `stdout`), 文件描述符:  1, 默认情况: 输出到屏幕(即控制台)
3. 错误输出(error output, `stderr`), 文件描述符: 2, 默认情况: 输出到屏幕(即控制台)

#输出重定向
基本命令: 
1. command >filename //`标准输出重定向到文件`
2. command 1>filename //同1
3. command >>filename //`标准输出追加到文件`
4. command 1>>filename //同3
5. command 2>filename //错误输出重定向到文件
6. command 2>>filename //错误输出追加到文件

#输入重定向
1. command <filename //以filename文件作为标准输入
2. command 0<filename //同1
3. command <<delimiter //从标准输入读入,直到遇到delimiter分隔符


#重定向绑定
`>/dev/null 2>&1`
该命令分两部分
1. `>/dev/null`
将标准输出重定向到/dev/null中,`/dev/null代表linux的空设备文件, 往这个文件中写入的数据都会丢失`, 执行>/dev/null之后, 
`标准输出不会存在, 因为没有地方可找到输出的内容`;

2. `2>&1`
该命令使用了重定向绑定,`用&可以将两个输出绑定,将错误输出和标准输出绑定到同一个文件描述符`;

`>/dev/null 2>&1`的作用就是将标准输出重定向到/dev/null中(丢弃标准输出),错误输出重用了标准输出的文件描述符,因此
错误输出也重定向到了/dev/null中(丢弃错误输出), `执行之后shell,命令不会输出任何命令到控制台和文件`;

cmd >a 2>a: stdout和stderr都输出到文件a, a打开了两次stdout和stderr会相互覆盖;
cmd >a 2>&1: 只使用了一个管道, 但是已包含了stderr和stdout;
在IO效率上, cmd >a 2>&1效率更高;

#>/dev/null 2>&1 和 2>&1 /dev/null区别
linux在执行shell指令之前,`会先确定输入输出的位置,并且从左到右执行指令`; 

1. 2>&1 `先将错误输出绑定到标准输出`,此时标准输出是默认值,输出到屏幕,则错误输出输出到屏幕
2. `>/dev/null`将标准输出1重定向到/dev/null;

#若不使用重定向绑定
`>/dev/null 2>/dev/null`
`标准输出和错误输出会抢占out文件的管道,因此可能出现输出的覆盖和丢失,而且由于out文件打开了两次,效率较低`