# the type of transport services provided by the Internet(TCP/IP network)
1. TCP
2. UDP

- TCP

  > TCP 提供了面向连接的可靠传输

  - connection-oriented service 面向连接的服务

    - 需要发送 control information 来提醒双方做好连接的准备，也就是所谓的 handshaking 过程
    - 握手成功之后，就建立了一条 TCP connetction, 这条连接是全双工，双方可以同时同时发送消息给对方
    - 当双方消息发送完成之后，需要一方手动关闭连接

  - reliable data transfer service

    > TCP 的可靠传输能够提供错误检测，并且能够保证消息的顺序和完整性

    - error checking
    - proper order

  - congestion-control 用塞控制

- UDP

  > 提供最基础的服务，在发送消息之前不需要握手建立连接，不可靠
  >
  > 到达的消息可能是无序的
