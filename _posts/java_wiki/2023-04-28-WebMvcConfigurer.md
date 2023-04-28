---
layout: post
title:  "WebMvcConfigurer是干什么用的"
date:   2023-04-28
categories: Java
---

WebMvcConfigurer是Spring MVC提供的一个接口，它可以用于配置和定制Spring MVC的一些行为和特性。

具体来说，WebMvcConfigurer接口提供了一系列回调方法，可以在Spring MVC的初始化过程中对框架的一些配置进行修改，包括：

1. 配置视图解析器(ViewResolver)：可以配置多个视图解析器，包括JSP、Thymeleaf、FreeMarker等。

2. 配置静态资源的处理：可以配置Spring MVC如何处理静态资源，如CSS、JS、图片等。

3. 配置拦截器(Interceptor)：可以配置拦截器来实现一些通用的逻辑，如日志记录、权限控制、跨域等。

4. 配置消息转换器(MessageConverter)：可以配置Spring MVC如何处理请求和响应中的消息内容，如JSON、XML、文本等。

5. 配置跨域(Cors)：可以配置Spring MVC如何处理跨域请求，包括允许哪些域名访问、允许哪些HTTP方法等。

除了上述功能外，WebMvcConfigurer还提供了其他一些回调方法，可以实现更加细粒度的定制和配置。

需要注意的是，WebMvcConfigurer是一个接口，我们需要编写实现该接口的类，并在Spring MVC配置文件中进行配置，才能使其生效。


### WebMvcConfigurer可以配置拦截静态资源吗

WebMvcConfigurer可以配置拦截器(Interceptor)，但是默认情况下它不会拦截静态资源。

静态资源的处理是由DefaultServletHandlerConfigurer或者WebMvcAutoConfiguration类中的静态资源处理器来处理的，因此，如果我们需要拦截静态资源，就需要在WebMvcConfigurer中配置静态资源的处理方式。

具体来说，可以通过WebMvcConfigurer中的addResourceHandlers方法来配置静态资源的处理方式，例如：

```java
@Configuration
@EnableWebMvc
public class MyWebMvcConfigurer implements WebMvcConfigurer {
 
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/static/**").addResourceLocations("classpath:/static/");
    }

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new MyInterceptor()).addPathPatterns("/**");
    }
}
```

在上述例子中，我们通过addResourceHandlers方法来添加一个静态资源处理器，它将处理以“/static/”开头的所有请求，并将请求映射到“classpath:/static/”目录下的文件。同时，我们也添加了一个自定义的拦截器(MyInterceptor)，它将拦截所有的请求。

需要注意的是，配置静态资源的处理方式可能会影响性能，因此在实际开发中应该根据具体情况进行配置。
