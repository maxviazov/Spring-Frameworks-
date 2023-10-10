## What's New in Version 6.1

### Core Container

* [General compatibility with virtual threads](https://github.com/spring-projects/spring-framework/issues/23443) and JDK 21 overall.
* Configuration options for virtual threads: a dedicated [VirtualThreadTaskExecutor](https://docs.spring.io/spring-framework/docs/6.1.0-SNAPSHOT/javadoc-api/org/springframework/core/task/VirtualThreadTaskExecutor.html) and a [virtual threads mode on SimpleAsyncTaskExecutor](https://docs.spring.io/spring-framework/docs/6.1.0-SNAPSHOT/javadoc-api/org/springframework/core/task/SimpleAsyncTaskExecutor.html#setVirtualThreads(boolean)), plus an analogous [SimpleAsyncTaskScheduler](https://docs.spring.io/spring-framework/docs/6.1.0-SNAPSHOT/javadoc-api/org/springframework/scheduling/concurrent/SimpleAsyncTaskScheduler.html) with a new-thread-per-task strategy and a virtual threads mode.
* Lifecycle integration with Project CRaC for JVM checkpoint restore (see [related documentation](https://docs.spring.io/spring-framework/reference/6.1/integration/checkpoint-restore.html)).
* Lifecycle integrated [pause/resume capability](https://github.com/spring-projects/spring-framework/issues/30831) and [parallel graceful shutdown](https://github.com/spring-projects/spring-framework/issues/27090) for `ThreadPoolTaskExecutor` and `ThreadPoolTaskScheduler` as well as `SimpleAsyncTaskScheduler`.
* Async/reactive destroy methods (e.g. on R2DBC `ConnectionFactory`); see [26691](https://github.com/spring-projects/spring-framework/issues/26991).
* Async/reactive cacheable methods, including corresponding support in the `Cache` interface and in `CaffeineCacheManager`; see [17559](https://github.com/spring-projects/spring-framework/issues/17559) and [17920](https://github.com/spring-projects/spring-framework/issues/17920).
* Reactive `@Scheduled` methods (including Kotlin coroutines); see [22924](https://github.com/spring-projects/spring-framework/pull/29924).
* Selecting a specific target scheduler for each `@Scheduled` method; see [20818](https://github.com/spring-projects/spring-framework/issues/20818).
* `@Scheduled` methods for one-time tasks (with just an initial delay); see [31211](https://github.com/spring-projects/spring-framework/issues/31211).
* Observation instrumentation of `@Scheduled` methods; see [29883](https://github.com/spring-projects/spring-framework/issues/29883).
* Spring Framework will not produce observations out-of-the-box for `@Async` or `@EventListener` annotated methods, but will help you with propagating context (e.g. MDC logging with the current trace id) for the execution of those methods. See the new `ContextPropagatingTaskDecorator`, the [relevant reference documentation section](https://docs.spring.io/spring-framework/reference/6.1/integration/observability.html#observability.application-events) and [issue 31130](https://github.com/spring-projects/spring-framework/issues/31130).
* `Validator` factory methods for programmatic validator implementations; see [29890](https://github.com/spring-projects/spring-framework/pull/29890).
* `Validator.validateObject(Object)` with returned `Errors` and `Errors.failOnError` method for flexible programmatic usage; see [19877](https://github.com/spring-projects/spring-framework/issues/19877).
* `MethodValidationInterceptor` throws `MethodValidationException` subclass of `ConstraintViolationException` with violations adapted to `MessageSource` resolvable codes, and to `Errors` instances for `@Valid` arguments with cascaded violations. See [29825](https://github.com/spring-projects/spring-framework/issues/29825), and umbrella issue [30645](https://github.com/spring-projects/spring-framework/issues/30645).
* Support for resource patterns in `@PropertySource`; see [21325](https://github.com/spring-projects/spring-framework/issues/21325).
* Support for `Iterable` and `MultiValueMap` binding in `BeanWrapper` and `DirectFieldAccessor`; see [907](https://github.com/spring-projects/spring-framework/pull/907) and [26297](https://github.com/spring-projects/spring-framework/issues/26297).
* Revised `Instant` and `Duration` parsing (aligned with Spring Boot); see [22013](https://github.com/spring-projects/spring-framework/issues/22013).
* Support for letters other than A-Z in property/field/variable names in SpEL expressions; see [30580](https://github.com/spring-projects/spring-framework/issues/30580). 
* Support for registering a `MethodHandle` as a SpEL function (see [related documentation](https://docs.spring.io/spring-framework/reference/6.1/core/expressions/language-ref/functions.html)).
* Spring AOP now supports Coroutines; see [22462](https://github.com/spring-projects/spring-framework/issues/22462).

### Data Access and Transactions

* Common `TransactionExecutionListener` contract with before/afterBegin, before/afterCommit and before/afterRollback callbacks triggered by the transaction manager (for thread-bound as well as reactive transactions); see [27479](https://github.com/spring-projects/spring-framework/issues/27479).
* `@TransactionalEventListener` and `TransactionalApplicationListener` always run in the original thread, independent from an async multicaster setup; see [30244](https://github.com/spring-projects/spring-framework/issues/30244).
* `@TransactionalEventListener` and `TransactionalApplicationListener` can participate in reactive transactions when the `ApplicationEvent` gets published with the transaction context as its event source; see [27515](https://github.com/spring-projects/spring-framework/issues/27515).
* A failed `CompletableFuture` triggers a rollback for an async transactional method; see [30018](https://github.com/spring-projects/spring-framework/issues/30018).
* `DataAccessUtils` provides various `optionalResult` methods with a `java.util.Optional` return type; see [27735](https://github.com/spring-projects/spring-framework/pull/27735).
* The new `JdbcClient` provides a unified facade for query/update statements on top of `JdbcTemplate` and `NamedParameterJdbcTemplate`, with flexible parameter options as well as flexible result retrieval options; see [30931](https://github.com/spring-projects/spring-framework/issues/30931). 
* `SimplePropertyRowMapper` and `SimplePropertySqlParameterSource` strategies for use with `JdbcTemplate`/`NamedParameterJdbcTemplate` as well as `JdbcClient`, providing flexible constructor/property/field mapping for result objects and named parameter holders; see [26594](https://github.com/spring-projects/spring-framework/issues/26594#issuecomment-1678725276).
* `SQLExceptionSubclassTranslator` can be configured with an overriding `customTranslator`; see [24634](https://github.com/spring-projects/spring-framework/issues/24634).
* The R2DBC `DatabaseClient` provides `bindValues(Map)` for a pre-composed map of parameter values and `bindProperties(Object)` for parameter objects based on bean properties or record components, see [27282](https://github.com/spring-projects/spring-framework/issues/27282).
* The R2DBC `DatabaseClient` provides `mapValue(Class)` for plain database column values and `mapProperties(Class)` for result objects based on bean properties or record components; see [26021](https://github.com/spring-projects/spring-framework/issues/26021).
* `BeanPropertyRowMapper` and `DataClassRowMapper` available for R2DBC as well; see [30530](https://github.com/spring-projects/spring-framework/pull/30530).

### Web Applications

* Spring MVC and WebFlux now have built-in method validation support for controller method parameters with `@Constraint` annotations. That means you no longer need `@Validated` at the controller class level to enable method validation via AOP proxy. Built-in method validation is layered on top of the existing argument validation for model attribute and request body arguments. The two are more tightly integrated and coordinated, e.g. avoiding cases with double validation. See [Upgrading to 6.1](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x#web-applications) for migration details, [29825](https://github.com/spring-projects/spring-framework/issues/29825) for more on the built-in support in M1, and the umbrella issue [30645](https://github.com/spring-projects/spring-framework/issues/30645) for related tasks and feedback.
* [ErrorResponse](https://docs.spring.io/spring-framework/docs/6.1.0-SNAPSHOT/javadoc-api/org/springframework/web/ErrorResponse.html) allows [customization](https://docs.spring.io/spring-framework/reference/6.1/web/webmvc/mvc-ann-rest-exceptions.html#mvc-ann-rest-exceptions-i18n) of `ProblemDetail` type via `MessageSource` and use of custom `ProblemDetail` through its builder.
* Spring MVC throws `NoHandlerFoundException` or `NoResourceFoundException` (new in 6.1) to allow consistent handling of 404 errors, including with an RFC 7807 error response. See [29491](https://github.com/spring-projects/spring-framework/issues/29491).
* The new `RestClient` is a synchronous HTTP client that offers an API similar to `WebClient`, using the same infrastructure as `RestTemplate`. See [29552](https://github.com/spring-projects/spring-framework/issues/29552).
* Jetty-based `ClientHttpRequestFactory` for use with `RestTemplate` and `RestClient`; see [30564](https://github.com/spring-projects/spring-framework/issues/30564).
* JDK HttpClient-based `ClientHttpRequestFactory` for use with `RestTemplate` and `RestClient`; see [30478](https://github.com/spring-projects/spring-framework/pull/30478).
* Reactor Netty-based `ClientHttpRequestFactory` for use with `RestTemplate` and `RestClient`; see [30835](https://github.com/spring-projects/spring-framework/issues/30835).
* Improved buffering in various `ClientHttpRequestFactory` implementations; see [30557](https://github.com/spring-projects/spring-framework/issues/30557).
* JVM checkpoint restore support added to Reactor Netty-based `ClientHttpRequestFactory` for use with `RestTemplate` and `RestClient` and `ClientHttpConnector` for use with `WebClient`; see [31280](https://github.com/spring-projects/spring-framework/issues/31280), [31281](https://github.com/spring-projects/spring-framework/issues/31281) and [31180](https://github.com/spring-projects/spring-framework/issues/31180).
* General Coroutines support revision in WebFlux, which includes [`CoroutineContext` propagation in `CoWebFilter`](https://github.com/spring-projects/spring-framework/issues/27522), [`CoroutineContext` propagation in `coRouter` DSL with `filter`](https://github.com/spring-projects/spring-framework/issues/26977), [a new `context` function in `coRouter` DSL](https://github.com/spring-projects/spring-framework/issues/27010), [Support for `@ModelAttribute` with suspending function in WebFlux](https://github.com/spring-projects/spring-framework/issues/30894) and [consistent usage of the `Mono` variant of `awaitSingle()`](https://github.com/spring-projects/spring-framework/issues/31127).

### Messaging Applications

* Interface parameter annotations are detected for messaging handler methods as well (analogous to web handler methods).
* The SpEL-based `selector` header support in WebSocket messaging is now disabled by default and must be explicitly enabled. See [30550](https://github.com/spring-projects/spring-framework/issues/30550) and [Upgrading to 6.1](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-6.x#messaging-applications) for migration details.
* Observability support for JMS. We now produce observations when publishing messages with `JmsTemplate` and when processing messages with `MessageListener` or `@JmsListener`. See [the reference docs section](ttps://docs.spring.io/spring-framework/reference/6.1/integration/observability.html#observability.jms) and issue [30335](https://github.com/spring-projects/spring-framework/issues/30335).

### Testing

* `ApplicationContext` failure threshold support: avoids repeated attempts to load a failing `ApplicationContext` in the TestContext framework, based on a failure threshold which defaults to 1 but can be configured via a system property (see [related documentation](https://docs.spring.io/spring-framework/reference/6.1/testing/testcontext-framework/ctx-management/failure-threshold.html)).
* Support for recording asynchronous events with `@RecordApplicationEvents`. See [30020](https://github.com/spring-projects/spring-framework/pull/30020).
  * Record events from threads other than the main test thread.
  * Assert events from a separate thread – for example with Awaitility.
* Support for `null` in `MockHttpServletResponse.setCharacterEncoding()`. See [30341](https://github.com/spring-projects/spring-framework/issues/30341).


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
* New `MockHttpServletRequestBuilder.setRemoteAddress()` method.
* The four abstract base test classes for JUnit 4 and TestNG no longer declare listeners via `@TestExecutionListeners` and
instead now rely on registration of default listeners.
