#map(映射)的键可以是任何相等性操作支持的数据类型, 整型, 浮点, 字符串, 指针, 接口, 结构, 数组等;

`映射也是引用类型, 将映射传入函数, 函数内改变了映射的内容会影响函数外`;

`映射赋值和值的获取类似数组;`
offset:=timeZone["EST"]

`通过映射中不存在的元素取值时, 返回的是与该映射项类型一致的零值`;

判断元素是否存在:
func offset(tz string) int {
	if second, ok:=timeZone[tz]; ok {
		return seconds
	}
	return 0
}
`若tz存在, second会赋予相应的值, ok为true, 若不存在, second赋予相应的零值, ok为false`;

仅判断元素是否存在, _ 代替一般变量:
`_ , present:=timeZone[t]`

`内建函数delete删除映射的某项`;
delete(timeZone, "est")
