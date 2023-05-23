RequestContextHolder 怎么使用

`RequestContextHolder` 是 Spring 提供的一个类，用于保存当前请求（Request）相关的信息，例如 `HttpServletRequest` 和 `HttpServletResponse`。

下面是如何使用 `RequestContextHolder` 来获取 `HttpServletRequest` 和 `HttpServletResponse` 的例子：

```java
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.context.request.RequestContextHolder;
import org.springframework.web.context.request.ServletRequestAttributes;

public class SomeService {

    public void someMethod() {
        ServletRequestAttributes servletRequestAttributes =
                (ServletRequestAttributes) RequestContextHolder.currentRequestAttributes();

        HttpServletRequest request = servletRequestAttributes.getRequest();
        HttpServletResponse response = servletRequestAttributes.getResponse();

        // 现在你可以使用 request 和 response 对象了
    }
}
```

在这个例子中，我们首先通过 `RequestContextHolder.currentRequestAttributes()` 方法获取到 `ServletRequestAttributes` 对象。然后，我们就可以通过 `ServletRequestAttributes.getRequest()` 和 `ServletRequestAttributes.getResponse()` 方法来获取 `HttpServletRequest` 和 `HttpServletResponse` 对象了。

注意，这种方式只能在处理 HTTP 请求的线程中使用，也就是说，只能在 Controller、Service、Repository 这些 Bean 中使用，不能在新启动的线程或者定时任务中使用。这是因为 `RequestContextHolder` 内部使用了 `ThreadLocal` 来存储信息，每个新的线程都会有自己的 `ThreadLocal` 变量。如果你在新的线程或定时任务中使用 `RequestContextHolder`，可能会得到 null。