- 主要讨论以下几个应用层重要的软件
  1. Web
  2. email
  3. directory service（DNS）
     > DNS 是 互联网核心组件 在 应用层实现的一个典型例子
  4. video streaming
  5. P2P applications

- World Wide Web 万维网
  - 万维网可以为用户提供他们想要的信息

- Overview of HTTP

  - HTTP （HyperText transfer protocol）超文本传输协议，是 Web 应用在应用层采用的核心应用
  - 传输层使用 TCP 服务
  - HTTP 是无状态的协议
  - HTTP 主要以 URL 的形式来请求资源
  - URL (uniform resource locater) 统一资源定位器, 由 hostname 和 pathname 组成，功能主要在与定位
  - URI（Uniform resource indentifier）统一资源标识符，主要在于标识
  - URL 是 URI 的子集
  - 一个网页有很多对象组成，每个对象，例如base html, js, 图片，css 文件 都有自己的 URI
  - 互联网协议分层的好处之一：
    - HTTP 协议依赖于传输层TCP提供的协议，将可靠传输、用塞控制等功能都交给了TCP
  - 最早的HTTP协议为HTTP1.0,可以追溯到1970年，现在大部分的HTTP协议都为HTTP1.1, HTTP2正在慢慢发展中

  - Non-persistent and persistent connetctions 非持久化连接和持久化连接

    > 由于TCP协议是面向连接的，当我们在使用HTTP协议交换信息的时候，必须考虑一个问题，那就是我要采用持久化的连接还是非持久化的连接，
    > 也就是在一个TCP连接里，客户端是否可以发送多次请求

    - HTTP 协议即可以实现非持久化连接,也可以实现持久化连接,默认采用的是持久化连接
    - 另外一个 TCP 连接在两个终端是以socket对的形式存在的

  - 例如一个网页包含一个html文件,和10张图片,如果采用非持久化的连接的话,将产生11个TCP连接
  - 不同的浏览器在多个TCP连接的优化上不一样,多个并行的TCP连接能够有效提升速度
  - 完成一次HTTP请求所需要的过程和时间如下:
    1. 客户端首先发送一个请求包到服务端
    2. 服务端接受到该消息之后向客户端发送了一个ACK
    3. 客户端接受到服务端的ACK之后, 将请求的资源 + ACK 一起发送出去
    4. 服务端接受到请求的资源信息后, 将资源传输到socket,这个过程需要消耗传输文件的 transmission time

    - RTT (round trip time) 一个 packet 从 client 到 server, 再到 client 所消耗的时间
    - three-way handshake 三次握手
      1. 第一次 client 请求建立TCP连接
      2. 第二次 server 返回 ACK 确认包
      3. 第三次 client 发送 ACK + URL
    - 因此从建立连接到接受到第一个资源,所需要的时间大概为 2RTT + 在服务端传输文件所消耗的时间

- 非持久化连接的缺点:
  1. 每个请求的对象都创建一条TCP连接
  2. 每个TCP连接需要占用资源,TCP buffer, TCP 变量保存,对服务器造成很大的压力
  3. 请求时间长,每个请求对象需至少2RTT时间

- 持久化连接
  1. 多个请求对象可以在一个TCP连接中完成
  2. 支持pipelining, back-to-back request 连续的请求,NBA连续两天客场,称为back-to-back
     而 pipelining 流水线和工厂的流水线原理相似,是一直在运转的,不会因为中途的某个物件而停止流水线的运转
     因此不会因为pending 的request而导致其他请求处于等待的状态
  3. 通常来说,TCP连接在不使用后的一定时间会自动关闭,这个关闭可以自行配置

- HTTP Message Format
  - HTTP Message 分为 request message 和 response message
  - requeset message 由以下部分组成
    1. request line 请求行
       GET /dir/resource HTTP/1.1
       协议 URL HTTP协议版本
    2. header line 标题行
       HOST: www.baidu.com
       Connection: close 非持久化连接
       User-agent: Mozilla/5.0
       Accept-language: fr 希望返回fr语言版本的对象
    3. entity body 消息体
       GET 请求的消息体为空, 消息体主要用于 PUT 请求
    - HEAD 主要用于调试,不返回实际的请求对象
    - PUT 主要用于 web publishing tools
      上传对象到指定的服务器目录
      也可在应用程序中用于上传文件到指定的服务器目录
    - DELETE 删除服务器上的对象