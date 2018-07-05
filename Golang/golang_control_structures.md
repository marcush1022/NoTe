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
for k, v := range oldMap { newMap[k] = v }

for _, v := range Map {} (不需要第一个值)

#Switch
`switch无需表达式;`
func switchDemo(c byte) byte {
	switch { `switch后面没有表达式将匹配true`
		case '0' <= c && c <= '9':
			return c - '0'
		case 'a' <= c && c <= 'z':
			return c - 'a'
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
	case a != 'a':
		if a == 'b'{
			break
		}
}

#Defer
预设函数调用（推迟执行函数）, 该函数会在执行defer的函数返回之前立即执行;
(无论返回路径都必须释放资源的函数，如解锁互斥和关闭文件);
作用:
1. 确保不会忘记关闭文件；
2. 关闭和打开很近;
推迟的函数按LIFO的顺序执行:
for i:= 0; i < 5; i ++ {
    defer fmt.Println(i)
}
// 输出43210

