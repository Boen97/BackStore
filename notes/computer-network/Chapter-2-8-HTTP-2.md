## HTTP/2
- HTTP/2 协议在2015年提出，据统计，至2020年，有40%的网站和浏览器支持了HTTP/2协议
> HTTP/2 最主要的改进在于使用 单条TCP连接实现了 多路复用 的功能，并且对 HTTP header fields 进行了压缩，具体的协议和字段没有做修改
> the primory goal of HTTP/2 是为了减少在传输一个web page时的 TCP 连接数量

- HTTP/1.1 协议存在 HOL (Head of Line) bloking problem
  - HOL bloking
    假设一个web page,由最上方的video clip和下方的很多small object 组成, 最先且最大的video clip 阻塞了之后的小对象
  - parallel TCP connections
    很多浏览器为了解决 HOL blocking 和 欺骗 TCP 用塞控制协议获取更多带宽，往往会同时建立5/6个TCP连接

- HTTP/2 Framing
> HTTP/2 最重要的增强功能:
> beak messages into smaller binary frames, and interleave them

- 回想之前没有使用 HTTP/2 Framing HOL 的场景
  有一个1000 frames 大小的 big object, 还有两个 small object, 分别占用 2 frames
  由于 frames 没有采用 interleave 没有交织在一起，导致 small object 只能在 1000 个 frames 传送完毕之后再进行发送
- 使用了 HTTP/2 Framing 之后
  小对象在大对象传递完第一个 frame 之后就开始发送，大大减少了用户的预期时间

- client 和 server 的 message 都一样采用了 Framing 的技术
- frames 采用 binary encode 的好处
  1. more efficient to parse
  2. smaller frame
  3. less error-prone

- Response Message Prioritization and Server Push
  1. Response Message Prioritization
     
     当一个网站同时发起很多请求时，可以给每个请求添加对应的权重值，server 根据对应的权重值返回 response message
     
  2. Server Push
  
     Server 可以在客户端还没有请求资源的时候，自动将客户端所需要的对象 Push 到客户端
     能够大大减少 waiting for request 所带来的延迟，这个功能完全可以在网页上实现，因为一个网页在一开始需要什么对象，完全可以在 server 端进行分析

## HTTP/3

- HTTP/3 主要是为了支持运行 QUIC 协议，HTTP/2中的功能也都有
- QUIC 是一个全新的协议，运行在 应用层，使用UDP 协议实现，具有
  message multiplexing (interleaving), per-stream flow control, and low-latency connection establishment.
