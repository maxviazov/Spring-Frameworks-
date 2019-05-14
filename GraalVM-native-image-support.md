This wiki page is intended to provide an up-to-date status of Spring Framework support for GraalVM native images.

# GraalVM

One important thing to have in mind regarding to GraalVM is that it is an umbrella project with a wide scope and multiple components. As of May 2019 and the release of GraalVM 19 GA, GraalVM native images functionality (Substrate VM) which allows ahead-of-time compilation of Java applications into executable images is available as an **early adopter plugin**. 2 versions of GraalVM are provided: the community version which is free and the EE version which is not.

GraalVM native image allows to compile Spring applications to native executable with very fast startup (less than 100ms) with low memory consumption (usually 5x less than its regular JVM equivalent) at the price of lower throughput and various [limitations](https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md). [Reflection](https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md#reflection) and [dynamic proxies](https://github.com/oracle/graal/blob/master/substratevm/LIMITATIONS.md#dynamic-proxy) are supported but need to be configured. It also allows to produce small container images.

# Support at Spring level

Spring Framework provides [initial support for GraalVM native images](https://github.com/spring-projects/spring-framework/issues/21529) as of 5.1 but various issues on GraalVM during its RC phase prevented to use it correctly. Since GA, GraalVM allows to run Spring Framework applications with reflection configuration and command line arguments documented in the section.

The main missing piece for considering GraalVM as a suitable deployment target for Spring applications is providing custom `Feature` implementation at Spring Framework level to automatically register classes used in the dependency mechanism or Spring factories, see [the related issue #22968](https://github.com/spring-projects/spring-framework/issues/22968) for more details.

Spring Boot should leverage these Spring Framework capabilities with potentially dedicated support at its level, see the [spring-boot-graal-feature](https://github.com/aclement/spring-boot-graal-feature) experimental project created by Andy Clément.

## Known GraalVM issues impacting Spring
 * [#1196](https://github.com/oracle/graal/issues/1196) Having to delete a class from my project - delay or allow-incomplete-cp options not helping

## Reflection configuration

TODO

## Proxy configuration

TODO

## Command line arguments

TODO

# Support in integrated technologies

 * Netty supports GraalVM native image via [builtin substitution classes](https://github.com/netty/netty/issues/8959)