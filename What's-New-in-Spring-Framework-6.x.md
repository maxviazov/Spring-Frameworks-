## What's New in Version 6.0

### JDK 17+ and Jakarta EE 9+ Baseline

* Entire framework codebase based on Java 17 source code level now.
* Migration from "javax" to "jakarta" namespace for Servlet, JPA, etc.
* Compatible with latest web container generation: [Tomcat 10](https://tomcat.apache.org/whichversion.html), [Jetty 11](https://www.eclipse.org/jetty/download.php).
* Early compatibility with [virtual threads](https://spring.io/blog/2022/10/11/embracing-virtual-threads) (in preview as of JDK 19).

### General Core Revision

* Upgrade to ASM 9.4 and Kotlin 1.7.
* Complete CGLIB fork with support for capturing CGLIB-generated classes.
* Comprehensive foundation for [Ahead-Of-Time transformations](https://spring.io/blog/2022/03/22/initial-aot-support-in-spring-framework-6-0-0-m3).
* First-class support for [GraalVM](https://www.graalvm.org/) native images (see [related Spring Boot 3 blog post](https://spring.io/blog/2022/09/26/native-support-in-spring-boot-3-0-0-m5)).

### Core Container

* AOT processing support in GenericApplicationContext ("refreshForAotProcessing").
* Bean definition transformation based on pre-resolved constructors and factory methods.
* Support for early proxy class determination for AOP proxies and configuration classes.
* PathMatchingResourcePatternResolver uses NIO and module path APIs for scanning.

### Data Access and Transactions

* Support for pre-determining JPA managed types (for inclusion in AOT processing).
* JPA support for Hibernate ORM 6 (retaining compatibility with Hibernate ORM 5.6).
* Upgrade to R2DBC 1.0 (including R2DBC transaction definitions).
* Removal of JCA CCI support.

### Spring Messaging

* [RSocket interface client](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#rsocket-interface) based on `@RSocketExchange` service interfaces.
* Early support for Reactor Netty 2 based on [Netty 5](https://netty.io/wiki/new-and-noteworthy-in-5.0.html) alpha.

### General Web Revision

* [HTTP interface client](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/integration.html#rest-http-interface) based on `@HttpExchange` service interfaces.
* Support for [RFC 7807 problem details](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web.html#mvc-ann-rest-exceptions).
* Unified HTTP status code handling.
* Micrometer-based observability for `RestTemplate`.

### Spring MVC

* `PathPatternParser` used by default (with the ability to opt into `PathMatcher`).
* Integration with Micrometer [Context Propagation](https://github.com/micrometer-metrics/context-propagation#context-propagation-library) for `Flux` and `Mono` return values from controller methods.
* Removal of outdated Tiles and FreeMarker JSP support.
 
### Spring WebFlux

* New [`PartEvent`](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#partevent) API to stream multipart form uploads (both on client and server).
* Addition of `ResponseEntityExceptionHandler` to customize WebFlux exceptions and render RFC 7807 [error responses](https://docs.spring.io/spring-framework/docs/6.0.0-RC1/reference/html/web-reactive.html#webflux-ann-rest-exceptions).
* `Flux` return values for non-streaming media types (no longer collected to List before written).
* Early support for Reactor Netty 2 based on [Netty 5](https://netty.io/wiki/new-and-noteworthy-in-5.0.html) alpha.
* JDK `HttpClient` integrated with `WebClient`.
* Micrometer-based observability for `WebClient`.

### Testing

* Support for testing AOT-processed application contexts.
* Integration with HtmlUnit 2.64 request parameter handling.