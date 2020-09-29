SpringMvc流程图

流程说明 

第⼀步：⽤户发送请求⾄前端控制器DispatcherServlet 

第⼆步：DispatcherServlet收到请求调⽤HandlerMapping处理器映射器 

第三步：处理器映射器根据请求Url找到具体的Handler（后端控制器），⽣成处理器对象及处理器拦截 

器(如果 有则⽣成)⼀并返回DispatcherServlet 

第四步：DispatcherServlet调⽤HandlerAdapter处理器适配器去调⽤Handler 

第五步：处理器适配器执⾏Handler 

第六步：Handler执⾏完成给处理器适配器返回ModelAndView 

第七步：处理器适配器向前端控制器返回 ModelAndView，ModelAndView 是SpringMVC 框架的⼀个 

底层对 象，包括 Model 和 View 

第⼋步：前端控制器请求视图解析器去进⾏视图解析，根据逻辑视图名来解析真正的视图。 

第九步：视图解析器向前端控制器返回View 

第⼗步：前端控制器进⾏视图渲染，就是将模型数据（在 ModelAndView 对象中）填充到 request 域 

第⼗⼀步：前端控制器向⽤户响应结果



![](https://gitee.com/adc123321/blog_img/raw/master/image/202009/29/123653-327041.jpeg)

