#Go的控制结构

#For
`Go的for循环统一了for和while, 包括3种形式`
`like C for`
1. for init; condition; post {}
`like C while`
2. for condition {}
`like C for(;;)`
3. for {}

`遍历数组, slice, string, channel: range`
for k, v:=range oldMap { newMap[k]=v }

for _ ,v:=range Map {} (不需要第一个值)

#Switch
`switch无需表达式;`
func switchDemo(c byte) byte {
	switch { `switch后面没有表达式将匹配true`
		case '0'<=c && c<='9':
			return c-'0'
		case 'a'<=c && c<='z':
			return c-'a'
	}
	return c
}
`(go风格)将if-else-if-else链写成switch;`

case可以列举相同的处理条件;
switch c {
	case ' ', '0', 'a':
		return 0
}

`可使用break跳出switch循环;`
switch a {
	case a!='a':
		if a=='b'{
			break
		}
}
