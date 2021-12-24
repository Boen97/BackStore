- IoC(Inversion of Control) container (Spring框架最核心的功能)
- AOP(Aspect-Oriented Programming) 面向切面编程
  - Spring 有自己的AOP,也可以和 AspectJ 整合

## The IoC Container

- IoC is also known as DI(dependency injection)
- `org.springframework.bean` 和 `org.springframework.context` 两个包是实现IoC的基础
- `BeanFactory Interface`
  - the root interface for accessing a spring bean container
  - basic client view of a bean container
- ApplicationContext
  - central interface to provide configuration for an application
    为应用程序提供配置的中央接口
- BeanFactroy 提供了配置的框架和基础功能
- ApplicationContext 添加了许多特定于企业的功能
- **beans**
  - objects managed by Spring IoC container