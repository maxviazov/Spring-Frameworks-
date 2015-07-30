# Work In Progress

This document is being introduced in conjunction with the release of
Spring Framework 4.2; however, this document is still a _work in progress_.
As such, you can expect to see multiple updates throughout the course of
the 4.2.x timeline.

# Overview

Over the years, the Spring Framework has continually evolved its support for
annotations, _meta-annotations_, and _composed annotations_. This document
is intended to aid developers (both end users of Spring and developers of
the Spring Framework and Spring portfolio projects) in the development and
use of annotations with Spring.

## Goals of this Document

This document has the following primary goals.

* Explain how to use annotations with Spring.
* Explain how to develop annotations for use with Spring.
* Explain how Spring _finds_ annotations (i.e., how Spring's annotation
  search algorithms work).

## Non-goals of this Document

This document does not aim to explain the semantics or configuration
options for particular annotations in the Spring Framework. For details
on a particular annotation, developers are encouraged to consult the
corresponding Javadoc of applicable sections of the reference manual.

# @AliasFor

Spring Framework 4.2 introduces first-class support for declaring and
looking up aliases for annotation attributes. The new `@AliasFor`
annotation can be used to declare a pair of aliased attributes within
a single annotation or to declare an alias from one attribute in a
custom composed annotation to an attribute in a meta-annotation.

For example, `@ContextConfiguration` from the `spring-test` module
is now declared as follows:

    public @interface ContextConfiguration {

        @AliasFor("locations")
        String[] value() default {};
        
        @AliasFor("value")
        String[] locations() default {};
        
        // ...
    }

Similarly, _composed annotations_ that override attributes from
meta-annotations can now use `@AliasFor` for fine-grained control
over exactly which attributes are overridden within an annotation
hierarchy. In fact, it is now possible to declare an alias for the
`value` attribute of a meta-annotation.

For example, one can now develop a composed annotation with a custom
attribute override as follows.

    @ContextConfiguration
    public @interface MyTestConfig {

        @AliasFor(annotation = ContextConfiguration.class, attribute = "value")
        String[] xmlFiles();
    
        // ...
    }

# Appendix

## Annotations using @AliasFor

- `org.springframework.cache.annotation.Cacheable`
- `org.springframework.cache.annotation.CacheEvict`
- `org.springframework.cache.annotation.CachePut`
- `org.springframework.context.annotation.ComponentScan.Filter`
- `org.springframework.context.annotation.ComponentScan`
- `org.springframework.context.annotation.ImportResource`
- `org.springframework.context.annotation.Scope`
- `org.springframework.context.event.EventListener`
- `org.springframework.jmx.export.annotation.ManagedResource`
- `org.springframework.messaging.handler.annotation.Header`
- `org.springframework.messaging.handler.annotation.Payload`
- `org.springframework.messaging.simp.annotation.SendToUser`
- `org.springframework.test.context.ActiveProfiles`
- `org.springframework.test.context.ContextConfiguration`
- `org.springframework.test.context.jdbc.Sql`
- `org.springframework.test.context.TestExecutionListeners`
- `org.springframework.test.context.TestPropertySource`
- `org.springframework.transaction.annotation.Transactional`
- `org.springframework.transaction.event.TransactionalEventListener`
- `org.springframework.web.bind.annotation.ControllerAdvice`
- `org.springframework.web.bind.annotation.CookieValue`
- `org.springframework.web.bind.annotation.CrossOrigin`
- `org.springframework.web.bind.annotation.MatrixVariable`
- `org.springframework.web.bind.annotation.RequestHeader`
- `org.springframework.web.bind.annotation.RequestMapping`
- `org.springframework.web.bind.annotation.RequestParam`
- `org.springframework.web.bind.annotation.RequestPart`
- `org.springframework.web.bind.annotation.ResponseStatus`
- `org.springframework.web.bind.annotation.SessionAttributes`
- `org.springframework.web.portlet.bind.annotation.ActionMapping`
- `org.springframework.web.portlet.bind.annotation.RenderMapping`
