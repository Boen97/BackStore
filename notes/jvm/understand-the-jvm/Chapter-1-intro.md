JDK
: Java language, JVM, Java library 
: minimal requirements for Java development

JRE
: Java SE API and JVM
: run time environment for Java program.

Java 技术体系划分
1. Java Card
   : 支持 Java 小程序(Applets) 在小内存设备上运行
   
2. Java ME (Micro Edition)
   : 支持 Java 程序在移动终端运行
   : Android 不属于 Java ME
   
3. Java SE (Standard Edition)
   : 支持面向桌面级应用的Java平台
   : 提供了完整的 Java 核心 API
   : 以 java.* 为包名的大多是 Java SE API 的核心包
   : 以 javax.* 大多是 Java EE 的扩展包

4. Java EE (Enterprice Edition)
   : 多层架构的企业应用
   : 在 JDK 10 抛弃，捐献给了 Eclipse 基金会，被称为 Jakarta EE.
   

## Java 发展历史
- Java 1.2
  : J2SE, J2ME, J2EE
  : 第一次内置了 JIT 
  : Classic VM, Hotspot VM, Exact VM

- Hotspot VM
  : 刚发布时作为 JDK1.2 的附加程序
  : JDK1.3 之后默认的 Java 虚拟机

- 2006 年 Sun公司宣布计划要把Java开源
  : 并建立了 OpenJDK 组织对这些源码进行管理
  : OpenJDK几乎拥有了当时SunJDK 7的全部代码

- JDK 11
  : 首先，Oracle从 JDK 11起把以前的商业特性[16]全部开源给OpenJDK，这样OpenJDK 11和OracleJDK 11的代码和功能，在本质上就是完全相同的(官方原文是Essentially Identical)
  : 同时发布两个JDK
    1. GPLv2+CE协议下由Oracle发行的OpenJDK
    2. 新的OTN协议下发行的传统的OracleJDK
    3. OpenJDK 可以免费使用，但是只有半年的更新支持
    4. 后者只有个人可以免费使用

- JDK 12
  : RedHat同时从Oracle手上接过OpenJDK 8和OpenJDK 11的管理权利和维护职责
  : 加入了由RedHat领导开发的Shen-andoah垃圾收集器。
  : 与Oracle在JDK 11中发布的ZGC几乎完全 一致，两者天生就存在竞争。
  : 在OracleJDK 12里把Shenandoah的代码通过条件编 译强行剔除掉
  
## Java 虚拟机家族

1. Sun Classic VM
   : JDK 1.0, 世界上第一款商用 Java 虚拟机
   : 纯解释方式来执行 Java 代码
   : 外挂 JIT compiler
   : 解释器和 JIT 不能配合工作，使用JIT的时候，会对每一行代码进行编译

2. Exact VM (JDK1.2)
   : 具备现代高性能虚拟机雏形，支持热点探测，编译器与解释器混合工作模式
   : Exact memory management 
   : 虚拟机可以知道内存中某个位置的数据是什么类型，可以准确分辨出哪些内存是引用类型，有助于垃圾回收
   : 抛弃了 Classic VM 基于句柄（Handle）的对象查找方式
     - 垃圾收集后，对象可能会被移动位置，需要使用句柄来保持引用值的稳定性
     - 每次定位对象时，减少了一次间接查找的开销，显著提升执行性能
     
3. Hotspot VM
   : 继承了 Classic VM 和 Exact VM 的优点 （如准确式内存管理）
   : Hotspot 热点代码探测技术

4. Mobile/Embedded VM
   : 面向移动和嵌入式市场

5. BEA JRockit/IBM J9 VM
   - JRockit
   : JRockit内部不包含解释器实现，全部代码都靠即时编译器编译后执行
   : 被Oracle收购，现已不再 继续发展
   
   - IBM J9 VM
   : IBM主力发展无疑就是J9
   : IBM J9直至今天仍旧非常活跃，IBM J9虚拟机的职责分离与模块化做得比HotSpot更优秀
   : 由J9 虚拟机中抽象封装出来的核心组件库(包括垃圾收集器、即时编译器、诊断监控子系统等)就单独构 成了IBM OMR项目，可以在其他语言平台如Ruby、Python中快速组装成相应的功能
   : 2016 年开源，捐给了 Eclipse, 重新命名为 Eclipse OMR 和 OpenJ9

6. BEA Liquid VM/Azul VM
   : 与特定硬件平台绑定、软硬件配合工作的专有虚拟机, 能够实现 更高的执行性能
   - Liquid VM
   : Liquid VM也被称为JRockit VE(Virtual Edition，VE)
   : Liquid VM不需要操作系统的支持，或者说它自己本 身实现了一个专用操作系统的必要功能
   : 虚拟机越过通用操作系统直接控制硬件可以获得很多好处
   : 随着JRockit虚拟机终止开发，Liquid VM 项目也已经停止了。
   - Azul VM
   : 在HotSpot基础上进行大量改进，运行于Azul Systems公司的专有硬 件Vega系统上的Java虚拟机
   : 每个Azul VM实例都可以管理至少数十个CPU和数百GB的内存的硬件资源
   : 提供在巨大内存范围内停顿时间可控的垃圾收集器(即业内赫赫有名的**PGC**和**C4收集器**)
   : 2010 发布了 **Zing虚拟机**
   : Azul Systems公司最终也放弃了Vega产品线，把全部精力投入到Zing 和Z ulu产品线中。
   
   - Zing VM
   : 基于 Hotspot, Azul 公司为他编写了新的垃圾收集器
   : 在要求低延迟，快速预热等场景，Zing VM 要比 Hotspot 表现更好
   > Zing 的 PGC, C4 收集器可以轻易支持 TB 级别的Java 堆内存，保证暂停时间不超过10毫秒
   > Hotspot 一直到 JDK11 和 JDK12 的 ZGC 和 Shenandoah 收集器才达到了相同的目标，目前效果远不如 C4
   > Zing 的 Ready Now !功能可以利用之前运行时收集到的性能监控数据，引导虚拟机在启动后快速达到稳定的高性能水平，减少启动后从解释执行到即时编译的等待时间
  
## Java 技术的未来

1. 无语言倾向 - Graal VM
   : Run programs faster anywhere
   : Graal VM被官方称为“Universal VM”和“Polyglot VM”，这是一个在HotSpot虚拟机基础上增强而成 的跨语言全栈虚拟机
   : 可以作为“任何语言”的运行平台使用
   : Graal VM可以无额外开销地混合使用这些编程语言， 支持不同语言中混用对方的接口和对象
   : Graal VM的基本工作原理是将这些语言的源代码(例如JavaScript)或源代码编译后的中间格式 (例如LLVM字节码)通过解释器转换为能被Graal VM接受的中间表示(Intermediate Representation)
   : Graal VM提供了Truffle工具集来快速构建面向一种新语言的解释器，并用它构建了一个称为Sulong的高性能LLVM 字节码解释器。
   : 由于Graal VM 本身能够对输入的中间表示进行自动优化，在运行时还能进行即时编译优化
   : 因此使用Graal VM实现往往能够获得比原生编译器更优秀的执行效率

     
     
