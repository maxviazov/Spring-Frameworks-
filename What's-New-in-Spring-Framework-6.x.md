## What's New in Version 6.0

### JDK 17+ and Jakarta EE 9+ Baseline

* Entire framework codebase based on Java 17 source code level now.
* Migration from `javax` to `jakarta` namespace for Servlet, JPA, etc.
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