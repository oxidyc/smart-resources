# MongoDB Guide

## Spring Data MongoDB
Spring Data MongoDB 的MongoTemplate提供了两种存储文档方式，分别是save、insert方法，二者的区别：
- `save`：在新增文档时，如有一个相同_ID的文档时，会覆盖原来的；批量操作时，需要遍历列表，进行一个个的插入。
  - void save(Object objectToSave) 保存文档到默认的集合
  - void save(Object objectToSave, String collectionName) 对指定的集合进行保存
- `insert`：在新增文档时，如有一个相同的_ID时，会新增失败；批量操作时，可以一次性插入一整个列表，而不用进行遍历操作，效率相对较高。
  - void insert(Object objectToSave) 保存文档到默认的集合
  - void insertAll(Object objectToSave) 批量添加到默认的集合
  - void insert(Object objectToSave, String collectionName) 对指定的集合进行保存

## 支持的Repository
Keyword                         | Sample                                                | Logical result
-----------------------------   | -----------------------------                         | -----------------------------
After                           | findByBirthdateAfter(Date date)                       | `{"birthdate" : {"$gt" : date}}`
GreaterThan                     | findByAgeGreaterThan(int age)                         | `{"age" : {"$gt" : age}}`
GreaterThanEqual                | findByAgeGreaterThanEqual(int age)                    | `{"age" : {"$gte" : age}}`
Before                          | findByBirthdateBefore(Date date)                      | `{"birthdate" : {"$lt" : date}}`
LessThan                        | findByAgeLessThan(int age)                            | `{"age" : {"$lt" : age}}`
LessThanEqual                   | findByAgeLessThanEqual(int age)                       | `{"age" : {"$lte" : age}}`
Between                         | findAgeBetween(int from, int to)                      | `{"age" : {"$gt" : from, "$lt" : to}}`
In                              | findByAgeIn(Collection ages)                          |  `{"age" : {"$in" : [ages...]}}`
NotIn                           | findByAgeNotIn(Collection ages)                       | `{"age" : {"$nin" : [ages...]}}`
IsNotNull, NotNull              | findByFirstnameNotNull()                              | `{"firstname" : {"$ne" : null}}`
IsNull, Null                    | findByFirstnameNull()                                 | `{"firstname" : null}`
Like, StartingWith, EndingWith  | findByFirstnameLike(String name)                      | `{"firstname" : name} (name as regex)`
NotLike,IsNotLike               | findByFirstnameNotLike(String name)                   | `{"firstname" : {"$not" : name}} (name as regex)`
Containing on String            | findyFirstnameContaining(String name)                 | `{"firstname" : name} (name as regex)`
NotContaining on String         | findByFirstnameNotContaining(String name)             | `{"firstname" : {"$not": name}} (name as regex)`
Containing on Collection        | findByAdressesContaining(Address address)             | `{"addresses" : {"$in" : address}}`
NotContaining on Collection     | findByAddressesNotContaining(Address address)         | `{"addresses" : {"$not":{"$in" : address}}}`
Regex                           | findByFirstnameRegex(String firstname)                | `{"firstname" : {"$regex" : firstname}}`
(No keyword)                    | findByFirstname(String name)                          | `{"firstname" : name}`
Not                             | findByFirstnameNot(String name)                       | `{"firstname" : {"$ne" : name}}`
Near                            | findByLocationNear(Point point)                       | `{"location" :{"$near":[x,y]}}`
Near                            | findByLocationNear(Point point, Distance max)         | `{"location" : {"$near" : [x,y], "$maxDistance" : nax}}`
Near                            | findByLocationNear(Point point, Distance min, Distance max) | `{"location" : {"$near" : [x,y], "$minDistance" : min, "$maxDistance": max}}`
Within                          | findByLocationWithin(Circle circle)                   | `{"location" : {"$geoWithin": {"$center" : [[x,y],distance]}}}`
Within                          | findByLocationWithin(Box box)                         | `{"location" : {"$geoWithin" :{"$box":[[x1,y1],x2,y2]}}}`
IsTrue,True                     | findByActiveIsTrue()                                  | `{"active" : true}`
IsFalse,False                   | findByActiveIsFalse                                   | `{"active": false}`
Exists                          | findByLocationExists(boolean exists)                  | `{"location" : {"$exists" : exists}}`





## Resource
- https://blog.csdn.net/xiaojin21cen/article/details/40480609
- https://www.cnblogs.com/arli/p/7001158.html
- https://docs.spring.io/spring-data/data-mongo/docs/2.1.1.RELEASE/reference/html/#repository-query-keywords