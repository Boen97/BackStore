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
  

