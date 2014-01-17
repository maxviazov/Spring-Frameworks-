This page provides information when upgrading to newer versions of the Spring Framework. If you find items not covered yet, please raise a [ticket in JIRA](http://jira.springsource.org) or submit a pull-request against this page.


## Migrating to Spring Framework 4.0
For a general overview of new features, refer to [New Features and Enhancements in Spring Framework 4.0](http://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/htmlsingle/#new-in-4.0) in the reference documentation.

### JDK 6
Spring Framework 4.0 requires Java SE 6 or above (specifically, a minimum API level equivalent to JDK 6 update 18, a.k.a. 1.6.0_18, as released in January 2010). If you are migrating from an older version of Java, you will need to update your installation to a recent version of JDK 6 at least. Java 7 and 8 are recommended for use with Spring Framework 4.0, with Java 8 support in stable developer preview state until OpenJDK 8 becomes generally available in March 2014.

### Java EE 6
If you deploy your Spring application to a Java EE server, you should ensure that it is certified for Java EE 6 or above. Of particular importance are the JPA 2.0 and Servlet 3.0 specifications. That said, it is still possible to deploy a Spring Framework 4.0 application to a Servlet 2.5 container (e.g. Google App Engine, WebSphere 7, WebLogic 10.3); however, some Servlet 3.0 based Spring features won't be available.

### Dependency Updates
As of Spring Framework 4.0.1, we declare the following minimum (optional) dependencies as officially supported. Those versions and later are what the Spring team recommends, in particular with respect to providing support for Spring applications that interact with those servers and libaries. Note that earlier versions may still work with Spring to some degree, as long as the fundamental system requirements are met; however, when using older versions, you are on your own from a support perspective.

#### Specifications
* Servlet 3.0 (2.5 supported for deployment)
* JPA 2.0
* Bean Validation 1.0
* JSF 2.0
* JCache 1.0 RC1
* JDO 3.0

#### Servers
* Tomcat 6.0.33 / 7.0.20
* Jetty 7.5
* JBoss AS 6.1
* GlassFish 3.1
* Oracle WebLogic 10.3.4 (with JPA 2.0 patch applied)
* IBM WebSphere 7.0.0.9 (with JPA 2.0 feature pack installed)

#### Libraries
* Joda-Time 2.0
* Hibernate Validator 4.3
* Hibernate 3.6.1 (3.6.6 as of Spring Framework 4.1)
* EhCache 2.4 (2.5 as of Spring Framework 4.1)
* Quartz 1.8.5 (2.1 as of Spring Framework 4.1)
* Jackson 1.8 (2.0 as of Spring Framework 4.1)
* Groovy 1.8
* Hessian 4.0
* XStream 1.4
* Apache POI 3.5
* Apache Velocity 1.7
* Apache Tiles 2.2.2
* Apache Derby 10.6

### Deprecated code
The following classes and methods have been deprecated in Spring Framework 4.0. These will be removed at a future date, so please check the javadoc and migrate to the suggested alternatives:

#### Quartz 1.x
Quartz 1.x support in the `org.springframework.scheduling.support` package is deprecated and will be removed in Spring Framework 4.1, with that package only working with Quartz 2.0+ from then onwards.

#### Jackson 1.x
All Jackson v1 support is deprecated in favor of Jackson v2, and will be removed in Spring Framework 4.1:
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

### Spring MVC Test and Java 6
An issue with compiling Spring MVC Test framework tests with JDK 1.6 has been [identified and fixed](https://jira.springsource.org/browse/SPR-11238) for version 4.0.1.

## Migrating to Spring Framework 3.2
The migration guide for upgrading to Spring 3.2 is available as [Appendix D in the Spring 3.2 reference documentation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#migration-3.2).


## Migrating to Spring Framework 3.1
The migration guide for upgrading to Spring 3.1 is available as [Appendix C in the Spring 3.2 reference documentation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#migration-3.1).
