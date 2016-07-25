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
  * 
* Java EE 7 API level required in Spring's corresponding modules now.
  * Servlet 3.1, JMS 2.0, JPA 2.1, Bean Validation 1.1
* Full compatibility with JDK 9 as of July 2016.
  * Project spring-framework can be built on JDK 9; test suite passes.

### Removed Packages, Classes and Methods

* Package mock.staticmock removed from spring-aspects module.
  * No support for AnnotationDrivenStaticEntityMockingControl anymore.
* Packages web.view.tiles2 and orm.hibernate3/hibernate4 dropped.
  * Minimum requirement: Tiles 3 and Hibernate 5 now.
* Support dropped: Portlet, Velocity, JDO, OpenJPA, XMLBeans, Guava.
  * Recommendation: Stay on Spring Framework 4.3 for those if needed.
* Many deprecated classes and methods removed across the codebase.
  * A few compromises made for commonly used methods in the ecosystem.

### Core Container Improvements

* JDK 8+ enhancements
  * Efficient method parameter access based on Java 8 reflection enhancements.
  * Selective use of Java 8 default methods in core Spring interfaces.
  * Consistent use of JDK 7 Charset and StandardCharsets enhancements.
* JDK 9 preparations
  * Consistent instantiation via constructors (with revised exception handling)

### Reactive Programming Model

### Web Improvements

* Support for Protobuf 3.0

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
* New _before_ and _after_ test execution callbacks in the Spring TestContext Framework
  with support for TestNG, JUnit 5, and JUnit 4 via the `SpringRunner` (but not via JUnit
  4 rules).
  * New `beforeTestExecution()` and `afterTestExecution()` callbacks in the
    `TestExecutionListener` API and `TestContextManager`.
* XMLUnit support upgraded to 2.2

----
# What's New in Spring Framework 4.x
The "What's New" guide for Spring Framework 4.x is available in the
[Spring Framework 4.3.x reference manual](http://docs.spring.io/spring/docs/4.3.x/spring-framework-reference/htmlsingle/#spring-whats-new).

----
# What's New in Spring Framework 3.x
The "What's New" guide for Spring Framework 3.x is available in the
[Spring Framework 3.2.x reference manual](http://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/htmlsingle/#spring-whats-new).
