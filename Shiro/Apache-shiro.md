# Apache Shiro

## Introduce
` Apache Shiro™` is a powerful and easy-to-use Java security framework that performs `authentication`, `authorization`, `cryptography`, and `session management`. With Shiro’s easy-to-understand API, you can quickly and easily secure any application – from the smallest mobile applications to the largest web and enterprise applications. 

Home：http://shiro.apache.org


## Detailed Architecture
- `Subject` (org.apache.shiro.subject.Subject):主体，当前用户
- `SecurityManager`（org.apache.shiro.mgt.SecurityManager）：安全管理器
- `Authenticator`（org.apache.shiro.authc.Authenticator）：用户认证管理器
  - `Authentication Strategy`（org.apache.shiro.authc.pam.AuthenticationStrategy）：用户认证策略
- `Authorizer`（org.apache.shiro.authz.Authorizer）：权限管理器
- `SessionManager`（org.apache.shiro.session.mgt.SessionManager）：会话管理器
  - `SessionDAO`（org.apache.shiro.session.mgt.eis.SessionDAO）：
- `CacheManager`（org.apache.shiro.cache.CacheManager）：缓存控制器
- `Cryptography`（org.apache.shiro.crypto.*）：加密技术
- `Realms`（org.apache.shiro.realm.Realm）：域

### Shiro的内置FilterChain
| 过滤器简称 | 含义 | Class |
|:----:|:---- |:----|
| `anon` | 无参，开放权限，未认证可以访问，可以理解为匿名用户或游客 | org.apache.shiro.web.filter.authc.AnonymousFilter |
| `authc` | 无参，认证后可以访问 | org.apache.shiro.web.filter.authc.FormAuthenticationFilter |
| `authcBasic` | 无参，httpBasic认证 | org.apache.shiro.web.filter.authc.BasicHttpAuthenticationFilter |
| `logout` | 无参，注销，执行后会直接跳转到shiroFilterFactoryBean.setLoginUrl();设置的url | org.apache.shiro.web.filter.authc.LogoutFilter |
| `noSessionCreation` | | org.apache.shiro.web.filter.session.NoSessionCreationFilter|
| `perms` | 需要特定权限才能访问 | org.apache.shiro.web.filter.authz.PermissionsAuthorizationFilter |
| `port` | 需要特定端口才能访问(不常用) | org.apache.shiro.web.filter.authz.PortFilter |
| `rest` | 根据指定HTTP请求才能访问（不常用） | org.apache.shiro.web.filter.authz.HttpMethodPermissionFilter |
| `roles` | 需要特定角色才能访问 | org.apache.shiro.web.filter.authz.RolesAuthorizationFilter |
| `ssl` | 无参，安全的URL请求，协议为HTTPS  | org.apache.shiro.web.filter.authz.SslFilter |
| `user` | 无参，必须存在永固，当登入操作时不做检查，需要特定用户才能访问 | org.apache.shiro.web.filter.authc.UserFilter |

## 权限控制
### URL级别粗粒度权限控制
- 配置`web.xml`的`shiroFilter`拦截 `/*`
- 在spring的`applicationContext-shiro.xml`配置文件中配置同名bean，配置`filterChainDefinitions`拦截控制规则
```
xxx.html* = anon
xxx.html* = authc
xxx.html* = perm[权限]
xxx.html* = roles[角色]
```

### 方法级别细粒度权限控制
- 基于URL粗粒度之上配置
- 在spring的`applicationContext-shiro.xml`配置 spring AOP 对spring管理bean对象开启`shiro注解`支持
```java
@RequiresPermissions(权限)
@RequiresRoles(角色)
@RequiresAuthentication
@RequiresUser
@RequiresGuest
```

### 通过shiro自定义标签，实现页面元素显示控制
```jsp
<%@taglib uri="http://shiro.apache.org/tags" prefix="shiro"%>

<shiro:authenticated>
<shiro:notAuthenticated>
<shiro:guest>
<shiro:user>
<shiro:hasAnyRoles name="abc,123">
<shiro:hasRole name="abc">
<shiro:lacksRole name="abc">
<shiro:hasPermission name="abc">
<shiro:lacksPermission name="abc">
<shiro:principal>
```
