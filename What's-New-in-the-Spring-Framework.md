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

### JDK 8+9 and Java EE 7 Baseline

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

### Core Container Improvements

* JDK 8+ enhancements:
  * Efficient method parameter access based on Java 8 reflection enhancements.
  * Selective declarations of Java 8 default methods in core Spring interfaces.
  * Consistent use of JDK 7 `Charset` and `StandardCharsets` enhancements.
* JDK 9 preparations:
  * Consistent instantiation via constructors (with revised exception handling)
* XML configuration namespaces streamlined towards unversioned schemas.
  * Always resolved against latest `xsd` files; no support for deprecated features.
  * Version-specific declarations still supported but validated against latest schema.
* Spring Framework 5.0 comes with its own Commons Logging bridge out of the box.
  * `spring-jcl` instead of standard Commons Logging; still excludable/overridable.
  * Autodetecting Log4j 2.x, SLF4J, JUL (java.util.logging) without any extra bridges.
* `Resource` abstraction provides `isFile` indicator for defensive `getFile` access.
  * Also features NIO-based `readableChannel` accessor.
* Consistent detection of transaction, caching, async annotations on interface methods.
  * In case of CGLIB proxies.
* Functional style on `GenericApplicationContext`/`AnnotationConfigApplicationContext`
  * `Supplier`-based bean registration API with bean definition customizer callbacks.
* First-class support for Kotlin through specific functional style extensions.
  * For bean registration as well as `JdbcTemplate` and functional endpoints.

### General Web Improvements

* Full Servlet 3.1 signature support in Spring-provided `Filter` implementations.
* Unified support for common media types through `MediaTypeFactory` delegate.
  * Superseding use of the Java Activation Framework.
* Data binding with immutable objects (Kotlin / Lombok / @ConstructorProperties)
* Support for Jackson 2.9 (GA expected along with Spring Framework 5.0 GA).
* Support for the JSON Binding API (as an alternative to Jackson and GSON).
* Support for Protobuf 3.

### Reactive Programming Model

* `spring-core` `DataBuffer` and `Encoder`/`Decoder` abstractions with non-blocking semantics.
* `spring-web` HTTP message codec implementations with JSON (Jackson) and XML (JAXB) support.
* New `spring-webflux` module with reactive support for the `@Controller` programming model,
adapting [Reactive Streams](https://github.com/reactive-streams/reactive-streams-jvm) to Servlet
3.1 containers as well as non-Servlet runtimes such as Netty and Undertow.
* New functional endpoint registration model on the same reactive web foundation.
* New `WebClient` with reactive support on the client side.
* For more details refer to the chapter
["WebFlux framework"](http://docs.spring.io/spring/docs/5.0.0.BUILD-SNAPSHOT/spring-framework-reference/htmlsingle/#web-reactive) in the reference docs.

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
* Support for parallel test execution in the Spring TestContext Framework. See the
  _Parallel test execution_ section of the _Testing_ chapter for details.
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
* XMLUnit support upgraded to 2.2

----
# What's New in Spring Framework 4.x
The "What's New" guide for Spring Framework 4.x is available in the
[Spring Framework 4.3.x reference manual](http://docs.spring.io/spring/docs/4.3.x/spring-framework-reference/htmlsingle/#spring-whats-new).

----
# What's New in Spring Framework 3.x
The "What's New" guide for Spring Framework 3.x is available in the
[Spring Framework 3.2.x reference manual](http://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/htmlsingle/#spring-whats-new).
