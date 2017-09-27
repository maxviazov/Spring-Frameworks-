### What is Spring Framework 5?

Spring Framework 5 is a major version upgrade of the Spring Framework, several years in the making. It introduces a new non-blocking web framework called [Spring WebFlux](https://docs.spring.io/spring-framework/docs/5.0.x/spring-framework-reference/reactive-web.html#webflux) which uses [Reactor](https://projectreactor.io/) to support the [Reactive Streams](https://github.com/reactive-streams/reactive-streams-jvm) API. It also offers a functional programming alternative to annotated controllers, and first-class Kotlin language support. It is based on Java 8 language features, and designed to work with Java 9.

For more details see the [reference documentation](https://docs.spring.io/spring/docs/5.0.0.BUILD-SNAPSHOT/spring-framework-reference/web-reactive.html#spring-webflux), or watch [Spring Framework 5 Themes & Trends](https://www.youtube.com/watch?v=ETFe3KiYwt8) by Juergen Hoeller.

### Will Spring Boot support Spring Framework 5?

Yes, the Spring Boot 2.x line is built on Spring Framework 5. Spring Boot 2.0 is [expected to GA](https://github.com/spring-projects/spring-boot/milestones) after Spring Framework 5.0, aiming for a timeframe around [SpringOne Platform](https://springoneplatform.io). For the latest release check the [spring.io/spring-boot](https://projects.spring.io/spring-boot/) website or [GitHub](https://github.com/spring-projects/spring-boot/milestones).

### Why are we introducing Spring WebFlux?

Blocking threads consume resources. For latency sensitive workloads which need to handle a large number of concurrent requests, the non-blocking async programming model is more efficient. This is particularly relevant for mobile applications and interconnected microservices.

The goal of Spring WebFlux is to offer Spring developers a non-blocking event-loop style programming model similar to [node.js](https://nodejs.org/en/about/). For more details and demos, watch [Servlet vs Reactive Stacks in Five Use Cases](https://www.infoq.com/presentations/servlet-reactive-stack) and [Reactive Web Applications with Spring Framework 5](https://www.youtube.com/watch?v=rdgJ8fOxJhc), both by Rossen Stoyanchev.

### Can I keeping using Spring MVC with Spring Framework 5?

Absolutely, Spring MVC is included alongside the new WebFlux framework in Spring Framework 5. Upgrading to Spring Framework 5 does not require re-writing your applications to use Spring WebFlux. By all means, keep using Spring MVC if you are developing web apps that don't need a non-blocking programming model, or that use blocking JPA or JDBC libraries for persistence.

### What are Mono and Flux?

The WebFlux framework in Spring Framework 5 uses [Reactor](https://projectreactor.io/) as its async foundation. This project provides the core types, [Mono](https://projectreactor.io/docs/core/release/reference/docs/index.html#core-features) to represent a single async value, and [Flux](https://projectreactor.io/docs/core/release/reference/docs/index.html#core-features) to represent a stream of async values. It also provides a library of [operators](https://projectreactor.io/docs/core/release/reference/docs/index.html#which-operator) for manipulating these values. For more information see the [reactor-core](https://github.com/reactor/reactor-core) and the [reactive-streams-commons](https://github.com/reactor/reactive-streams-commons) projects on GitHub

### How do I make all my code non-blocking?

For handlers to be fully non-blocking, you need to use reactive libraries throughout the processing chain, all the way to the persistence layer. Reactive Spring Data libraries are already available for Cassandra, MongoDB, Redis, and Couchbase. JPA and JDBC are inherently blocking APIs. We are still waiting for common ground around non-blocking relational database drivers. Other Spring projects which are already reactive include Spring Security, Spring Vault, and Spring Cloud Stream.

### What if there is no reactive library for my database?

One suggestion for handling a mix of blocking and non-blocking code, would be to use the power of a microservice boundary to separate the blocking backend datastore code from the non blocking front-end API.

### What about interoperability with other Reactive libraries like RxJava?

Reactor uses the same underlying Pub/Sub API as RxJava and [other libraries](https://en.wikipedia.org/wiki/Reactive_Streams#Adoption) built on [Reactive Streams](https://github.com/reactive-streams/reactive-streams-jvm). This is a collaboration between engineers from Kaazing, Lightbend, Netflix, Pivotal, Red Hat, Twitter and many others.

### Can I still write controller methods with annotations?

Yes, both Spring MVC and Spring WebFlux support the same annotation-based programming model with @Controller, @RequestMapping, etc. Instead of taking ownership of the thread and and doing the work immediately, WebFlux controller methods operate on async Request and Response types.

### Can I write controller methods without using annotations?

Yes, for developers who prefer to avoid the magic of annotations and reflection, Spring Framework 5 offers a new [functional API](https://github.com/spring-projects/spring-framework/blob/master/src/docs/asciidoc/web/webflux-functional.adoc) to match routes with handler functions programmatically. This is made possible by the first class function support in Java 8, using lambdas or method references. For more information about how to compose handlers, see the blog post [New in Spring Framework 5: Functional Web Framework](https://spring.io/blog/2016/09/22/new-in-spring-5-functional-web-framework) by Arjen Poutsma.

### On which HTTP containers will the WebFlux framework run?

The WebFlux framework will run on Tomcat, Jetty, Netty, Undertow. Since it is designed to support async programming, the framework does not expose the servlet API, but it does use the non-blocking features of servlet 3.1 containers.

### Will Spring Framework 5 work with Java 6 or Java 7?

No. Spring Framework 5 requires Java 8 or later.

### Will Spring Framework 5 work with the new Java 9 module system?

Yes, Spring Framework 5 will ship with automatic module name entries in the manifests of our Spring Framework 5 jars. The public API surface of the Spring libraries should remain unchanged.

### How do I upgrade to Spring Framework 5?

Please consult this [wiki page](https://github.com/spring-projects/spring-framework/wiki/Migrating-to-Spring-Framework-5.x) for details on migrating to Spring Framework 5.

### What about HTTP Client code?

The [AsyncRestTemplate](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/AsyncRestTemplate.html) has been deprecated in favor of the new [WebClient](https://docs.spring.io/spring-framework/docs/5.0.x/spring-framework-reference/reactive-web.html#webflux-client) which provides a more fluent API, and is capable of both sync and async in one package. RestTemplate itself is not deprecated and there is nothing wrong with using it; the WebClient can be seen as its more modern successor 

### Does Spring Framework 5 support Kotlin?

Yes, Spring Framework 5 officially supports Kotlin. More details are available in the [Kotlin support documentation](https://docs.spring.io/spring-framework/docs/5.0.x/spring-framework-reference/kotlin.html). There are also two great blog posts about Kotlin support in Spring 5. [Introducing Kotlin support in Spring Framework 5](https://spring.io/blog/2017/01/04/introducing-kotlin-support-in-spring-framework-5-0) and [Spring Framework 5 Kotlin APIs, the functional way](https://spring.io/blog/2017/08/01/spring-framework-5-kotlin-apis-the-functional-way), both by Sébastien Deleuze.

### Where should I ask a technical question about Spring Framework 5?

Please post technical questions to StackOverflow, using tags like [spring-webflux](https://stackoverflow.com/questions/tagged/spring-webflux) and [project-reactor](https://stackoverflow.com/questions/tagged/project-reactor).

### I want to contribute / get involved with Spring Framework 5, what should I do?

A great place to start might be our [contributor guidelines](https://github.com/spring-projects/spring-framework/wiki/Contributor-guidelines)