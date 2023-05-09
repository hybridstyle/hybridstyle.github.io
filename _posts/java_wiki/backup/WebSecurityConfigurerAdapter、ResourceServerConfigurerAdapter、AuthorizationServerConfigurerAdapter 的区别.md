WebSecurityConfigurerAdapter、ResourceServerConfigurerAdapter、AuthorizationServerConfigurerAdapter 的区别


`WebSecurityConfigurerAdapter`、`ResourceServerConfigurerAdapter` 和 `AuthorizationServerConfigurerAdapter` 都是 Spring Security 中用于配置安全性的适配器类，但是它们的主要目的和使用方式略有不同。

`WebSecurityConfigurerAdapter` 用于配置 Web 安全性，包括身份验证和授权，以及如何保护 Web 应用程序的特定部分。它提供了一组方法，可以通过覆盖这些方法来配置安全性功能，例如：

- `configure(HttpSecurity http)`：用于配置请求授权规则、认证方式、登录页面等；
- `configure(AuthenticationManagerBuilder auth)`：用于配置身份验证机制、用户信息来源等；

`ResourceServerConfigurerAdapter` 用于配置 OAuth2 资源服务器，包括如何验证令牌、授权范围和保护资源。它提供了一组方法，可以通过覆盖这些方法来配置资源服务器的功能，例如：

- `configure(HttpSecurity http)`：用于配置请求授权规则、认证方式、访问令牌等；
- `configure(ResourceServerSecurityConfigurer resources)`：用于配置资源服务器安全属性、令牌解析等；

`AuthorizationServerConfigurerAdapter` 用于配置 OAuth2 授权服务器，包括如何颁发和验证令牌、客户端详细信息和授权类型等。它提供了一组方法，可以通过覆盖这些方法来配置授权服务器的功能，例如：

- `configure(ClientDetailsServiceConfigurer clients)`：用于配置客户端详细信息、授权类型、授权范围等；
- `configure(AuthorizationServerEndpointsConfigurer endpoints)`：用于配置授权服务器的端点，包括身份验证管理器、用户详细信息服务和令牌存储。

综上所述，这三个适配器类的主要目的是配置 Spring Security 在不同场景下的安全性。它们分别用于配置 Web 安全性、OAuth2 资源服务器和授权服务器。根据您的具体需求，可以选择使用其中的一个或多个适配器类来配置 Spring Security。