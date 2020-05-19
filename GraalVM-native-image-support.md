This wiki page is intended to provide an up-to-date status of Spring Framework support for [GraalVM](https://www.graalvm.org/) native images.

# GraalVM

One important thing to have in mind regarding to GraalVM is that it is an umbrella project with a wide scope and multiple components. **While GraalVM is now GA, GraalVM native image feature which allows ahead-of-time compilation of Java applications into executable images is only available as an early adopter plugin, so we don't consider it production ready yet**. 2 versions of GraalVM are provided: the community version which is free and the EE version which is not.

GraalVM native image allows to compile Spring applications to native executable with very fast startup (less than 100ms) with low memory consumption (usually 5x less than its regular JVM equivalent) at the price of lower throughput and various [limitations](https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md). **[Reflection](https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md#reflection) and [dynamic proxies](https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md#dynamic-proxy) are supported but need to be configured manually or via dedicated support**. It also allows to produce small container images.

# Support of native images at Spring Framework level

Spring Framework provides [initial support for GraalVM native images](https://github.com/spring-projects/spring-framework/issues/21529) as of 5.1.

But various issues on GraalVM during its RC phase prevented to use it correctly, so Spring Framework 5.2 development cycle has been mainly dedicated to reporting these issues by collaborating with GraalVM development team. Since GA, GraalVM almost (see known GraalVM issues impacting Spring) allows to run Spring Framework applications with the relevant reflection configuration and command line arguments.

Working toward GraalVM native image support without requiring additional configuration or workaround is one of the themes of upcoming Spring Framework 5.3. The main missing piece for considering GraalVM as a suitable deployment target for Spring applications is providing custom GraalVM `Feature` implementation at Spring Framework level to automatically register classes used in the dependency mechanism or Spring factories, see [the related issue #22968](https://github.com/spring-projects/spring-framework/issues/22968) for more details.

Support at tooling level is also likely to be required to make it usable by end users (passing the right command-line arguments to `native-image`, packaging).

## Experimental support

The [spring-graalvm-native](https://github.com/spring-projects-experimental/spring-graalvm-native) experimental project, created by Andy Clement, shows how it is possible to run a Spring Boot application out of the box as a GraalVM native image. It could be used as a basis for a potential upcoming official support.

# Support in integrated technologies

 * Netty supports GraalVM native image via [builtin substitution classes](https://github.com/netty/netty/issues/8959)
 * Tomcat supports GraalVM native image via adaptive code paths