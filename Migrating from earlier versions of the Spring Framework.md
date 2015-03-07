This page provides information when upgrading to newer versions of the Spring Framework. If you find items not covered yet, please raise a [ticket in JIRA](http://jira.springsource.org) or submit a pull-request against this page.

### Actively supported generations: 3.2 and 4.1
Note that the 3.0.x and 3.1.x lines have been retired already, with no support whatsoever available anymore, in favor of the 3.2.x line. Limited support for 4.0.x is still available but no further maintenance releases are planned in that line. We strongly recommend an upgrade to the latest Spring Framework 3.2.x release or - preferably - to the 4.1.x line: http://projects.spring.io/spring-framework/

## Migrating to Spring Framework 4.1
For an overview of new features, refer to [New Features and Enhancements in Spring Framework 4.1](http://docs.spring.io/spring-framework/docs/4.1.x/spring-framework-reference/htmlsingle/#new-in-4.1) in the reference documentation.

In general, there are no special migration steps from 4.0 to 4.1. Make sure that you satisfy all of 4.0's requirements as stated in the 4.0 section below. 4.1 will then just be a minor upgrade, with the most noticeable part being the enforcement of several optional dependency versions...

### Enforced minimum dependency versions
As of Spring Framework 4.1, several optional dependencies are required to be within the supported range: in particular, _EhCache 2.5+, Quartz 2.1.4+, Jackson 2.1+, and ROME 1.5+_ (see below for details about 4.x dependency declarations in the Spring Framework 4.0 section). Older versions have still been tolerated in the Spring Framework 4.0.x line for a smoother upgrade path; as of 4.1, the intended minimum versions are being enforced. _Most importantly, don't use Quartz 1.8.x anymore; upgrade to Quartz 2.1.4+ instead!_

Note that as of Spring Framework 4.1.4, Apache HttpComponents HttpClient needs to be 4.3+ across the framework. The previous partial tolerance of old HttpClient versions had to be dropped in order to fix several configuration issues when running against 4.3+.

## Migrating to Spring Framework 4.0
For a general overview of new features, refer to [New Features and Enhancements in Spring Framework 4.0](http://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/htmlsingle/#new-in-4.0) in the reference documentation.

### JDK 6
Spring Framework 4.0 requires Java SE 6 or above: specifically, a minimum API level equivalent to JDK 6 update 18, a.k.a. 1.6.0_18, as released in January 2010. You have to update to a recent version of JDK 6 at least: From a known bug-fix level, we require a minimum of JDK 6 update 21, and we suggest JDK 6 update 25 or higher from a support perspective. Java 7 and 8 are recommended for use with Spring Framework 4.0, with Java 8 supported in production since Oracle's JDK 8 launch in March 2014.

#### A note on the IBM JDK
Spring generally supports equivalent generations of the IBM JDK and JRE, in particular as shipped with the WebSphere application server. Since not only WebSphere 7 but also WebSphere 8 and 8.5 have been shipping with IBM JDK 6 as the default JDK up until 2013, we intend to retain our JDK 6 support for the entire Spring Framework 4.x line, as long as those generations of WebSphere are supported by IBM themselves. At the same time, if available to you, we recommend IBM JDK 7 with WebSphere 8.5.

### Java EE 6
If you deploy your Spring applications to Java EE servers, we recommend server generations certified for Java EE 6. Of particular importance are the JPA 2.0 and Servlet 3.0 specifications. That said, it is still possible to deploy Spring 4 applications to servers with a Servlet 2.5 container (e.g. Google App Engine, WebSphere 7, WebLogic 10.3); however, some Servlet 3.0 based Spring features won't be available then. For Tomcat, the same rules apply: We recommend Tomcat 7 or 8 but still support Tomcat 6 as well.

#### A note on Java EE levels
The Spring Framework generally doesn't require a specific level of Java EE overall but rather specific minimum levels of individual specifications, such as JPA 2.0. This approach allows for running on "intermediate" server generations which selectively introduce new specifications while being based on an older EE platform level: e.g. WebSphere 7.0.0.9 with its JPA 2.0 feature pack, WebLogic 10.3.4 with its JPA 2.0 patch, or now WebLogic 12.1.3 (as released in June 2014) with its JPA 2.1 support and WebSphere 8.5 Liberty Profile (December 2014 edition) with its Servlet 3.1 and JSR-236 Concurrency support on an EE 6 baseline.

### Dependency updates
As of Spring Framework 4.0.3, we declare the following minimum (optional) dependencies as officially supported. Those versions and later are what the Spring team recommends, in particular with respect to providing support for Spring applications that interact with those servers and libraries. Note that earlier versions may still work with Spring to some degree, as long as the fundamental system requirements are met; however, when using older versions, you are on your own from a support perspective.

#### Specifications
* Servlet 3.0  _(2.5 supported for deployment)_
* JPA 2.0
* Bean Validation 1.0
* JSF 2.0
* JCache 1.0
* JDO 3.0

#### Servers
* Tomcat 6.0.33 / 7.0.20 / 8.0.9
* Jetty 7.5
* JBoss AS 6.1  _(note: JBoss EAP 6 recommended, since AS 6/7 community releases have many unresolved bugs)_
* GlassFish 3.1  _(note: deployment workaround necessary for non-serializable session attributes)_
* Oracle WebLogic 10.3.4  _(with JPA 2.0 patch applied)_
* IBM WebSphere 7.0.0.9  _(with JPA 2.0 feature pack installed)_

#### Libraries
* Hibernate Validator 4.3
* Hibernate ORM 3.6.10  _(note: to be deprecated as of Spring Framework 4.2, with Hibernate 4.2/4.3 recommended)_
* Apache Tiles 2.2.2 _(note: to be deprecated as of Spring Framework 4.2, with Tiles 3.0.5 recommended)_
* Apache HttpComponents 4.3 _(required for Spring's http.client package, and for all of Spring as of 4.1.4)_
* EhCache 2.4.7 _(note: minimum 2.5 as of Spring Framework 4.1, with EhCache 2.8 or later recommended)_
* Quartz 1.8.6 _(note: minimum 2.1.4 as of Spring Framework 4.1, with Quartz 2.2.1 recommended)_
* Jackson 1.8.6 _(note: minimum 2.1 as of Spring Framework 4.1, with Jackson 2.3 or later recommended)_
* Rome 1.0 _(note: minimum 1.5 as of Spring Framework 4.1, dependency group id has also changed from "rome" to "com.rometools")_
* Groovy 1.8.6 _(note: 2.3 or later recommended)_
* Joda-Time 2.1 _(note: 2.3 or later recommended)_
* Hessian 4.0.33
* XStream 1.4
* Apache Velocity 1.7
* Apache POI 3.8
* Apache Derby 10.8
* JUnit 4.7 _(note: minimum 4.9 as of Spring Framework 4.1, with JUnit 4.11 or later recommended)_

### Deprecated code
The following classes and methods have been deprecated in Spring Framework 4.0 or will be deprecated along the Spring Framework 4.x line. They will be removed at a future date, so please check the javadocs and migrate to the suggested alternatives...

#### Hibernate 3.6.10
The `org.springframework.orm.hibernate3` package will be deprecated as of Spring Framework 4.2. We keep fully supporting it for the time being against Spring Framework 4.0 and 4.1. However, we recommend a timely upgrade to Hibernate 4.2/4.3.

As of Spring Framework 4.0.1, we provide a HibernateTemplate variant in `org.springframework.orm.hibernate4` to ease migration for common Hibernate 3.x data access code, in particular if your motivation for an upgrade is the lack of bug fixes in the Hibernate 3.x line. Note that newly written code is recommended to use Hibernate's native `SessionFactory.getCurrentSession()` style.

On a related note, HibernateInterceptor is deprecated in `org.springframework.orm.hibernate3` and doesn't exist anymore in `org.springframework.orm.hibernate4`. As a replacement for basic Session binding needs outside of transactions, consider the use of the new OpenSessionInterceptor variant, available for both Hibernate 3 and 4 as of Spring Framework 4.0.2.

Note: The Spring Framework 4.0.0 release accidentally restricted HibernateTemplate's List element types to Object only. This has been fixed as of 4.0.2 (https://jira.springsource.org/browse/SPR-11402), allowing for immediate casts to specifically typed Lists again. If you run into any issues migrating existing Hibernate access code, please upgrade to Spring Framework 4.0.2 first.

#### Tiles 2.2.2
While Spring Framework 4.0 and 4.1 still fully support Tiles 2.2.2, the corresponding `org.springframework.web.servlet.view.tiles2` package will be deprecated as of Spring Framework 4.2. We recommend a timely upgrade to Tiles 3.0.5, supported in `org.springframework.web.servlet.view.tiles3`.

#### Quartz 1.8
Quartz 1.8 support in the `org.springframework.scheduling.support` package is deprecated and has been removed for Spring Framework 4.1, with that package only working with Quartz 2.1.4+ from then onwards.

#### Jackson 1.8/1.9
All Jackson v1 support is deprecated in favor of Jackson v2 and has been removed in Spring Framework 4.1:
* `JacksonObjectMapperFactoryBean`
* `MappingJacksonHttpMessageConverter`
* `MappingJacksonJsonView`
* `MappingJacksonMessageConverter` for JMS

#### Burlap
Burlap is no longer under active development and support will be dropped entirely in the future:
* `BurlapClientInterceptor`
* `BurlapExporter`
* `BurlapProxyFactoryBean`
* `BurlapServiceExporter`
* `SimpleBurlapServiceExporter`

#### Outdated JBoss classes
The following classes are deprecated since they no longer work with current JBoss releases:
* `JBossWorkManagerTaskExecutor`
* `JBossWorkManagerUtils`

#### JAX-WS feature configuration
* `AbstractJaxWsServiceExporter.setWebServiceFeatures(Object[] webServiceFeatures)`
* `JaxWsPortClientInterceptor.setWebServiceFeatures(Object[] webServiceFeatures)`

#### Generic type resolution
Several methods from the `GenericTypeResolver` have been deprecated. For new code the `ResolvableType` class provides a good alternative to `GenericTypeResolver` & `GenericCollectionTypeResolver`:
* `GenericTypeResolver.getTargetType(MethodParameter methodParam)`
* `GenericTypeResolver.resolveType(Type genericType, Map<TypeVariable, Type> map)`
* `GenericTypeResolver.getTypeVariableMap(Class<?> clazz)`

### Default cache key generator
The default `KeyGenerator` used by Spring's cache abstraction has changed from `DefaultKeyGenerator` to `SimpleKeyGenerator`. The new generator does not suffer from key collisions and less likely to cause a cached method to return incorrect results. You will need to configure the deprecated `DefaultKeyGenerator` if you prefer the previous key strategy, or create a custom `KeyGenerator` implementation yourself.

### MVC namespace
The Spring MVC namespace XSD had been updated to correct the casing used for a couple of attributes. When upgrading to `spring-mvc-4.0.xsd`, you should replace `enableMatrixVariables` and `ignoreDefaultModelOnRedirect` with `enable-matrix-variables` and `ignore-default-model-on-redirect` respectively.

### Using Spring's JSP tags with FreeMarker
As of Spring 4.0, Spring's JSP tag library uses specifically declared attribute types, relying on externally applied EL parsing as supported by JSP 2.0+. As a consequence, some attributes that used to accept Object values - e.g. for String EL expressions or Boolean target values - are now specifically declared for the actual target type - e.g. boolean, suggesting a target type for external EL parsing.

Native JSP parsing can handle this change transparently, just requiring a recompile of the JSP pages. However, FreeMarker's JSP tag support cannot handle String values against a boolean target type - e.g. readonly='false' - and requires a change to an actual boolean value - e.g. readonly=false. In case you happened to specify such values as Strings before, please adapt those values to the actual target type.

### Spring MVC Test and Java 6
An issue with compiling Spring MVC Test framework tests with JDK 1.6 has been [identified and fixed](https://jira.springsource.org/browse/SPR-11238) for version 4.0.1.

## Migrating to Spring Framework 3.2
The migration guide for upgrading to Spring 3.2 is available as [Appendix D in the Spring 3.2 reference documentation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#migration-3.2).

## Migrating to Spring Framework 3.1
The migration guide for upgrading to Spring 3.1 is available as [Appendix C in the Spring 3.2 reference documentation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#migration-3.1).