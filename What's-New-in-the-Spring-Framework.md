This page provides information pertaining to new features and changes in various versions
of the Spring Framework.

For assistance with migrating to a newer version of the Spring Framework, consult the
[[Migrating from earlier versions of the Spring Framework]] wiki page.

----
**Table of Contents**

- [What's New in Spring Framework 5.x](#whats-new-in-spring-framework-5x)
- [What's New in Spring Framework 4.x](#whats-new-in-spring-framework-4x)
- [What's New in Spring Framework 3.x](#whats-new-in-spring-framework-3x)

----
# What's New in Spring Framework 5.x

## New Features and Enhancements in Spring Framework 5.0

### JDK 8+ and Java EE 7+ Baseline

* Entire framework codebase based on Java 8 source code level now.
  * Improved readability through inferred generics etc.
  * Conditional support for Java 8 features now in straight code.
* Compatibility with JDK 9 at runtime.
  * In classpath mode as well as automatic module mode.
* Java EE 7 API level required in Spring's corresponding modules now.
  * Servlet 3.1, JMS 2.0, JPA 2.1, Bean Validation 1.1
  * Recent servers: e.g. Tomcat 8.5+, Jetty 9.4+, WildFly 10+
* Compatibility with Java EE 8 API level at runtime.
  * Servlet 4.0, Bean Validation 2.0, JSON Binding API

### Removed Packages, Classes and Methods

* Package `beans.factory.access` (`BeanFactoryLocator` mechanism).
* Package `jdbc.support.nativejdbc` (`NativeJdbcExtractor` mechanism).
* Package `mock.staticmock` removed from `spring-aspects` module.
  * No support for `AnnotationDrivenStaticEntityMockingControl` anymore.
* Packages `web.view.tiles2` and `orm.hibernate3/hibernate4` dropped.
  * Minimum requirement: Tiles 3 and Hibernate 5 now.
* Dropped support: Portlet, Velocity, JasperReports, XMLBeans, JDO, Guava.
  * Recommendation: Stay on Spring Framework 4.3.x for those if needed.
* Many deprecated classes and methods removed across the codebase.
  * A few compromises made for commonly used methods in the ecosystem.

### General Core Revision

* JDK 8+ enhancements:
  * Efficient method parameter access based on Java 8 reflection enhancements.
  * Selective declarations of Java 8 default methods in core Spring interfaces.
  * Consistent use of JDK 7 `Charset` and `StandardCharsets` enhancements.
* JDK 9 compatibility:
  * Consistent instantiation via constructors (with revised exception handling)
* Spring Framework 5.0 comes with its own Commons Logging bridge out of the box.
  * `spring-jcl` instead of standard Commons Logging; still excludable/overridable.
  * Autodetecting Log4j 2.x, SLF4J, JUL (java.util.logging) without any extra bridges.
* `Resource` abstraction provides `isFile` indicator for defensive `getFile` access.
  * Also features NIO-based `readableChannel` accessor now.

### Core Container

* Functional style on `GenericApplicationContext`/`AnnotationConfigApplicationContext`
  * `Supplier`-based bean registration API with bean definition customizer callbacks.
* First-class support for Kotlin through specific functional style extensions.
  * For bean registration as well as `JdbcTemplate` and functional endpoints.
* Support for any `@Nullable` annotations as indicators for optional injection points.
  * Also for Kotlin nullability declarations.
* Consistent detection of transaction, caching, async annotations on interface methods.
  * In case of CGLIB proxies.
* Support for candidate component index (as alternative to classpath scanning).
* XML configuration namespaces streamlined towards unversioned schemas.
  * Always resolved against latest `xsd` files; no support for deprecated features.
  * Version-specific declarations still supported but validated against latest schema.

### Spring WebMVC

* Full Servlet 3.1 signature support in Spring-provided `Filter` implementations.
* Support for Servlet 4.0 `PushBuilder` argument in Spring MVC controller methods.
* `MaxUploadSizeExceededException` for Servlet 3.0 multipart parsing on common servers.
* Unified support for common media types through `MediaTypeFactory` delegate.
  * Superseding use of the Java Activation Framework.
* Data binding with immutable objects (Kotlin / Lombok / `@ConstructorProperties`)
* Support for Jackson 2.9 (GA expected along with Spring Framework 5.0 GA).
* Support for the JSON Binding API (as an alternative to Jackson and GSON).
* Support for Protobuf 3.
* Support for Reactor 3.1 `Flux` and `Mono` as well as RxJava 1.3 and 2.1 as return values from Spring MVC controller methods targeting use of the new reactive `WebClient` (see below) or Spring Data Reactive repositories in Spring MVC controllers.
* New `ParsingPathMatcher` alternative to `AntPathMatcher` with more efficient parsing and [extended syntax](http://docs.spring.io/spring/docs/5.0.0.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/util/patterns/PathPattern.html).
* `@ExceptionHandler` methods allow `RedirectAttributes` arguments (and therefore flash attributes).
* Support for `ResponseStatusException` as a programmatic alternative to `@ResponseStatus`.


### Spring WebFlux

* New [spring-webflux](http://docs.spring.io/spring/docs/5.0.0.BUILD-SNAPSHOT/spring-framework-reference/htmlsingle/#web-reactive) module, an alternative to `spring-webmvc` built on a [reactive](https://github.com/reactive-streams/reactive-streams-jvm) foundation -- fully asynchronous and non-blocking, intended for use in an event-loop execution model vs traditional large thread pool with thread-per-request execution model.
* Reactive infrastructure in `spring-core` such as `Encoder` and `Decoder` for encoding and decoding streams of Objects; `DataBuffer` abstraction, e.g. for using Java `ByteBuffer` or Netty `ByteBuf`; `ReactiveAdapterRegistry` for transparent support of reactive libraries in controller method signatures.
* Reactive infrastructure in `spring-web` including `HttpMessageReader` and `HttpMessageWriter` that build on and delegate to `Encoder` and `Decoder`; server `HttpHandler` with adapters to (non-blocking) runtimes such as Servlet 3.1+ containers, Netty, and Undertow; `WebFilter`, `WebHandler` and other non-blocking contract alternatives to Servlet API equivalents.
* `@Controller` style, annotation-based, programming model, similar to Spring MVC, but supported in WebFlux, running on a reactive stack, e.g. capable of supporting reactive types as controller method arguments, never blocking on I/O, respecting backpressure all the way to the HTTP socket, and running on extra, non-Servlet containers such as Netty and Undertow.
* New [functional web framework](https://github.com/spring-projects/spring-framework/blob/master/src/docs/asciidoc/web/web-flux-functional.adoc) ("WebFlux.fn") as an alternative to the `@Controller`, annotation-based, programming model -- minimal and transparent with an endpoint routing API, running on the same reactive stack and WebFlux infrastructure.
* New `WebClient` with a functional and reactive API for HTTP calls, comparable to the `RestTemplate` but through a fluent API and also excelling in non-blocking and streaming scenarios based on WebFlux infrastructure; in 5.0 the `AsyncRestTemplate` is deprecated in favor of the `WebClient`.

### Testing Improvements

* Complete support for [JUnit 5](http://junit.org/junit5/)'s _Jupiter_ programming and 
  extension models in the Spring TestContext Framework.
  * `SpringExtension`: an implementation of multiple extension APIs from JUnit Jupiter 
    that provides full support for the existing feature set of the Spring TestContext 
    Framework. This support is enabled via `@ExtendWith(SpringExtension.class)`.
  * `@SpringJUnitConfig`: a composed annotation that combines 
    `@ExtendWith(SpringExtension.class)` from JUnit Jupiter with `@ContextConfiguration` 
    from the Spring TestContext Framework.
  * `@SpringJUnitWebConfig`: a composed annotation that combines 
    `@ExtendWith(SpringExtension.class)` from JUnit Jupiter with `@ContextConfiguration` 
    and `@WebAppConfiguration` from the Spring TestContext Framework.
  * `@EnabledIf`: signals that the annotated test class or test method is _enabled_ if
    the supplied SpEL expression or property placeholder evaluates to `true`.
  * `@DisabledIf`: signals that the annotated test class or test method is _disabled_ if
    the supplied SpEL expression or property placeholder evaluates to `true`.
* Support for parallel test execution in the Spring TestContext Framework.
  * See the _Parallel test execution_ section of the _Testing_ chapter for details.
* New _before_ and _after_ test execution callbacks in the Spring TestContext Framework
  with support for TestNG, JUnit 5, and JUnit 4 via the `SpringRunner` (but not via JUnit
  4 rules).
  * New `beforeTestExecution()` and `afterTestExecution()` callbacks in the
    `TestExecutionListener` API and `TestContextManager`.
* `MockHttpServletRequest` now has `getContentAsByteArray()` and `getContentAsString()`
  methods for accessing the content (i.e., request body).
* The `print()` and `log()` methods in Spring MVC Test now print the request body
  if the character encoding has been set in the mock request.
* The `redirectedUrl()` and `forwardedUrl()` methods in Spring MVC Test now support
  URI templates with variable expansion.
* XMLUnit support upgraded to 2.3

----
# What's New in Spring Framework 4.x
The "What's New" guide for Spring Framework 4.x is available in the
[Spring Framework 4.3.x reference manual](http://docs.spring.io/spring/docs/4.3.x/spring-framework-reference/htmlsingle/#spring-whats-new).

----
# What's New in Spring Framework 3.x
The "What's New" guide for Spring Framework 3.x is available in the
[Spring Framework 3.2.x reference manual](http://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/htmlsingle/#spring-whats-new).
