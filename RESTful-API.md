# RESTful API

## Introduce
REST 全称是`Re`presentational `S`tate `T`ransfer，即：资源在网络中以某种形式进行状态转移，中文是：表述性状态转移。REST最早是由Roy Fielding博士发表的论文中提到的，他也曾参与设计了HTTP协议。论文地址：http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm

## 特征与优点
1. **`客户端-服务器（Client-Server）`**：提供服务的服务器和使用服务的客户端分离解耦；

   优点：
   - 提高客户端的便捷性（操作简单）
   - 简化服务器提高可伸缩性（高性能、低成本）
   - 允许客户端服务端分组优化，彼此不受影响

2. **`无状态（Stateless）`**：来自客户的每一个请求必须包含服务器处理该请求所需的所有信息（请求信息唯一性）；

   优点：
   - 提高可见性（可以单独考虑每个请求）
   - 提高可靠性（更容易故障恢复）
   - 提高了可扩展性（降低了服务器资源使用）

3. **`可缓存（Cachable）`**：服务器必须让客户端知道请求是否可以被缓存？如果可以，客户端可以重用之前的请求信息发送请求；

   优点：
   - 减少交互连接数
   - 减少连接过程的网络时延

4. **`分层系统（Layered System）`**：允许服务器和客户端之间的中间层（代理，网关等）代替服务器对客户端的请求进行回应，而客户端不需要关心与它交互的组件之外的事情；

   优点：
   - 提高了系统的可扩展性
   - 简化了系统的复杂性

5. **`统一接口（Uniform Interface）`**：客户和服务器之间通信的方法必须是统一化的。（例如：GET,POST,PUT.DELETE）

   优点：
   - 提高交互的可见性
   - 鼓励单独优化改善组件

6. **`支持按需代码（Code-On-Demand，可选）`**：服务器可以提供一些代码或者脚本并在客户的运行环境中执行。

   优点：提高可扩展性

## 概要设计方法
1. `协议`。API与用户的通信协议，总是使用`HTTPS`协议
2. `域名`。应该尽量将API部署在专用域名之下。如果确定API很简单，不会有进一步扩展，可以考虑放在主域名下
```js
https://api.example.com
https://examole.com/api/
```
3. `版本（Versioning）`。应该将API的版本号放入URL。另一种做法是，将版本号放在HTTP头信息中，但不如放在URL方便和直观。
```js
https://api.example.com/v1/
```
4. `路径（Endpoint）`。表示API的具体网址。

    在RESTful架构中，每个网址代表一种资源（rescource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的集合（collection），所以API中的名词也应该使用复数。
    >注意：根据RFC3986定义，URL是大小写敏感的，所以为了避免歧义，尽量使用小写字母
5. `方法（Method）即 HTTP动词`。对资源的具体操作类型，由HTTP动词表示。常见的HTTP动词有下面五个（括号里是对应的SQL命令）
```css
GET（SELECT）：从服务器取出资源（一项或多项）。
POST（CREATE）：在服务器新建一个资源。
PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
DELETE（DELETE）：从服务器删除资源。
HEAD：获取资源的元数据。（不常用）
OPTIONS：获取信息，关于资源的哪些属性是客户端可以改变的。（不常用）
```
下面是一些例子。
```css
GET /zoos：列出所有动物园
POST /zoos：新建一个动物园
GET /zoos/ID：获取某个指定动物园的信息
PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
DELETE /zoos/ID：删除某个动物园
GET /zoos/ID/animals：列出某个指定动物园的所有动物
DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物
```
----
下表汇总了电子商务示例的大多数RESTful实现所采用的常见约定：
| Resource           | POST | GET | PUT | DELETE |
|--------           | ----| ----| ---| ---|
|/users                | 创建一个新的User | 检索所有Users | 批量更新Users | 删除所有Users|
|/users/1             | `error` | 检索User=1的详细 | 更新User=1的详细信息（如果存在） | 删除User=1的User |
|/users/1/orders   | 为User=1创建一个新的order | 检索User=1的所有orders | 批量更新User=1的orders | 删除User=1的所有orders |

6. `过滤信息（Filtering）`。如果记录数量很多，服务器不可能都将他们返回给用户。API应该提供参数，过滤返回结果。下面是一些常用的参数。
```css
?limit=10：指定返回记录的数量
?offset=10：指定返回记录的开始位置。
?page=2&per_page=100：指定第几页，以及每页的记录数。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
?animal_type_id=1：指定筛选条件
```
参数的设计允许存在冗余，即允许API路径和URL参数偶尔有重复。比如，GET /zoo/ID/animals 与 GET /animals？zoo_id=ID的含义是相同的。

7. `状态码（Status Codes）`。服务器向用户返回的状态码和提示信息，常见的有以下一些（方括号中是该状态码对应的HTTP动词）
``` css
200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
204 NO CONTENT - [DELETE]：用户删除数据成功。
400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。
403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。
```
状态码的完全列表参见[这里](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

8. `错误处理（Error Handling）`。如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。
```json
{
    error:"Invalid API key"
}
```
9. `返回结果`。针对不同操作，服务器向用户返回的结果应该符合以下规范。
```css
GET /collection：返回资源对象的列表（数组）
GET /collection/resource：返回单个资源对象
POST /collection：返回新生成的资源对象
PUT /collection/resource：返回完整的资源对象
PATCH /collection/resource：返回完整的资源对象
DELETE /collection/resource：返回一个空文档
```
10. `Hypermedia API`（[HATEOAS](http://en.wikipedia.org/wiki/HATEOAS)）
11. `其他`。
- API的身份验证应该使用OAuth 2.0框架
- 服务器返回的数据格式，应该尽量使用JSON，避免使用XML


## Resource
- https://en.wikipedia.org/wiki/Representational_state_transfer
- 微软的 [API设计](https://docs.microsoft.com/zh-cn/azure/architecture/best-practices/api-design)，[API design英文版](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
- [RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html) ，作者阮一峰，2014年5月22日
- [Principles of good RESTful API Design](https://codeplanet.io/principles-good-restful-api-design/)
- https://www.jianshu.com/p/84568e364ee8
- [**RESTful API Design. Best Practices in a Nutshell.**](https://blog.philipphauer.de/restful-api-design-best-practices/) （[RESTful API设计最佳实践](https://www.zcfy.cc/article/restful-api-design-best-practices-in-a-nutshell-4388.html?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)），作者Philipp Hauer
- [REST接口设计规范](http://wangwei.info/about-rest-api/)
- [跟着 Github 学习 Restful HTTP API 设计](http://cizixs.com/2016/12/12/restful-api-design-guide/)
- [Github API](https://developer.github.com/v3/)
- https://www.zhihu.com/question/28557115