#INTERFACE
`in OOP, a [protocal] or [interface] is a common means for unrelated objects to communicate with each other;`
interface是一种抽象类型，与之相对的是具体类型(int, string等);
`golang中的interface是一个方法的集合`, 是duck-type programming的一种，不关心数据只关心方法;
`使用时可以自定义自己的struct, 并实现特定interface中的方法就可以将其当作该interface使用;`

golang 中有两种interface:
1. func foo(somestring string, args ...interface{})
// 变参函数，interface意味着任何值，可传入不确定类型的参数;
2. type Foobar interface { 
       method1() 
       method2()
   }
// `用于实现泛型编程和隐藏具体实现`;

#type可实现interface
`a type can implements multiple interfaces;`
example: 

type Sequence []int

func (s Sequence) Len() int {...}
func (s Sequence) Less() bool {...}
func (s Sequence) Swap(i, j int) {...}

func (seq Sequence) String() string {
    sort.Sort(seq) // type sequence implements all method of sort, so it can be sorted by sort;
}

// sort源码
func sort(data Interface) {
    ...
}





