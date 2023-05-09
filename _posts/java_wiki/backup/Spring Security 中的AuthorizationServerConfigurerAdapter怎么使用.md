Spring Security 中的AuthorizationServerConfigurerAdapter怎么使用


Spring Security 中的 `AuthorizationServerConfigurerAdapter` 用于配置 OAuth2 授权服务器。它提供了一种简单的方式来配置授权服务器以及客户端详细信息、令牌端点、令牌存储等等。

要使用 `AuthorizationServerConfigurerAdapter`，您需要创建一个继承自它的配置类，并重写其中的一些方法。以下是一个简单的示例：

```java
@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Autowired
    private UserDetailsService userDetailsService;

    @Autowired
    private TokenStore tokenStore;

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
        clients.inMemory()
            .withClient("client-id")
            .secret("client-secret")
            .authorizedGrantTypes("password", "refresh_token")
            .scopes("read", "write")
            .accessTokenValiditySeconds(600)
            .refreshTokenValiditySeconds(3600);
    }

    @Override
    public void configure(AuthorizationServerEndpointsConfigurer endpoints) throws Exception {
        endpoints.authenticationManager(authenticationManager)
            .userDetailsService(userDetailsService)
            .tokenStore(tokenStore);
    }
}
```

在上面的示例中，我们使用 `@EnableAuthorizationServer` 注解启用了授权服务器功能，并创建了一个名为 `AuthorizationServerConfig` 的配置类，该类继承了 `AuthorizationServerConfigurerAdapter`。

在 `configure(ClientDetailsServiceConfigurer clients)` 方法中，我们配置了客户端详细信息，包括客户端 ID、客户端密码、授权类型、授权范围以及访问令牌和刷新令牌的有效期。

在 `configure(AuthorizationServerEndpointsConfigurer endpoints)` 方法中，我们配置了授权服务器的端点，包括身份验证管理器、用户详细信息服务和令牌存储。

注意，上面的示例中注入了 `AuthenticationManager`、`UserDetailsService` 和 `TokenStore` 实例。这些都需要在您的应用程序中进行配置，并且可以根据您的需求进行调整。

使用 `AuthorizationServerConfigurerAdapter`，您可以轻松地配置 Spring Security 授权服务器，并控制授权类型、客户端详细信息和令牌有效期等参数。您可以根据需要调整和添加配置。