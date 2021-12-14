## 1. 什么是 Internet ?
> network of network
- 具体 Internet 的组成角度来理解
- 抽象 互联网提供的 服务
### 具体
- 概念
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