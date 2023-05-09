SpringBoot 配置 Spring Security 从数据库读取用户信息

从数据库中读取用户信息并进行身份验证和授权，可以通过以下步骤实现：

1. 在数据库中创建一个用户表，并插入一些用户数据，例如：

   ```sql
   CREATE TABLE `user` (
     `id` int(11) NOT NULL AUTO_INCREMENT,
     `username` varchar(50) NOT NULL,
     `password` varchar(100) NOT NULL,
     `enabled` tinyint(1) NOT NULL,
     PRIMARY KEY (`id`)
   ) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4;

   INSERT INTO `user` (`id`, `username`, `password`, `enabled`)
   VALUES
       (1, 'user', '$2a$10$gsGsq13aAUBHwL1FlvGkSe0l10.UdqVy1FrlQh8jvD9tQ/EYtDByS', 1);
   ```

   上述示例中，我们创建了一个名为 `user` 的表，其中包含 `id`、`username`、`password` 和 `enabled` 四个字段。我们插入了一个用户数据，用户名为 `user`，密码为 `password`（使用 BCrypt 加密），并将 `enabled` 设置为 1，表示该用户已启用。

2. 创建一个实现了 `UserDetailsService` 接口的类，用于从数据库中读取用户信息，例如：

   ```java
   @Service
   public class UserDetailsServiceImpl implements UserDetailsService {

       @Autowired
       private UserRepository userRepository;

       @Override
       public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
           User user = userRepository.findByUsername(username);
           if (user == null) {
               throw new UsernameNotFoundException("User not found");
           }
           return new org.springframework.security.core.userdetails.User(user.getUsername(), user.getPassword(), user.isEnabled(), true, true, true, getAuthorities(user.getRoles()));
       }

       private Collection<? extends GrantedAuthority> getAuthorities(Collection<Role> roles) {
           return roles.stream()
               .flatMap(role -> role.getPermissions().stream())
               .map(permission -> new SimpleGrantedAuthority(permission.getName()))
               .collect(Collectors.toList());
       }
   }
   ```

   在上述示例中，我们定义了一个 `UserDetailsServiceImpl` 类，实现了 `UserDetailsService` 接口。在 `loadUserByUsername` 方法中，我们从数据库中查询用户信息，并创建一个 `UserDetails` 对象来表示用户信息。在上述示例中，我们还使用了 `getAuthorities` 方法来获取用户的权限信息，并将其包装成 `GrantedAuthority` 对象。

   注意，上述示例中使用了一个名为 `UserRepository` 的类，用于从数据库中查询用户信息。这里的 `UserRepository` 类可以使用 Spring Data JPA 来实现，例如：

   ```java
   @Repository
   public interface UserRepository extends JpaRepository<User, Long> {
       User findByUsername(String username);
   }
   ```

   上述示例中，我们定义了一个 `UserRepository` 接口，继承自 `JpaRepository` 类，并定义了一个 `findByUsername` 方法来查询指定用户名的用户信息。

3. 在 `WebSecurityConfigurerAdapter` 类中配置 `UserDetailsService`，例如：

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/login").permitAll()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .loginPage("/custom-login")  // 自定义登录页面的 URL
                .loginProcessingUrl("/login") // 处理登录表单提交的 URL，与模板中指定的一致
                .defaultSuccessUrl("/home")
                .failureUrl("/custom-login?error=true")
                .permitAll()
                .and()
            .logout()
                .logoutUrl("/logout")
                .logoutSuccessUrl("/login")
                .permitAll();
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(passwordEncoder());
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

在上述示例中，我们通过 `@Autowired` 注解将之前定义的 `UserDetailsService` 类注入到了 `SecurityConfig` 类中。在 `configure` 方法中，我们定义了应用程序的安全配置，包括：

- 对所有请求进行身份验证，除了 `/login` 请求；
- 使用表单登录，并指定登录页面、默认成功页面和失败页面；
- 允许注销，并指定注销 URL 和成功注销后的页面。

在 `configure(AuthenticationManagerBuilder auth)` 方法中，我们将之前定义的 `UserDetailsService` 类设置为认证管理器的 `userDetailsService` 属性，并使用 `BCryptPasswordEncoder` 作为密码编码器。

需要注意的是，以上示例仅供参考，具体实现可能因应用场景的不同而有所差异。例如，有些应用程序可能需要同时使用多种身份验证方式，此时可能需要使用多个 `WebSecurityConfigurerAdapter` 类来分别配置各种身份验证方式。
