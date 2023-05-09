Spring Security 的WebSecurityConfigurerAdapter 怎么使用


Spring Security 是用于在 Web 应用程序中提供身份验证和授权的框架。`WebSecurityConfigurerAdapter` 是一个用于配置 Spring Security 的适配器类。它提供了一个方便的方式来配置 Spring Security，使其适应不同的 Web 应用程序需求。

要使用 `WebSecurityConfigurerAdapter`，您需要创建一个继承自它的配置类，并重写其中的一些方法。以下是一个简单的示例：

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
 
    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
            .withUser("user").password("{noop}password").roles("USER")
            .and()
            .withUser("admin").password("{noop}password").roles("USER", "ADMIN");
    }
 
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .antMatchers("/**").hasAnyRole("USER", "ADMIN")
            .and().formLogin();
    }
}
```

在上面的示例中，我们使用 `@EnableWebSecurity` 注释启用了 Spring Security，并创建了一个名为 `SecurityConfig` 的配置类，该类继承了 `WebSecurityConfigurerAdapter`。

在 `configureGlobal()` 方法中，我们使用了一个内存身份验证，创建了两个用户：一个名为 `user`，密码为 `password`，拥有 `USER` 角色，另一个名为 `admin`，密码也为 `password`，拥有 `USER` 和 `ADMIN` 两个角色。

在 `configure()` 方法中，我们配置了 HTTP 安全性，限制了 `/admin/**` 路径下的页面只能由 `ADMIN` 角色的用户访问，并且限制了所有其他页面只能由 `USER` 或 `ADMIN` 角色的用户访问。此外，我们还启用了表单登录。

使用 `WebSecurityConfigurerAdapter`，您可以轻松地配置 Spring Security，以满足您的应用程序的安全需求。您可以根据需要调整和添加配置。