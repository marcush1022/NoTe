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