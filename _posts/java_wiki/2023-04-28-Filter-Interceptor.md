---
layout: post
title:  "spring 中 Filter 与Interceptor的区别"
date:   2023-04-26
categories: Java
---


在Spring框架中，Filter和Interceptor都是用于在请求处理过程中执行特定操作的组件，但是它们有以下不同之处：

1. 执行顺序：Filter的执行顺序在Interceptor之前，因为Filter是在Servlet容器级别上执行的，而Interceptor是在Spring MVC框架级别上执行的。

2. 作用范围：Filter作用于Servlet容器层面，可以拦截所有的请求和响应；而Interceptor只能拦截Controller层面的请求和响应，不能拦截静态资源。

3. 配置方式：Filter需要在web.xml中进行配置，而Interceptor需要在Spring的配置文件中进行配置。

4. 功能：Filter可以进行一些比较底层的操作，如字符编码转换、安全控制、日志记录等；而Interceptor可以进行一些高级的功能，如权限控制、登录拦截、性能监控等。

总的来说，Filter和Interceptor都是非常重要的组件，它们可以对请求进行拦截和处理，从而达到一些特定的目的，但是在具体使用时需要根据需求选择合适的组件。