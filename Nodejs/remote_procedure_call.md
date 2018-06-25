#RPC, Remote Procedure Call
一种进程间的通信方式，允许程序调用另一个地址空间（通常是共享网络的另一台机器）的过程或函数, 而不需要显示的实现这个方法或函数的细节;

#RPC的结构
1. User;
2. User-stub;
3. RPCRuntime;
4. Server-stub;
5. Server;

user即客户端，user希望发起远程调用时，则调用本地的user-stub, user-stub进行编码然后通过本地的RPCRuntime将接口，方法和函数传递到远程的RPCRuntime, 远程的RPCRuntime接受请求后交给server-stub进行解码，调用结果返回到user;

RPC的主要目标是使构建分布式计算更容易;

RPC调用分类：
1. 同步调用；
2. 异步调用;
`异步和同步的区别是是否等待服务端执行完成并返回结果；`

RPC的server通过RPCServer导出远程接口的方法，client通过RPCclient导入远程接口的方法，client像调用本地方法一样调用远程接口的方法；

#PROTOCAL BUFFERS
grpc默认使用protocal buffers，是一种结构数据序列化的机制，使用proto file创建grpc服务，使用protocal buffers消息类型定义方法参数和返回类型；


