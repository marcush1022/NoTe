#GOLANG HTTP

`golang标准库"net/http"提供了http相关的接口, 封装了内部TCP连接和报文解析的细节，只需使用http.request和http.ResponseWriter进行交互即可;`
`即写一个handler, 请求通过参数传入，然后进行请求的数据处理，结果写入response;`

#EXAMPLE    

type FooHandler struct{}

func (fh *FooHandler) ServeHTTP(w http.ResponseWriter, req *http.Request) {
	w.Write([]byte("FOOOOOOOOOBARRRRRRRRRRRRRR"))
}

func TestHttp() {
	// Handle func(pattern string, handler Handler)
	http.Handle("/1", &FooHandler{})
	http.ListenAndServe(":3000", nil)
}
handler的接口原型：
type Handler interface {
	ServeHTTP(ResponseWriter, *Request)
}
`每次使用handler时都需要实现handler接口并实现serverHttp方法;`

#封装
`HandleFunc: 将特定的函数直接作为handler;`
func fooHandlerFunc(w http.ResponseWriter, req *http.Request) {
	for {
		io.WriteString(w, "foo")
	}
}

func TestHttp() {
	http.HandleFunc("/2", fooHandlerFunc)
	http.ListenAndServe(":3000", nil)
}
`handlerFunc最终使用的依然是serverHttp, 只是会直接使用f(w, r);`
type HandlerFunc func(ResponseWriter, *Request)

// ServeHTTP calls f(w, r).
func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request) {
	f(w, r)
}

#路由
ServeMux: `可注册多个url和handler的关系, 并自动将请求对应到相应的handler进行处理`;
EXAMPLE:
func fooHandler(w http.ResponseWriter, r *http.request) {
    io.WriteString(w, "THIS IS FOO\n")
}

func barHandler(w http.ResponseWriter, r *http.request) {
    io.WriteString(w, "THIS IS BAR\n")
}

func main() {
    mux:=http.NewServerMux()
    mux.HandlerFunc(fooHandler)
    mux.HandlerFunc(barHandler)
    http.ListenAndServer(":3000", mux)
}

`net/http默认后台默认创建并使用DefaultServeMux, 因此可以在不使用mux时使用路由功能`;

#HANDLER的两个参数: http.Request 和 http.ResponseWriter
#1. REQUEST
即封装的用户请求, 包含URL，method，header等参数;



#2. RESPONSE_WRITER
responseWriter是一个接口，定义了3个方法, 
1. header() // 返回一个header对象，可以通过set()设置头部;
2. write() // 写response的主体部分;
3. wirteHeader() // 设置 status code;