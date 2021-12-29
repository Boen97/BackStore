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