`shell支持的运算符`
1. 算数运算符
2. 关系运算符
3. 布尔运算符
4. 字符串运算符
5. 文件测试运算符

#shell通过awk和expr实现数学运算

val=`expr 2 + 2`
`运算符之间需要加空格`
完整的表达式需要加`...`

乘法:
val=`expr 2 \* 2`

条件表达式
[ $a == $b ], `条件表达式放在有空格的方括号之间`

#关系运算符
`关系运算符只支持数字, 不支持字符串, 除非字符串的值是数字`
[ $a -eq $b ] //是否相等
[ $a -ne $b ] //是否不相等
[ $a -gt $b ] //左边是否大于右边
[ $a -lt $b ] //左边是否小于右边
[ $a -ge $b ] //左边是否大于等于右边
[ $a -le $b ] //左边是否小于等于右边

#布尔运算符
[ !false ] 
[ $a -lt 20 -o $b -gt 100 ] //-o或
[ $a -lt 20 -a $b -gt 100 ] //-a与

#逻辑运算符
[[ $a -lt 20 || $b -gt 100 ]] //OR
[[ $a -lt 20 $$ $b -gt 100 ]] //AND

#字符串运算符
a为"abc", b为"efd"
[ $a = $b ] //字符串相等
[ $a != $b ] 
[ -z $a ] //长度是否为0, 为0返回true
[ -n $a ] //长度是否为0, 不为0返回true
[ $a ] //字符串是否为true

