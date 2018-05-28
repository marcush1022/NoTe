#反射
# `反射在运行时检查类型和变量<大小, 方法等>`
  reflect.ValueOf, reflect.TypeOf, 类型和值

#fmt格式化输出
`用"%v"标志, 它可以以适当的格式输出任意的类型( 包括数组和结构) `
`使用Print和Println不需要格式化输出, 会根据参数类型自动转换. Print默认将参数以%v输出, Println在Print的基础上增加换行.`
`Println还会在参数之间加入空格`

普通占位符
# `%v 相应值的默认格式`
  打印结构体时, %+v会添加字段名
# `%#v 相应值的GO语法表示`
  Printf("#v", site) ---> main.Website{Name:"studygolang"}
# `%T 相应值的类型的GO语法表示`
  Printf("%T", site) ---> main.Website
# `%% 字面上的百分号, 并非占位符`
  Printf("%%") ---> %

布尔占位符
# `%t Printf("%t", true) ---> true`

整数占位符
`%b 二进制
%d 十进制
%c unicode码表示的字符 Printf("%c", 0x4E2D) ---> 中
%U unicode格式 Printf("%U", 0x4E2D) ---> U+4E2D`

浮点数
`%f 有小数无指数`

字符串与切片
`%s 字符串
%q 带引号的字符串`

打印值的类型
%T
