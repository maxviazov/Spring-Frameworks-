_This page provides guidance on upgrading to Spring Framework 6.0._

## Upgrading to Version 6.0

### Core Container

The JSR-330 based `@Inject` annotation is to be found in `jakarta.inject` now. The corresponding JSR-250 based
annotations `@PostConstruct` and `@PreDestroy` are to be found in `jakarta.annotation`. For the time being,
Spring keeps detecting their `javax` equivalents as well, covering common use in pre-compiled binaries.

The core container performs basic bean property determination without `java.beans.Introspector` by default.
For full backwards compatibility with 5.3.x in case of sophisticated JavaBeans usage, specify the following
content in a `META-INF/spring.factories` file which enables 5.3-style full `java.beans.Introspector` usage:
`org.springframework.beans.BeanInfoFactory=org.springframework.beans.ExtendedBeanInfoFactory`

When staying on 5.3.x for the time being, you may enforce forward compatibility with 6.0-style property
determination (and better introspection performance!) through a custom `META-INF/spring.factories` file:
`org.springframework.beans.BeanInfoFactory=org.springframework.beans.SimpleBeanInfoFactory`

`ListenableFuture` has been deprecated in favor of `CompletableFuture`. 
See [27780](https://github.com/spring-projects/spring-framework/issues/27780).

`SimpleEvaluationContext` disables array allocations now, aligned with regular constructor resolution.

### Data Access and Transactions

Due to the Jakarta EE migration, make sure to upgrade to Hibernate ORM 5.6.x with the `hibernate-core-jakarta`
artifact, alongside switching your `javax.persistence` imports to `jakarta.persistence`.

Alternatively, consider migrating to Hibernate ORM 6.1 right away (exclusively based on `jakarta.persistence`)
which is the Hibernate version that Spring Boot 3.0 comes with.

The corresponding Hibernate Validator generation is 7.0.x, based on `jakarta.validation` (Jakarta EE 9).
You may also choose to upgrade to Hibernate Validator 8.0 right away (based on Jakarta EE 10).

### Web Applications

Due to the Jakarta EE migration, make sure to upgrade to Tomcat 10, Jetty 11, or Undertow 2.2.14 with the
`undertow-servlet-jakarta` artifact, alongside switching your `javax.servlet` imports to `jakarta.servlet`.

Several outdated Servlet-based integrations have been dropped: e.g. Commons FileUpload and Tiles, as well
as FreeMarker JSP support. We recommend `StandardServletMultipartResolver` for multipart file uploads
and regular FreeMarker template views if needed, and a general focus on REST-oriented web architectures.

Spring MVC and Spring WebFlux no longer detect controllers based solely on a type-level `@RequestMapping`
annotation. That means interfaced based AOP proxying for web controllers may no longer work. Please,
enable class based proxying for such controllers or otherwise the interface must also have `@Controller`,
see [22154](https://github.com/spring-projects/spring-framework/issues/22154).

`HttpMethod` is a class and no longer an enum. Though the public API has been maintained, some 
migration might be necessary (i.e. change from `EnumSet<HttpMethod>` to `Set<HttpMethod>`, use `if 
else` instead of `switch`). For the rationale behind this decision, see 
[27697](https://github.com/spring-projects/spring-framework/issues/27697).

The Kotlin extension function to `WebTestClient.ResponseSpec::expectBody` now returns the Java `BodySpec`
type, and no longer uses the workaround type `KotlinBodySpec`.Spring 6.0 uses Kotlin 1.6, which fixed the
bug that needed this workaround ([KT-5464](https://youtrack.jetbrains.com/issue/KT-5464)).
This means that `consumeWith` is not longer available.

`RestTemplate`, or rather the `HttpComponentsClientHttpRequestFactory`, now requires Apache HttpClient 5.