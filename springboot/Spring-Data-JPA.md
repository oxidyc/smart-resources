# Spring Data JPA

## Supported keywords inside method names
| Keyword | Sample | JPQL snippet |
|------|------|------|
| And | findByLastnameAndFirstname | ... where x.lastname = ?1 and x.firstname = ?2 |
| Or | findByLastnameOrFirstname | ... where x.lastname = ?1 or x.firstname = ?2 |
| Is,Equals | findByFirstname,findByFirstnameIs,findByFirstnameEquals | ... where x.firstname = ?1 |
| Between | findByStartDateBetween | ... where x.startDate between ?1 and ?2 |
| LessThan | findByAgeLessThan | ... where x.age < ?1 |
| LessThanEqual | findByAgeLessThanEqual | ... where x.age <= ?1 |
| GreaterThan | findByAgeGreaterThan | ... where x.age > ?1 |
| GreaterThanEqual | findByAgeGreaterThanEqual | ... where x.age >= ?1 |
| After | findByStartDateAfter | ... where x.startDate > ?1 |
| Before | findByStartDateBefore | ... where x.startDate < ?1 |
| IsNull | findByAgeIsNull | ... where x.age is null |
| IsNotNull,NotNull | findByAge(Is)NotNull | ... where x.age not null |
| Like | findByFirstnameLike | ... where x.firstname like ?1 |
| NotLike | findByFirstnameNotLike | ... where x.firstname not like ?1 |
| StartingWith | findByFirstnameStartingWith | ... where x.firstname like ?1 (parameter bound with appended %) |
| EndingWith | findByFirstnameEndingWith | ... where x.firstname like ?1 (parameter bound with prepended %) |
| Containing | findByFirstnameContaining | ... where x.firstname like ?1 (parameter bound wrapped in %) |
| OrderBy | findByAgeOrderByLastnameDesc | ... where x.age = ?1 order by x.lastname desc |
| Not | findByLastnameNot | ... where x.lastname <> ?1 |
| In | findByAgeIn(Collection<Age> ages) | ... where x.age in ?1 |
| NotIn | findByAgeNotIn(Collection<Age> ages) | ... where x.age not in ?1 |
| True | findByActiveTrue() | ... where x.active = true |
| False | findByActiveFalse() | ... where x.active = false |
| IgnoreCase | findByFirstnameIgnoreCase | ... where UPPER(x.firstame) = UPPER(?1) |

## Query keywords
| Logical keyword | Keyword expressions |
|------|------|
| AND | And |
| OR | Or |
| AFTER | After, IsAfter |
| BEFORE | Before, IsBefore |
| CONTAINING | Containing, IsContaining, Contains |
| BETWEEN | Between, IsBetween |
| ENDING_WITH | EndingWith, IsEndingWith, EndsWith |
| EXISTS | Exists |
| FALSE | False, IsFalse |
| GREATER_THAN | GreaterThan, IsGreaterThan |
| GREATER_THAN_EQUALS | GreaterThanEqual, IsGreaterThanEqual |
| IN | In, IsIn |
| IS | Is, Equals, (or no keyword) |
| IS_EMPTY | IsEmpty, Empty |
| IS_NOT_EMPTY | IsNotEmpty, NotEmpty |
| IS_NOT_NULL | NotNull, IsNotNull |
| IS_NULL | Null, IsNull |
| LESS_THAN | LessThan, IsLessThan |
| LESS_THAN_EQUAL | LessThanEqual, IsLessThanEqual |
| LIKE | Like, IsLike |
| NEAR | Near, IsNear |
| NOT | Not, IsNot |
| NOT_IN | NotIn, IsNotIn |
| NOT_LIKE | NotLike, IsNotLike |
| REGEX | Regex, MatchesRegex, Matches |
| STARTING_WITH | StartingWith, IsStartingWith, StartsWith |
| TRUE | True, IsTrue |
| WITHIN | Within, IsWithin |


## Resource
- https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.sample-app.finders.strategies
- https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repository-query-keywords