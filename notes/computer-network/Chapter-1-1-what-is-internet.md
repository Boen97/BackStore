## 1. 什么是 Internet ?
> network of network
- 具体 Internet 的组成角度来理解
- 抽象 互联网提供的 服务
### 具体
  - **Host/End System**
  - End System are connected together by a network of **communication links** and **package switches**
    - communication links
      - coaxial cable 同轴电缆
      - copper wire 双绞线
      - optical fiber 光纤
      - radio spectrum 无线频谱
  - transmission rate (bits/second)
  - packets

    > resulting packages of information

  - package switch

    > 将 package 从 incomming links 转发到 outgoing links

    - package switch 主要分为 **routers** 和 **link-layer switches**
      - link-layer switches 主要用于**接入网络** (network edge)
      - routers 主要用于 **network core**

  - route or path

    > packet 到达目的地所经过的 links 和 package switches

  - packet-switched networks 就像现实生活中的交通网络

    > 假设从一个仓库搬运一堆货物到另一个仓库, 这堆货物将被拆成很多小的包裹来运送
    >
    > 装载着拆分后的货物的卡车就类似 packet, 仓库类似终端，十字路口类似 packet switches

  - ISP (Internet Service Provider)

    > ISP 为终端系统提供互联网服务，常见的 ISP 例如电信和移动（住宅ISP）
    >
    > 每个 ISP 是一个 packet-switched networks

  - ISP 为用户了提供了多种接入互联网的方式

    1. 住宅宽带接入（cable modem 有线调制解调器 or DSL）
    2. 高速局域网接入
    3. 手机无线接入

  - 互联网就是把终端系统连接起来，因此ISP之间也必须互相连接

    > 低级的ISP通过高级的ISP（国内或者国际的ISP）互相连接，高级的ISP之间互相连接
    >
    > 高级的ISP由高速路由器和高速光纤链路组成

  - 每个ISP都是独立管理的，运行 IP 协议，并且遵循特定的命名和地址规范

  - **Protocol**

  > 协议将整个互联网的各个部分有序得组织在一起
  >
  > 互联网的主要协议统称为 TCP/IP, TCP(transimission control protocol)

  - **Internet standards**

  > 协议必须有一套标准，才能让不同的人参与进来

    - 互联网标准由IETF制定（Internet Enginnering Task Force）
    - RFCs(request for comments) 征求意见，IETF的标准文档
    - 其他机构也参与制定了标准
    - The IEEE 802 LAN Standards Committee [IEEE 802 2020] 制定了 **the Ethernet and wireless WiFi standards.**

### 作为一项服务

> 作为一项基础设施，为应用提供**服务**

  - 分布式应用，在多个终端间交换传输数据
  - **网络应用运行在终端，而不是在互联网的中心**
  - package switches 负责在多个终端间传输数据，但是他们并不关心应用本身，因此分组交换机是一项隐形的基础设施
  - socket interface

    > socket interface 指定了终端系统之间如何利用网络基础设施来传递数据
    >
    > socket interface 制定了一套发送终端必须遵守的规则，就像邮寄一封信到另一个地方，需要遵守邮局制定的规则,
    > 类似于 post service interface

    - 和邮局提供多种服务一样，互联网这个邮局系统也需要提供多种服务，在开发应用程序的时候，你需要选择一项你所要使用的服务
