## What's New in Version 6.0

### JDK 17+ and Jakarta EE 9+ Baseline

* Entire framework codebase based on Java 17 source code level now.
* Migration from "javax" to "jakarta" namespace for Servlet, JPA, etc.
* Compatible with latest web container generation: Tomcat 10, Jetty 11.
* Early compatibility with Jakarta EE 10 based providers (e.g. Jetty 12).
* Early compatibility with virtual threads (in preview as of JDK 19).

### General Core Revision

* Upgrade to ASM 9.4 and Kotlin 1.7.
* Complete CGLIB fork with support for capturing CGLIB-generated classes.
* Comprehensive foundation for [Ahead-Of-Time transformations](https://spring.io/blog/2022/03/22/initial-aot-support-in-spring-framework-6-0-0-m3).
* First-class support for [GraalVM](https://www.graalvm.org/) native images (see [related Spring Boot 3 blog post](https://spring.io/blog/2022/09/26/native-support-in-spring-boot-3-0-0-m5)).
* Early support for Netty 5 (alpha) in parallel to Netty 4.1.84+.

### Core Container

* AOT processing support in GenericApplicationContext ("refreshForAotProcessing").
* Bean definition transformation based on pre-resolved constructors and factory methods.
* Support for early proxy class determination for AOP proxies and configuration classes.
* PathMatchingResourcePatternResolver uses NIO and module path APIs for scanning.

### Data Access and Transactions

* Support for pre-determining JPA managed types (for inclusion in AOT processing).
* JPA support for Hibernate ORM 6 (retaining compatibility with Hibernate ORM 5.6).
* Upgrade to R2DBC 1.0 (including R2DBC transaction definitions).

### Spring Messaging

* Support for RSocket interface clients.
* Early support for Reactor Netty 2 (based on Netty 5).

### General Web Revision

* HTTP interface clients based on @HttpExchange service interfaces.
* Support for RFC 7807 problem details.
* Unified HTTP status code handling.
* Micrometer-based observability for RestTemplate.

### Spring MVC

* PathPatternParser by default (with the ability to opt into PathMatcher).
* Removal of outdated Tiles and FreeMarker JSP support.
 
### Spring WebFlux

* Revised reactive multipart processing.
* JDK HttpClient integration with WebClient.
* Micrometer-based observability for WebClient.

### Testing

* Support for testing AOT-processed application contexts.