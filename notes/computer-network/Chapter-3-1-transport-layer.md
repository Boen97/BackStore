> transport layer providing communication services between application processed running on different hosts.

- the relationship between transport layer and network layer
network layer delivery service between two end systems
transport layer extending delivery service between two application-layer processes running on hosts
- logical communication
transport layer provide logical communication between application processes running on different hosts
- transport layer are implemented in the end systems but not in network routes
- 传输层最重要的功能是构建两个应用程序之间的逻辑链路，所以在network router中，只处理网络层数据包
- transport layer 将 application messages 转化并分割为小段的 transport-layer segament, 并加上 transport layer header 传输层控制头信息

- transport provides logic communication between processes
- network layer provides logic communication between hosts
-  If the network-layer protocol cannot provide delay or bandwidth guarantees for transport- layer segments sent between hosts, then the transport-layer protocol cannot provide delay or bandwidth guarantees for application messages sent between processes.

- transport layer protocols
1. UDP (User Datagram Protocol)
2. TCP (Transmission Control Protocol)

- transport layer packet are called **segament** 分段（将 application message 分段）
- network layer packet are called **datagram** 数据报

- transport multiplexing and demultiplexing
Extending host-to-host delivery to process-to-process delivery is called transport-layer multiplexing and demultiplexing. 
在host-to-host的时候，和网络层数据包多路复用
在process-to-process的时候，demultiplexing

- transport layer 提供的最小服务为：
1. process-to-process data delivery
2. error checking (UDP has error checking feature)


