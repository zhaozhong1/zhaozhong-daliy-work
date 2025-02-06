# SpringBoot 启动流程

## **1. 入口方法启动**

- 应用程序的入口通常是一个包含 `main()` 方法的类，且类上通常带有 `@SpringBootApplication` 注解。
- 在 `main()` 方法中，调用 `SpringApplication.run(Application.class, args)` 来启动整个应用。

## **2. 创建 SpringApplication 实例**

- `SpringApplication.run()` 内部会创建一个 `SpringApplication` 实例，这个对象负责整个启动流程的控制。
- 在构造过程中，会自动注册默认的**初始化器（ApplicationContextInitializer）\**和\**监听器（ApplicationListener）**。

## **3. 准备运行环境**

- Spring Boot 会构建**Environment**（包括加载配置文件、命令行参数、系统属性等），并初始化日志系统。
- 同时执行所有注册的环境初始化器，调整环境变量。

## **4. 创建 ApplicationContext** (IoC容器)

- 根据应用类型（Web 应用或普通应用），Spring Boot 会创建合适的 `ApplicationContext` 实现，常见的是 `AnnotationConfigServletWebServerApplicationContext`（Web 应用）或 `AnnotationConfigApplicationContext`（非 Web 应用）。
- 在这一步，Spring Boot 会注册主配置类（通常就是带有 `@SpringBootApplication` 的类）。

## 5. **Bean 的加载和注册**

- 启动过程中会扫描类路径下的组件（包括 `@Component`、`@Configuration`、`@Service` 等注解标识的类），并将它们注册到 ApplicationContext 中。
- 自动配置（Auto-Configuration）模块也在此时生效，通过条件注解（如 `@ConditionalOnClass`、`@ConditionalOnMissingBean` 等）判断并配置相应的 Bean。

## 6. **刷新 ApplicationContext**

- 调用 `refresh()` 方法，完成所有 Bean 的初始化、依赖注入、AOP 代理创建以及事件发布等工作。
- 此时，所有的 Bean 都已初始化并可供使用。

## 7. **启动内嵌服务器（针对 Web 应用）**

- 对于 Web 应用，Spring Boot 会启动内嵌的 Servlet 容器（如 Tomcat、Jetty 或 Undertow），并将 Spring 的 DispatcherServlet 注册到容器中，完成 web 环境的启动。

## 8. **运行 CommandLineRunner 和 ApplicationRunner**

- 如果在上下文中定义了 `CommandLineRunner` 或 `ApplicationRunner` 接口的 Bean，在 ApplicationContext 刷新后，这些组件会被调用，从而执行一些初始化任务或启动业务逻辑。

## 9. **应用正式启动**

- 至此，Spring Boot 应用完成启动过程，处于运行状态，等待接收请求或执行后台任务。