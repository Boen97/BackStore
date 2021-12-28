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