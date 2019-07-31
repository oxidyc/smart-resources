# JWT （JSON Web Tokens）



在 https://jwt.io/ 网站中收录有各类语言的JWT库实现(有关JWT详细介绍请访问 https://jwt.io/introduction/)


按顺序依次是
- Auth0实现 的 com.auth0 / `java-jwt`
    - **`测试用例`**：https://github.com/monkeyk/MyOIDC/blob/1.1.0/myoidc-server/src/test/java/myoidc/server/infrastructure/Auth0JwtTest.java
    - **`点评`**:
    Auth0提供的JWT库简单实用, 依赖第三方(如JAVA运行环境)提供的证书信息(keypair);
    有一问题是在 生成id_token与 校验(verify)id_token时都需要 公钥(public key)与密钥(private key), 个人感觉是一不足(实际上在校验时只需要public key即可)

- Brian Campbell实现的 org.bitbucket.b_c / `jose4j`
   - **`测试用例`**：https://github.com/monkeyk/MyOIDC/blob/1.1.0/myoidc-server/src/test/java/myoidc/server/infrastructure/Jose4JTest.java
   - **`点评`**:
    jose4j提供了完整的JWT实现, 可以不依赖第三方提供的证书信息(keypair, 库本身自带有RSA的实现),类定义与JWT协议规定匹配度高,易理解与上手；
    对称加密与非对称加密都有提供实现

- connect2id实现的 com.nimbusds / `nimbus-jose-jwt`
   - **`测试用例`**：https://github.com/monkeyk/MyOIDC/blob/1.1.0/myoidc-server/src/test/java/myoidc/server/infrastructure/NimbusJoseJwtTest.java
   - **`点评`**:
   nimbus-jose-jwt库类定义清晰,简单易用,易理解 , 依赖第三方提供的证书信息(keypair), 对称算法 与非对称算法皆有实现.

- Les Haziewood实现的 io.jsonwebtoken / `jjwt`
   - **`测试用例`**：https://github.com/monkeyk/MyOIDC/blob/1.1.0/myoidc-server/src/test/java/myoidc/server/infrastructure/JJwtTest.java
   - **`点评`**:
    jjwt小巧够用, 但对JWT的一些细节包装不够, 比如 Claims (只提供获取header,body)

- FusionAuth实现的 io.fusionauth / `fusionauth-jwt`

- Inversoft实现的`prime-jwt`
   - **`测试用例`**：https://github.com/monkeyk/MyOIDC/blob/1.1.0/myoidc-server/src/test/java/myoidc/server/infrastructure/PrimeJwtTest.java
   - **`点评`**:
   prime jwt库怎么说呢, 有些地方不符合JAVA语言规范, 支持对称算法(HMAC) 与非对称算法(RSA), 也算容易理解

- Vertx实现的 io.vertx / `vertx-auth-jwt`
   - **`测试用例`**：https://github.com/monkeyk/MyOIDC/blob/1.1.0/myoidc-server/src/test/java/myoidc/server/infrastructure/VertxAuthJwtTest.java
   - **`点评`**:
    Vertx Auth Jwt 库算是最不容易理解的一个库了.花了不少时间才弄通这一示例. 不容易上手. 并且生成与校验id_token 时都需要公钥与私钥,不足.

以下是在使用中的一些总结或注意点

1. 几乎所有库都要求JAVA版本1.7或更高版本, 1.6或以下的版本需要二次开发(或不支持)
2. 从易用性, 扩展性, 完整性等来看, 使用首先推荐 jose4j, 其次是 Nimbus-jose-jwt.
3. JWT是实现OIDC的基石,掌握其使用对实现OIDC有很大帮助(同时对JAVA证书使用, PKI体系的掌握也有要求)





## Resource 

- [各类JWT库(java)的使用与评价](http://andaily.com/blog/?p=956)