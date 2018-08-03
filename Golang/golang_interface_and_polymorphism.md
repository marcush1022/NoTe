#INTERFACE AND POLYMORPHISM

golang 中有两种interface:
1. `variadic function`:
func foo(somestring string, args ...interface{})
// 变参函数，interface意味着任何值，可传入不确定类型的参数;

非侵入性接口，去掉了繁杂的继承体系
2. type Foobar interface { 
       method1() 
       method2()
   }
// `用于实现泛型编程和隐藏具体实现`;

# C++ 虚函数 虚表 V-table
class Base 
{
    public:
    virtual void f() {...}
    virtual void g() {...}
    virtual void h() {...}
}

通过虚指针访问虚表中的函数, 单继承时，派生类会继承基类的虚表，若声明了新的虚函数，其虚函数append在虚表的基类函数后；
若重新声明已有函数则覆盖；
多继承时同理，派生类的声明的新的虚函数会append在按照声明顺序的第一个基类的虚表后面，有覆盖则覆盖;

`虚表中的virtual function 可在编译期获知`???, 其地址是不变的，`执行期不可对其进行改变`（新增或替换）;

V-table其构建与存取皆可由compiler完全控制，不需要执行期的介入;

# Golang interface 虚表
type Stringer interface {
    String() string
}

type Binary uint64

func (i Binary) Get() uint64 {
    return uint64(i)
}

func (i Binary) String() string {
    return strconv.Uittob64(i.Get(), 2)
}

# 接口类型的内存布局
`一个接口变量可以存储任意值（非接口），只要该值实现了接口的所有方法`；
`interface在内存中由两部分组成，指针tab指向虚表，指针data指向实际引用的数据`;
`虚表的内容：实际的类型信息和该接口所需要的方法集`（满足Stringer接口的`函数指针列表`func[0], func[1], func[2]...）；
`interface的虚表在运行时生成`；

通过interface调用func: 
s.table --> func[0](s.data)

C++的每一个类都会创建一个方法集, 即虚表，当使用继承机制时，C++的对象结构中就会多存一个虚指针，每个虚指针指向方法集的不同部分；
当派生类重写基类函数时，将表中相应的函数指针转为子类自己实现的函数，没有重写则指向基类的实现；

golang每种类型同样会生成一个方法集，不同的是interface的虚表是在运行时生成（C++在编译期生成, 但是函数表现出多态是在运行期决定）；
如：当遇到s:=Stringer(b)时，会生成Stringer对应于Binary类型的虚表;






