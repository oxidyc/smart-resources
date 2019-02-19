# Spring Webflux: A Basic CRUD Application

Source Code can be found at [Github](https://github.com/mydeveloperplanet/myspringwebfluxcrudplanet)

## Setup
Create a project with Spring Initializr. Select the following dependencies:
- Java 9
- Spring Boot 2.0.0
- Reactive Web
Generate the project and import it into your IDE.

Need th following:
- The domain objects
- A data repository
- A handler(read:service)
- A router

## Create the Domain Objects
The domain objects will be created in package `io.smart.tutorial.webflux.domain` .
```java
public class Show{
    private String id;
    private String title;

    //... getter and setter
}
```
## Create the `Show` Repository
create in the `io.smart.tutorial.webflux.repository` package a `ReactiveShowRepository`. all the methods that need to be implemented, make use of the reactive types `Mono` and `Flux`.
```java
@Repository
public class ReactiveShowRepository implements ReactiveCrudRepository<Show,String>{
    @Override
    public <S extends Show> Mono<S> save(S s) {
        return null;
    }

    @Override
    public <S extends Show> Flux<S> saveAll(Iterable<S> iterable) {
        return null;
    }

    @Override
    public <S extends Show> Flux<S> saveAll(Publisher<S> publisher) {
        return null;
    }

    @Override
    public Mono<Show> findById(String s) {
        return null;
    }

    @Override
    public Mono<Show> findById(Publisher<String> publisher) {
        return null;
    }

    @Override
    public Mono<Boolean> existsById(String s) {
        return null;
    }

    @Override
    public Mono<Boolean> existsById(Publisher<String> publisher) {
        return null;
    }

    @Override
    public Flux<Show> findAll() {
        return null;
    }

    @Override
    public Flux<Show> findAllById(Iterable<String> iterable) {
        return null;
    }

    @Override
    public Flux<Show> findAllById(Publisher<String> publisher) {
        return null;
    }

    @Override
    public Mono<Long> count() {
        return null;
    }

    @Override
    public Mono<Void> deleteById(String s) {
        return null;
    }

    @Override
    public Mono<Void> deleteById(Publisher<String> publisher) {
        return null;
    }

    @Override
    public Mono<Void> delete(Show show) {
        return null;
    }

    @Override
    public Mono<Void> deleteAll(Iterable<? extends Show> iterable) {
        return null;
    }

    @Override
    public Mono<Void> deleteAll(Publisher<? extends Show> publisher) {
        return null;
    }

    @Override
    public Mono<Void> deleteAll() {
        return null;
    }
}
```
## Create the Handler
```java
public class ShowHandler{
    private final ReactiveShowRepository showRepo;

    public ShowHandler(ReactiveShowRepository showRepo) {
        this.showRepo = showRepo;
    }

    public Mono<ServerResponse> all(ServerRequest serverRequest) {
        Flux<Show> shows = this.showRepo.findAll();
        return ServerResponse.ok().body(shows, Show.class);
    }
}
```
## Create the Router
create the Router in order to link a URL to our Handler. RouterFunctions are to be defined in a WebConfig class, which you can read about here.
```java
@Configuration
@EnableWebFlux
public class WebConfig implements WebFluxConfigurer {

    @Bean
    public RouterFunction<ServerResponse> routeShow(ShowHandler showHandler) {
        return RouterFunctions
            .route(RequestPredicates.GET("/shows"), showHandler::all);
    }
}
```


## Resource
- [Spring WebFlux: a basic CRUD application (part 1)](https://mydeveloperplanet.com/2018/03/21/spring-webflux-a-basic-crud-application-part-1/)
- [Spring Webflux: A Basic CRUD Application (Part 1) ](https://dzone.com/articles/spring-webflux-a-basic-crud-application-part-1)
- [Spring WebFlux: A Basic CRUD Application (Part 2) ](https://dzone.com/articles/spring-webflux-a-basic-crud-application-part-2)