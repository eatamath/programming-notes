# SpringMVC Notes



### 入门

配置DispatcherServlet

* 在 web.xml `<servlet>` 与 `servlet mapping` 中 配置 DispatherServlet
* 请求拦截，/ 所有除 jsp,/* all,*.do 配置在 `urll-pattern` 中

配置HandlerMapping

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191115200813937.png" alt="image-20191115200813937" style="zoom:50%;" />

* WEB-INFO/[servletname]-servler.xml 用来初始化 springMVC 对象