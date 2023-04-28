---
layout: post
title: "Spring向Thymeleaf传递参数的几种方式"
date: 2023-04-28 19:43
categories: Java
---
        
#一、通过 Model 传递

在 Spring Boot 中，你可以通过 Model 对象将参数传递给 Thymeleaf 模板，具体步骤如下：

1. 在控制器方法中添加 Model 参数。

```java
@Controller
public class MyController {

    @GetMapping("/hello")
    public String sayHello(Model model) {
        String message = "Hello, World!";
        model.addAttribute("message", message);
        return "hello";
    }
}
```

2. 在 Thymeleaf 模板中使用 Thymeleaf 表达式获取参数。

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Hello</title>
</head>
<body>
    <h1 th:text="${message}"></h1>
</body>
</html>
```

在上面的代码中，我们使用 Model 对象将参数 message 传递给了 Thymeleaf 模板，然后在模板中使用 Thymeleaf 表达式获取参数，渲染到 HTML 页面中。

需要注意的是，在 Thymeleaf 表达式中，使用 ${} 包裹变量名来获取变量的值。

除了使用 Model 对象传递参数之外，Spring Boot 还提供了其他几种传递参数的方法，具体如下：

#二. 使用 ModelAndView 对象传递参数

```java
@Controller
public class MyController {

    @GetMapping("/hello")
    public ModelAndView sayHello() {
        String message = "Hello, World!";
        ModelAndView mav = new ModelAndView("hello");
        mav.addObject("message", message);
        return mav;
    }
}
```

在控制器方法中，创建 ModelAndView 对象并指定要渲染的视图名称，然后使用 addObject() 方法向 ModelAndView 对象中添加参数。

#三. 直接将参数添加到 ModelMap 对象中

```java
@Controller
public class MyController {

    @GetMapping("/hello")
    public String sayHello(ModelMap modelMap) {
        String message = "Hello, World!";
        modelMap.addAttribute("message", message);
        return "hello";
    }
}
```

在控制器方法中，直接将参数添加到 ModelMap 对象中即可。

需要注意的是，ModelMap 是一个 Model 的子接口，也可以在方法签名中使用 Model 类型的参数代替。

#四. 使用 @ModelAttribute 注解

```java
@Controller
public class MyController {

    @ModelAttribute("message")
    public String message() {
        return "Hello, World!";
    }

    @GetMapping("/hello")
    public String sayHello() {
        return "hello";
    }
}
```

在控制器方法外部，使用 @ModelAttribute 注解定义一个方法，方法的返回值即为要传递的参数，然后在控制器方法中不需要再次添加参数，直接使用 Thymeleaf 表达式获取参数即可。

以上就是 Spring Boot 中常用的传递参数方法，可以根据具体场景选择合适的方法。需要注意的是，在使用 Model、ModelAndView 或 ModelMap 传递参数时，参数的名称和类型要与 Thymeleaf 模板中使用的名称和类型保持一致。

以上就是在 Spring Boot 中向 Thymeleaf 传递参数的基本方法。你可以根据实际需求和业务逻辑，传递不同类型的参数，实现不同的功能。


