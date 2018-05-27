#构造函数与复合字面(composite literals)
`返回初始化的构造函数`
func newFile(fd int, name string) * File{
	f:=new(File)
	f.fd=fd
	f.name=name
	f.info=nil
	f.id=0
	return f
}
`等价于:`
func newFile(fd int, name string) * File{
	f:=File(fd, name, nil, 0)
	return &f
}
`等价于:`
composite literals的字段必须`顺序全部列出`;
func newFile(fd int, name string) * File{
	return &File{fd, name, nil, 0}
}
`未全部列出的需要标明`
return &File{fd: fd, name:name}

`composite literals不包含任何字段与new等价`;
new(File) ==> &File{}

`composite literals可用于创建数组, 切片, 映射`;
a:=[...]string {Enone: "a", Eio: "b", Ein: "c"}
b:=[]string {Enone: "a", Eio: "b", Ein: "c"}
c:=map[int]string {Enone: "a", Eio: "b", Ein: "c"}
