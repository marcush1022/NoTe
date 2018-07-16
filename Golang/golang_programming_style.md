#GOLANG PROGRAMMING STYLE

#文件名
文件名用小写;

#包名
用小写;

#接口名
单个函数的接口名使用er作为后缀, 如Reader;
接口的实现去掉er;

两个函数的接口名综合两个函数，如
type writeReader interface {
    Write([]byte) (int, error)
    Reader() error
} 

三个函数及以上的接口名类似结构体
type Car interface {
    Start() error
    Stop() error
    Display() error
}

#变量
常量: 大写, 采用下划线;

#import
import (
    "fmt"
    "time"
)
多种类型的包:
import (
    "fmt"
    "time"

    "folder/someFile"
    "folder2/someFile2"
)
不要使用相对路径;

#函数名
驼峰命名, 尽量不使用下划线;

#错误处理
error作为函数的返回值返回，需要尽快处理;
采用独立的错误流进行处理;
例：
if err != nil {
    // some handle option
    return 
}
//normal option
若返回值需要初始化:
res, err:= f()
if err != nil {
    // some handle option
    return 
}
// use res

#panic
逻辑处理中禁用panic
main包中只有无法继续运行时使用panic, 如文件读取失败，数据库连接失败等;
但是其他的package的对外接口中不能有panic, 只能在包内使用;

####################################################################################################################

1. 未使用的局部变量会报错，但是未使用的全局变量不会报错;
2. 未使用的导入包会报错；
3. 短变量声明只能在函数体内;
a:=1 // 报错
func main() {
    dosomething()
}
4. 不能使用nil显示的初始化变量;
var a = nil // 报错
var str string = nil // 报错
5. 空的slice可以添加元素，但是空的map不行;
var s []int
s=append(s, 1) // ok
var m map[string]int
m["one"] = 1 // error
6. cap不能用于map；
m := make(map[string]int,99)
cap(m) // error
7. 数组作为函数参数传递不会退化为指针，数组以副本的形式传参；
8. 用slice作为数组的替代传参, slice是引用类型;
9. 不能使用自增前缀;
a:=1
++a // error




