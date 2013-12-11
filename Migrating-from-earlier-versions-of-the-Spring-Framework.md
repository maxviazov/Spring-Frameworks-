This page discusses what what users will want to know when upgrading from earlier version of this Spring Framework. Previously, migration guides were included as an Appendix to the reference documentation. Starting with Spring Framework 4.0, we will be exclusively using this WIKI page for upgrade information.

If you find any issues that are not covered by this guide please raise a [JIRA](http://jira.springsource.org) or submit a pull-request against this page.


## Migrating to Spring Framework 4.0
In this section we discuss what users will want to know when upgrading to Spring Framework 4.0. For a general overview of features, please read [New Features and Enhancements in Spring Framework 4.0](http://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/htmlsingle/#new-in-4.0) from the reference documentation.

### JDK 6
Spring Framework 4.0 requires Java SE 6.0 or above. If you are migrating from an older version of Java you will need to update your JDK. Java 7 and 8 are fully supported by Spring.

### Java EE 6
If you deploy your Spring application to a Java EE server, you should ensure that it is certified for Java EE 6 or above. Specifically the JPA 2.0+ and Servlet 3.0+ specifications should be used if possible. It is still possible to deploy a Spring Framework 4.0 application to a Servlet 2.5 container, however, some features may not be available.

### Default cache key generator
The default `KeyGenerator` used by Spring's cache abstraction has changed from `DefaultKeyGenerator` to `SimpleKeyGenerator`. The new generator does not suffer from key collisions and less likely to cause a cached method to return incorrect results. You will need to configure `DefaultKeyGenerator` if you prefer the previous implementation. 

### MVC Namespace
The Spring MVC namespace XSD had been updated to correct the casing used for a couple of attributes. When upgrading you should replace `enableMatrixVariables` and `ignoreDefaultModelOnRedirect` with `enable-matrix-variables` and `ignore-default-model-on-redirect` respectively.

### Dependency Updates
The following dependencies updates are required for Spring Framework 4.0:

#### Containers
* Oracle WebLogic 7+ (up to and including v10)
* AOP weaving is now supported for Glassfish 3 & 4
* `TomcatInstrumentableClassLoader` requires Tomcat 6.0+

#### Specifications
* JPA 2.0
* Servlet 3.0 (2.5 supported for deployment)
* JSF 2.0

#### Libraries
* Joda Time 2.0 or above
* Bean Validation 1.0 (with 1.1 required for some features and special support for Hibernate Validator 4.3 and 5.0)
* EhCache 2.1 (with 2.5+ recommended)
* JCache 0.11 is now supported
* Quartx v1.8 - v2.2 is now supported (2.2+ recommended)
* Jackson 1.8 (2.0 recommended)
* Hibernate 3.6 (4.6 recommended)
* JDO 3.0
* XStream 1.4
* Hessian 4.0
* Apache POI 3.5

### Deprecated code
The following classes and methods have been deprecated in Spring Framework 4.0. These will be removed at a future date so please check the Javadoc and migrate to the suggested alternatives:

#### Jackson v1
All Jackson v1 support is deprecated in favor of Jackson v2:
* `MappingJacksonMessageConverter`
* `JacksonObjectMapperFactoryBean`
* `MappingJacksonHttpMessageConverter`

#### Generic Types
Several methods from the `GenericTypeResolver` have been deprecated. For new code the `ResolvableType` class provides a good alternative to `GenericTypeResolver` & `GenericCollectionTypeResolver`:
* `GenericTypeResolver.getTargetType(MethodParameter methodParam)`
* `GenericTypeResolver.resolveType(Type genericType, Map<TypeVariable, Type> map)`
* `GenericTypeResolver.getTypeVariableMap(Class<?> clazz)`

#### Burlap
Burlap is no longer under active development and support will be dropped entirely in the future:
* `BurlapClientInterceptor`
* `BurlapExporter`
* `BurlapProxyFactoryBean`
* `BurlapServiceExporter`
* `SimpleBurlapServiceExporter`

#### Outdated JBoss Classes
The following classes are deprecated since there no longer work with current JBoss releases:
* `JBossWorkManagerTaskExecutor`
* `JBossWorkManagerUtils`

#### Miscellaneous deprecations 
* `AbstractJaxWsServiceExporter.setWebServiceFeatures(Object[] webServiceFeatures)`
* `JaxWsPortClientInterceptor.setWebServiceFeatures(Object[] webServiceFeatures)`


## Migrating to Spring Framework 3.2
The migration guide for upgrading to Spring 3.2 is available as [Appendix D in the Spring 3.2 reference documentation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#migration-3.2).


## Migrating to Spring Framework 3.1
The migration guide for upgrading to Spring 3.1 is available as [Appendix C in the Spring 3.2 reference documentation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#migration-3.1).

