# 泛型编程(generic programming): 代码不是针对特定的类型(例如适用int不适用string)有效, 而是对大部分类型的参数都是有效的;

`golang不支持泛型, 但是可以用interface实现泛型`;

#duckTyping: 判断一个对象的类型不是通过其类型定义来判断, 而是根据其是否满足某些特定的方法和属性判断;

#golang中的interface
`golang中的interface是一组方法的集合, 可视为一种定义内部方法的动态数据类型, 任意实现了这些方法的类型都可视为该动态数据类型`;
不关心`数据`, 只关心`行为`;

golang中有两种interface, `一种是类型, 一种是定义`;

#interface{}作为任意值
func foo(v interface{}) {}
`此时interface可以传入任意类型的值(int, string, 结构体等)`;

`类型断言`
`传入的参数为interface类型, 通过类型断言来获得参数类型`;
func foo(value interface{}) {
	switch v:=value.(type) {
		case string :
			fmt.Println("is string!")
		case int :
			fmt.Println("is int!")
	}
}

`指定类型`
`通过value.(类型)将interface传入的参数转化为指定类型`;
func foo(value interface{}) {
	fmt.Println("value is a string, read as: "+value.(string))
}

#interface作为接口
type Database interface {
	Read()
	Write()
}

Mysql结构体实现了Database接口:
type Mysql struct {}

func (m Mysql) Read() {}
func (m Mysql) Write() {}


#使用interface的优点

1. `Write generic algorithm(泛型编程)`
#例: 泛型编程, 标准库的sort
type Interface interface {
	Len() int
	Less(i, j int) bool
	Swap(i, j int)
}

func sort(data Interface) {
	n:=data.Len()
	maxDepth:=0
	for i:=n; i>0; i>>1 {
		maxDepth++
	}
	maxDepth*=2
	quickSort(data, 0, n, maxDepth)
}
`sort函数的形参是Interface, 含有3个方法, 任何实现了这3个方法的元素类型都可以使用sort函数`;

type Person struct {
	Name string
	Age int
}
`Person实现了Interface的3个方法;`
type ByAge []Person

func (a ByAge) Len() int { return len(a) }
func (a ByAge) Less(i, j int) bool { return a[i].Age < a[j].Age }
func (a ByAge) Swap(i, j int) { a[i], [j]=a[j], a[i] }

//package sort
func main() {
	people:=[]Person {
		{"a", 1},
		{"b", 2},
		{"c", 3},
	}
	//使用interface Sort
	`sort.Sort(ByAge([people]))`
}

2. `Hiding Implement Detail(隐藏实现细节)`
...


#golang的方法与函数
`函数:`
func foo() { fmt.Println("this is a function") }
`方法:`
type Foo struct {
	name string
	id int
}
func (f Foo) foobar() { fmt.Println("this is method") }
