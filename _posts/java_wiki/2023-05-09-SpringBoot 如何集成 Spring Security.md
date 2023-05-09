---
layout: post
title: "SpringBoot 如何集成 Spring Security"
date: 2023-05-09
categories: Java
---
        Spring Boot 集成 Spring Security 的步骤如下：

1. 添加 Spring Security 依赖：在 Maven 或 Gradle 项目中，需要添加 Spring Security 的依赖，例如：

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-security</artifactId>
   </dependency>
   ```

2. 配置安全性：在 Spring Boot 应用程序中，可以使用 Java Config 或者 XML 配置来配置 Spring Security。通常情况下，我们可以创建一个继承自 `WebSecurityConfigurerAdapter` 类的配置类，通过覆盖 `configure(HttpSecurity http)` 方法来配置安全性，例如：

   ```java
   @Configuration
   @EnableWebSecurity
   public class SecurityConfig extends WebSecurityConfigurerAdapter {

       @Override
       protected void configure(HttpSecurity http) throws Exception {
           http
               .authorizeRequests()
                   .antMatchers("/public/**").permitAll()
                   .anyRequest().authenticated()
                   .and()
               .formLogin()
                   .loginPage("/login")
                   .defaultSuccessUrl("/")
                   .permitAll()
                   .and()
               .logout()
                   .logoutUrl("/logout")
                   .permitAll();
       }

       // 配置用户信息
       @Override
       protected void configure(AuthenticationManagerBuilder auth) throws Exception {
           auth.inMemoryAuthentication()
               .withUser("user")
               .password("{noop}password")
               .roles("USER");
       }
   }
   ```

   上述配置示例中，我们定义了一个 `SecurityConfig` 配置类，通过 `@EnableWebSecurity` 注解启用 Spring Security。在 `configure(HttpSecurity http)` 方法中，我们定义了请求授权规则和登录/注销页面等配置，还定义了一个 `configure(AuthenticationManagerBuilder auth)` 方法来配置用户信息。

   注意，上述示例中使用了 `inMemoryAuthentication` 方法将用户信息存储在内存中，实际生产环境中应该使用其他方式存储用户信息，例如数据库或 LDAP 等。

3. 启用 CSRF 防御（可选）：Spring Security 默认启用 CSRF 防御机制，以保护应用程序免受 CSRF 攻击。在 Spring Boot 应用程序中，可以通过设置 `security.enable-csrf=true` 来启用 CSRF 防御，例如：

   ```properties
   security.enable-csrf=true
   ```

4. 配置登录页面（可选）：在 Spring Boot 应用程序中，默认情况下，Spring Security 会生成一个基本的登录页面，我们可以通过设置 `spring.security.form-login.login-page` 和 `spring.security.form-login.login-processing-url` 来自定义登录页面和登录请求的 URL，例如：

   ```properties
   spring.security.form-login.login-page=/my-login-page
   spring.security.form-login.login-processing-url=/my-login
   ```

完成以上步骤后，我们就可以在 Spring Boot 应用程序中集成 Spring Security，并配置身份验证和授权功能。