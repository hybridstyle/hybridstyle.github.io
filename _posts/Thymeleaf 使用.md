Thymeleaf 介绍

Thymeleaf是一种流行的Java模板引擎，用于将动态数据与HTML，XML，JavaScript，CSS等静态页面相结合。它旨在创建高度可维护的模板，同时具有非常清晰的语法，易于使用并且具有广泛的功能。

以下是Thymeleaf的一些主要特点：

- 与Spring框架集成：Thymeleaf与Spring框架完美集成，可以轻松地将模型数据绑定到模板上。

- 语法简单明了：Thymeleaf模板语法易于学习，与HTML模板类似，使开发人员能够快速构建动态Web应用程序。

- 支持多种模板类型：Thymeleaf支持多种模板类型，包括HTML，XML，文本，JavaScript和CSS。

- 支持模板片段：Thymeleaf支持模板片段，可以重复使用和组合多个片段来创建复杂的页面。

- 安全的输出：Thymeleaf支持安全的输出，可防止XSS攻击。

- 可扩展性：Thymeleaf支持各种插件，可以轻松地扩展其功能。

总之，Thymeleaf是一种功能强大的模板引擎，可用于构建高度可维护的动态Web应用程序。

##SpringBoot 整合 Thymeleaf
在Spring Boot中整合Thymeleaf非常简单。Spring Boot自带了Thymeleaf的依赖，只需要在Maven或Gradle中添加Thymeleaf的starter依赖即可开始使用Thymeleaf。

下面是使用Spring Boot和Thymeleaf开发Web应用程序的基本步骤：

1. 在pom.xml中添加Thymeleaf starter依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

2. 创建Thymeleaf模板文件：在src/main/resources/templates目录下创建一个HTML文件，文件名以“.html”结尾。在模板文件中可以使用Thymeleaf语法来绑定数据到模板上。

3. 创建控制器类：创建一个Spring Boot控制器类，使用@RequestMapping注解来处理请求并返回模板文件名称。

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String index(Model model) {
        model.addAttribute("message", "Hello Thymeleaf!");
        return "index";
    }
}
```

4. 在模板文件中使用Thymeleaf语法：在模板文件中使用Thymeleaf语法来绑定数据到模板上。

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Thymeleaf Example</title>
</head>
<body>
    <h1 th:text="${message}"></h1>
</body>
</html>
```

5. 运行应用程序：使用Spring Boot的内置Tomcat服务器运行应用程序。
