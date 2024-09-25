springboot将传统的web开发的mvc json tomcat 等框架整合，提供了spring-boot-starter-web组件，简化web应用配置

创建springboot项目勾选的spring web选项后，会自动将spring-boot-starter-web组件加入到项目中

Spring-boot-starter-web启动器主要包括web webmvc json tomcat等基础依赖组件，作用提供web开发常见所需要的所有底层依赖

webmvc为web开发的基础框架，json为JSON数据解析组件，tomcat为自带的容器依赖。

## 控制器@Controller @RestController

​	@Controller	请求页面和数据	通常与Thymeleaf模板引擎结合使用

​	@RestController	只请求数据	会将返回的对象数据转换为JSON格式



## 路由映射

​	**@RequestMapping**注解主要负责URL的路由映射，他可以添加在Controller类或者具体方法上

​	添加在Controller类上，则这个Controller中的所有路由映射都将会加上此映射规则

​	添加在方法上，只对当前方法生效

​	**@RequestMapping**注解包含很多属性参数来定义**HTTP的请求映射规则**。常用的属性为：

​		value：请求URL路径，支持URL模板，正则表达式	@RequestMapping("/user")		@RequestMapping("/getJson/*.json")

-通配符："**"：匹配任意路径 "?"：匹配单个字符 *：匹配任意字符	  	

​		method：HTTP请求方法	GET POST PUT DELETE HTTP支持全部的method	指定前端的请求方式：RequestMethod.GET  RequestMethod.POST  RequestMethod.DELETE  RequestMethod.PUT	@RequestMapping(value="/getData",method = RequestMethod.GET)	Method匹配也可以使用@GetMapping，@PostMapping等注解代替

​		consumes：请求的媒体类型(Content-Type),如application/json

​		produces:响应的媒体类型

​		params，headers：请求的参数及请求头的值

## 参数的传递	

​	**@RequestParam**将请求的参数**绑定到控制器的方法参数**上，接收的参数来自HTTP请求体或请求url的QueryString，当请求的参数名称与Controller的业务方式参数名称一致时，@RequestParam可以省略

​	@RequestParam是必须的

​	`//localhost:8080/hello nickname=zhangsan`&phone = 123

​	`@RequestMapping(value = "/hello",method = RequestMethod.GET)`

​	`public String hello(String nickname,String phone) {`

​		`return nickname` + phone

​	`}`

​	@PathVaraible：用来处理动态的URL，URL的值可以作为控制器中处理方法的参数

​	@RequestBody接收的参数来自requestBody中，即请求体，一般用于处理非Content-Type：application/x-www-form-urlencoded编码格式的数据，比如'application/json','application/xml'等类型的数据



## 静态资源访问

​	classpath:/static/目录

​	application.properties中定义过滤规则和静态资源位置：

​		spring.mvc.static-path-pattern=/static/**

​		spring.web.resources.static-locations=classpath:/static/

​	过滤规则为/static/**,静态资源位置为classpath:/static/

## 文件上传原理

​	表单是enctype属性规定在发送到服务器之前应该如何对表单数据进行编码。

​	当表单的enctype="application/x-www-form-urlencoded"时，form表单中的数据格式为:key=value&key=value

​	当表单的enctype="multipart/form-data"时，其传输数据形式如下

​	![截屏2024-09-25 16.47.50](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 16.47.50.png)

​	

##  Springboot实现文件上传功能

​	Springboot工程嵌入的tomcat限制了请求的文件大小，每个文件的配置最大为1Mb，单次请求的文件总数不能大于10Mb

​	要更改这个默认值需要在配置文件中加入两个配置	

```java
spring.servlet.multipart.max-file-size=10MB

spring.servlet.multipart.max-request-size=10MB
```

​	当表单的enctype="multipart/form-data"时，可以使用**MultipartFile**获取上传的文件数据，再通过transferTo方法将其写入到磁盘中

​	![截屏2024-09-25 17.03.23](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 17.03.23.png)

​	

​	

```java
PostMapping("/upload")
public String up(String nickname, MultipartFile photo, HttpServletRequest request)throws IOException {
    //获取图片的原始名称
    System.out.println(photo.getOriginalFilename());
    //获取文件类型
    System.out.println(photo.getContentType());
    System.out.println(System.getProperty("user.dir"));

    String path = request.getServletContext().getRealPath("/upload/");
    System.out.println(path);
    saveFile(photo,path);
    return "上传成功";

}
```

## 拦截器

​	权限检查：如果登陆检测，进入处理程序检测是否登陆，如果没有，则直接返回登陆界面

​	性能监控：在进入处理程序之前记录开始时间，在处理完后记录结束时间，从而得到该请求的处理时间

​	通用行为：读取cookie得到用户信息并将用户对象放入请求，从而方便后续流程使用，提取Locale Theme，只要是多个处理程序都需要的，即可使用拦截器实现。

​	springboot定义了HandlerInterceptor接口来实现自定义拦截器功能

​	HandlerInterceptor接口定义了**preHandle,postHandle,afterCompletion**三种方法，通过重写这三种方法实现请求前，请求后的操作。

![截屏2024-09-25 21.09.01](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.09.01.png)

### 拦截器定义Interceptor![截屏2024-09-25 21.09.38](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.09.38.png)

### 拦截器注册

addPathPatterns方法定义拦截的地址

excludePathPatterns定义排除某些地址不被拦截

添加的一个拦截器没有addPathPattern任何一个url则默认拦截所有请求

如果没有excludePathPatterns任何一个请求，则默认不放过任何一个请求

![截屏2024-09-25 21.13.52](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.13.52.png)



# Restful服务+Swagger

## RESTful介绍

![截屏2024-09-25 21.46.46](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.46.46.png)

![截屏2024-09-25 21.48.22](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.48.22.png)

![截屏2024-09-25 21.52.49](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.52.49.png)

![截屏2024-09-25 21.54.08](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.54.08.png)

## 构建RESTful应用接口

@GetMapping:处理GET请求，获取资源

@PostMapping:处理POST请求，新增资源

@PutMapping:处理PUT请求，更新资源

@DeleteMapping:删除资源

@PatchMapping:部分更新资源

![截屏2024-09-25 21.59.42](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 21.59.42.png)

```java
@RestController
public class UserController {
  @GetMapping("/user/{id}")
  //动态绑定id，通过PathVariable获取id
  public String 
  getUserById(@PathVariable int id) {
    return "根据id获取用户";
  }
  @PostMapping("/user")
  public String save(User user) {
    return "添加用户";
  }
  @PutMapping("/user")
  public String update(User user) {
    return "更新用户";
  }
  @DeleteMapping("/user/{id}")
  public String deleteById(@PathVariable int id) {
    return "根据id删除用户";
  }
```

## 使用Swagger生成Web API文档

### 什么是Swagger

![截屏2024-09-25 22.18.49](/Users/fulina/Library/Application Support/typora-user-images/截屏2024-09-25 22.18.49.png)

### Swagger依赖

```java
<dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.9.2</version>
</dependency>
<dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>2.9.2</version>
</dependency>
```

### Swagger	config配置类

```

```



​	