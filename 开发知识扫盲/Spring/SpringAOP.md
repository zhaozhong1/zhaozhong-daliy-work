# SpringAOP

## 什么是AOP

AOP是通过动态代理实现的，面向切面编程。这个编程范式能够将业务无关，但被业务所共同调用的逻辑封装起来，通过通知来织入切入点形成切面。

### SpringAOP 实现

通过`JDK Proxy` 和 `CGLib`实现：

- JDK Proxy：

  - 对实现接口的类代理。需要手动启用。

- CGLib

  - 默认方式，生成目标类的子类。换言之，CGLib不能代理那些声明final的类。

  

