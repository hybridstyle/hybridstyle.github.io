---
layout: post
title: "Spring Security 中的ResourceServerConfigurerAdapter怎么使用"
date: 2023-05-09
categories: Java
---
        

Spring Security 中的 `ResourceServerConfigurerAdapter` 用于保护资源服务器中的受保护资源。它提供了一个方便的方式来配置 Spring Security，以便根据需要对访问资源进行授权和认证。

要使用 `ResourceServerConfigurerAdapter`，您需要创建一个继承自它的配置类，并重写其中的一些方法。以下是一个简单的示例：

```java
@Configuration
@EnableResourceServer
public class ResourceServerConfig extends ResourceServerConfigurerAdapter {

    @Override
    public void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/public/**").permitAll()
            .antMatchers("/private/**").authenticated();
    }

    @Override
    public void configure(ResourceServerSecurityConfigurer resources) throws Exception {
        resources.resourceId("resource-id");
    }

    @Bean
    public TokenStore tokenStore() {
        return new InMemoryTokenStore();
    }

    @Override
    public void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/public/**").permitAll()
            .antMatchers("/private/**").authenticated();
    }

    @Override
    public void configure(ResourceServerSecurityConfigurer resources) throws Exception {
        resources.resourceId("resource-id");
    }

    @Bean
    public TokenStore tokenStore() {
        return new InMemoryTokenStore();
    }

    @Override
    public void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/public/**").permitAll()
            .antMatchers("/private/**").authenticated();
    }

    @Override
    public void configure(ResourceServerSecurityConfigurer resources) throws Exception {
        resources.resourceId("resource-id");
    }

    @Bean
    public TokenStore tokenStore() {
        return new InMemoryTokenStore();
    }
}
```

在上面的示例中，我们使用 `@EnableResourceServer` 注解启用了资源服务器功能，并创建了一个名为 `ResourceServerConfig` 的配置类，该类继承了 `ResourceServerConfigurerAdapter`。

在 `configure(HttpSecurity http)` 方法中，我们配置了 HTTP 安全性，限制了 `/private/**` 路径下的资源只能由经过身份验证的用户访问，并且允许所有用户访问 `/public/**` 路径下的资源。

在 `configure(ResourceServerSecurityConfigurer resources)` 方法中，我们指定了资源的 ID，这是一个字符串，用于标识资源服务器。

在 `tokenStore()` 方法中，我们创建了一个 `TokenStore` 实例，用于存储访问令牌。在本例中，我们使用了一个简单的 `InMemoryTokenStore`，但是在实际应用程序中，您可以使用其他的实现。

使用 `ResourceServerConfigurerAdapter`，您可以轻松地配置 Spring Security，以保护您的资源服务器中的受保护资源，并控制对这些资源的访问。您可以根据需要调整和添加配置。