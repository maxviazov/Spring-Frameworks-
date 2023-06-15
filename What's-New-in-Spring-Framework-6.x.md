## What's New in Version 6.1

### Core Container

* Configuration options for virtual threads on JDK 21: a dedicated [VirtualThreadTaskExecutor](https://docs.spring.io/spring-framework/docs/6.1.0-SNAPSHOT/javadoc-api/org/springframework/core/task/VirtualThreadTaskExecutor.html) and [a flag on SimpleAsyncTaskExecutor](https://docs.spring.io/spring-framework/docs/6.1.0-SNAPSHOT/javadoc-api/org/springframework/core/task/SimpleAsyncTaskExecutor.html#setVirtualThreads(boolean))
* Lifecycle integration with Project CRaC for JVM checkpoint restore (see [related documentation](https://docs.spring.io/spring-framework/reference/6.1-SNAPSHOT/integration/checkpoint-restore.html)).
* Support for resolving JDK 21 `SequencedCollection/Set/Map` at injection points.
* Revised `Instant` and `Duration` parsing (aligned with Spring Boot).
* Support for registering a `MethodHandle` as a SpEL function.
* Async/reactive destroy methods (e.g. on R2DBC `ConnectionFactory`).
* Reactive `@Scheduled` methods (including Kotlin coroutines).
* `Validator` factory methods for programmatic validator implementations. See [29890](https://github.com/spring-projects/spring-framework/pull/29890)
* `MethodValidationInterceptor` throws `MethodValidationException` subclass of `ConstraintViolationException` with violations adapted to `MessageSource` resolvable codes, and to `Errors` instances for `@Valid` arguments with cascaded violations. See [29825](https://github.com/spring-projects/spring-framework/issues/29825), and umbrella issue [30645](https://github.com/spring-projects/spring-framework/issues/30645).

### Data Access and Transactions

* Failed `CompletableFuture` triggers rollback for async transactional method.
* `BeanPropertyRowMapper` and `DataClassRowMapper` available for R2DBC as well.

### Web Applications

* Spring MVC and WebFlux now have built-in method validation support for controller method parameters with `@Constraint` annotations. That means you no longer need `@Validated` at the controller class level to enable method validation via AOP proxy. Built-in method validation is layered on top of the existing argument validation for model attribute and request body arguments. The two are more tightly integrated and coordinated, e.g. avoiding cases with double validation. See [Upgrading to 6.1](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x#web-applications) for migration details, [29825](https://github.com/spring-projects/spring-framework/issues/29825) for more on the built-in support in M1, and the umbrella issue [30645](https://github.com/spring-projects/spring-framework/issues/30645) for related tasks and feedback.
* Jetty-based ClientHttpRequestFactory, for use with RestTemplate.


## What's New in Version 6.0

### JDK 17+ and Jakarta EE 9+ Baseline

* Entire framework codebase based on Java 17 source code level now.
* Migration from `javax` to `jakarta` namespace for Servlet, JPA, etc.
* Runtime compatibility with Jakarta EE 9 as well as Jakarta EE 10 APIs.
* Compatible with latest web servers: [Tomcat 10.1](https://tomcat.apache.org/whichversion.html), [Jetty 11](https://www.eclipse.org/jetty/download.php), [Undertow 2.3](https://github.com/undertow-io/undertow).
* Early compatibility with [virtual threads](https://spring.io/blog/2022/10/11/embracing-virtual-threads) (in preview as of JDK 19).

### General Core Revision

* Upgrade to ASM 9.4 and Kotlin 1.7.
* Complete CGLIB fork with support for capturing CGLIB-generated classes.
* Comprehensive foundation for [Ahead-Of-Time transformations](https://spring.io/blog/2022/03/22/initial-aot-support-in-spring-framework-6-0-0-m3).
* First-class support for [GraalVM](https://www.graalvm.org/) native images (see [related Spring Boot 3 blog post](https://spring.io/blog/2022/09/26/native-support-in-spring-boot-3-0-0-m5)).

### Core Container

* Basic bean property determination without `java.beans.Introspector` by default.
* AOT processing support in `GenericApplicationContext` (`refreshForAotProcessing`).
* Bean definition transformation based on pre-resolved constructors and factory methods.
* Support for early proxy class determination for AOP proxies and configuration classes.
* `PathMatchingResourcePatternResolver` uses NIO and module path APIs for scanning, enabling support for classpath scanning within a GraalVM native image and within the Java module path, respectively.
* `DefaultFormattingConversionService` supports ISO-based default `java.time` type parsing.

### Data Access and Transactions

* Support for predetermining JPA managed types (for inclusion in AOT processing).
* JPA support for [Hibernate ORM 6.1](https://hibernate.org/orm/releases/6.1/) (retaining compatibility with Hibernate ORM 5.6).
* Upgrade to [R2DBC 1.0](https://r2dbc.io/) (including R2DBC transaction definitions).
* Aligned data access exception translation between JDBC, R2DBC, JPA and Hibernate.
* Removal of JCA CCI support.

### Spring Messaging

* [RSocket interface client](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#rsocket-interface) based on `@RSocketExchange` service interfaces.
* Early support for Reactor Netty 2 based on [Netty 5](https://netty.io/wiki/new-and-noteworthy-in-5.0.html) alpha.
* Support for Jakarta WebSocket 2.1 and its standard WebSocket protocol upgrade mechanism.

### General Web Revision

* [HTTP interface client](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/integration.html#rest-http-interface) based on `@HttpExchange` service interfaces.
* Support for [RFC 7807 problem details](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web.html#mvc-ann-rest-exceptions).
* Unified HTTP status code handling.
* Support for Jackson 2.14.
* Alignment with Servlet 6.0 (while retaining runtime compatibility with Servlet 5.0).

### Spring MVC

* `PathPatternParser` used by default (with the ability to opt into `PathMatcher`).
* Removal of outdated Tiles and FreeMarker JSP support.
 
### Spring WebFlux

* New `PartEvent` API to stream multipart form uploads (both on [client](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#partevent-2) and [server](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#partevent)).
* New `ResponseEntityExceptionHandler` to customize WebFlux exceptions and render RFC 7807 [error responses](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#webflux-ann-rest-exceptions).
* `Flux` return values for non-streaming media types (no longer collected to `List` before written).
* Early support for Reactor Netty 2 based on [Netty 5](https://netty.io/wiki/new-and-noteworthy-in-5.0.html) alpha.
* JDK `HttpClient` integrated with `WebClient`.

### Observability

Direct Observability instrumentation with [Micrometer Observation](https://micrometer.io/docs/observation) in several parts of the Spring Framework. The `spring-web` module now requires `io.micrometer:micrometer-observation:1.10+` as a compile dependency.

* `RestTemplate` and `WebClient` are instrumented to produce HTTP client request observations.
* Spring MVC can be instrumented for HTTP server observations using the new `org.springframework.web.filter.ServerHttpObservationFilter`.
* Spring WebFlux can be instrumented for HTTP server observations using the new `org.springframework.web.filter.reactive.ServerHttpObservationFilter`.
* Integration with Micrometer [Context Propagation](https://github.com/micrometer-metrics/context-propagation#context-propagation-library) for `Flux` and `Mono` return values from controller methods. 

### Testing

* Support for testing AOT-processed application contexts on the JVM or within a GraalVM native image.
* Integration with HtmlUnit 2.64+ request parameter handling.
* Servlet mocks (`MockHttpServletRequest`, `MockHttpSession`) are based on Servlet API 6.0 now.