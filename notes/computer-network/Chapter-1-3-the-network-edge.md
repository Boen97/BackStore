- Host或者终端系统位于互联网的 edge，经过互联网这个大黑盒子与其他终端进行交流

- 终端系统又被称为 Host 的原因在于，终端系统上运行着应用

- access network

  > 将终端系统物理地连接到第一个路由器（也称为 edge router）的网络

- how homes connect to the Internet

  - 最常见的两种家庭接入互联网的方式

    1. DSL（Digital Subscriber line) 数字用户线,传统中的电话线路

      - DSL modem 调制解调器，也就是我们俗称的 “猫”

        > 将数字信号转化为高频音调，通过电话线将信号线传出去

      - DSLAM（digital subscriber line access multiplexer）数字用户线接入复用器

        > 位于电信公司的CO（central office）负责将高频数据还原为数字信号

      - 电话线同时传输数据和传统的电话信号，分布在不同的频率上（多路复用）

        - 高度下行通道 在 50kHz 到 1MHz
        - 中速上行通道 在 4kHz 到 50kHz
        - 普通的电话双向通道在 0 到 4kHz

        > 也正是因为网络信号需要在高频率进行传输，这才需要 DSL modem，负责将数字信号转化为高频段信号

      - Splitter 分配器 负责将电话信号和网络数据分开，电话信号转发到电话，网络信号转发到 DSL modem

      - DSL transimission rates

        1. 下行通常为 24Mbps 和 52Mbps
        2. 上行通常为 3.5Mbps 和 16Mbps
        2. 2014年最新标准为 上行 + 下行 总速率为 1Gbps

        > 因此 DSL 这种方式是非对称的 （asymmetric）

      - 影响实际 DSL 速率的因素有

        1. tiered service 电信公司的分层服务，不同价格不同速率
        2. 双绞线的规格
        3. 实际地址到 CO 之间的距离
        4. 电干扰程度

      - DSL 主要适用于 5到10英里的短距离互联网接入 1英里大概为 1.6km

    2. Cable 有线电视

      > 利用了电线电视公司现有的基础设施

      - HFC （hybrid fiber coax）混合光纤同轴网络

        > 在一个系统中同时使用光纤和同轴电缆

      - cable head end 电缆头终端到社区连接处使用光纤链路，社区连接处（fiber node 光纤节点）到家采用同轴电缆

      - cable modem 和 DSL modem 类似

      - cable modem termination system 和 DSLAM 类似

      - cable modem 将 HFC 网络 分为 上下游通道 **downstream channel and upstream channel**
        和 DSL 一样，访问也是 非对称的

      - 下游通道速率通常为 40Mbps 到 1.2Gbps，上游通道通常为 30Mbps 到 100Mbps

      - **cable internet access is a shared broad-cast medium** 共享广播媒介

        > 上下游通道是共用的

          - 当多个用户在同时在下游通道下载东西时，分配到每个人的实际速率将会显著降低



