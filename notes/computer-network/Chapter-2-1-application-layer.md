- application 应用存在于互联网的终端，互联网对于应用来说，就像基础设施一样。当我们在开发应用的时候，直接使用现成的基础设施即可
- Application Architectures
  - client-service architecture
    - service is always on, and has a fixed, well-known address
  - P2P architecture
    - 高度分散 highly decentralized 面临安全、性能、可靠性的挑战
    - self scalability 可伸缩性

- Processes Communication

  > how programs in multiple end systems can communicate with each other

  - 应用程序之间的交流实际上是进程 process 之间的交流
  - 不管是同一主机还是不同主机上的进程都是通过交换 message 来互相交流的


- The Interface bewteen Process and the Computer Network

  - **socket** 进程通过socker接口，获取底层的网络基础上设施，来传输 message
  - socket 也被称为 API between application and network
  - 软件开发人员主要负责应用层端，很少需要介入socket的网络传出端
  - 软件开发人员在socket的传输端仅仅操作以下内容：
    1. 传输协议的选择
    2. 控制传输协议的一些参数，例如最大缓冲区大小，报文段segment的最大大小