# Work In Progress

This document was introduced in conjunction with the release of Spring
Framework 4.2; however, this document is still a _work in progress_. As such,
you can expect to see multiple updates throughout the course of the 4.2.x
timeline.

# Overview

Over the years, the Spring Framework has continually evolved its support for
annotations, _meta-annotations_, and _composed annotations_. This document is
intended to aid developers (both end users of Spring as well as developers of
the Spring Framework and Spring portfolio projects) in the development and use
of annotations with Spring.

## Goals of this Document

The primary goals of this document include explanations of the following:

* How to use annotations with Spring.
* How to develop annotations for use with Spring.
* How Spring _finds_ annotations (i.e., how Spring's annotation search
  algorithms work).

## Non-goals of this Document

This document does not aim to explain the semantics or configuration options
for particular annotations in the Spring Framework. For details on a particular
annotation, developers are encouraged to consult the corresponding Javadoc or
applicable sections of the reference manual.

# Terminology

## Meta-Annotations

A _**meta-annotation**_ is an annotation that is declared on another
annotation. An annotation is therefore _meta-annotated_ if it is annotated with
another annotation. For example, any annotation that is declared to be
_documented_ is meta-annotated with `@Documented` from the
`java.lang.annotation` package.

## Composed Annotations

A _**composed annotation**_ is an annotation that is _meta-annotated_ with one
or more annotations with the intent of combining the behavior associated with
those meta-annotations into a single custom annotation. For example, an
annotation named `@TransactionalService` that is meta-annotated with Spring's
`@Transactional` and `@Service` annotations is a composed annotation that
combines the semantics of `@Transactional` and `@Service`.

## Annotation Presence

The terms _**directly present**_, _**indirectly present**_, and _**present**_
have the same meanings as defined in the class-level Javadoc for
`java.lang.reflect.AnnotatedElement` in Java 8.

In Spring, an annotation is considered to be _**meta-present**_ on an element
if the annotation is declared as a meta-annotation on some other annotation
which is _present_ on the element. For example, given the aforementioned
`@TransactionalService`, we would say that `@Transactional` is _meta-present_
on any class that is directly annotated with `@TransactionalService`.

## Attribute Aliases and Overrides

An _**attribute alias**_ is an alias from one annotation attribute to another
annotation attribute. Attributes within a set of aliases can be used
interchangeably and are treated as equivalent. Attribute aliases can be
categorized as follows.

1. **Explicit Aliases**: if two attributes in one annotation are declared as
   aliases for each other via `@AliasFor`, they are _explicit aliases_.
2. **Implicit Aliases**: if two or more attributes in one annotation are
   declared as explicit overrides for the same attribute in a meta-annotation
   via `@AliasFor`, they are _implicit aliases_.
3. **Transitive Implicit Aliases**: given two or more attributes in one
   annotation that are declared as explicit overrides for attributes in
   meta-annotations via `@AliasFor`, if the attributes _effectively_ override
   the same attribute in a meta-annotation following the
   [law of transitivity](https://en.wikipedia.org/wiki/Transitive_relation),
   they are _transitive implicit aliases_.

An _**attribute override**_ is an annotation attribute that _overrides_ (or
_shadows_) an annotation attribute in a meta-annotation. Attribute overrides
can be categorized as follows.

1. **Implicit Overrides**: given attribute `A` in annotation `@One` and
   attribute `A` in annotation `@Two`, if `@One` is meta-annotated with `@Two`,
   then attribute `A` in annotation `@One` is an _implicit override_ for
   attribute `A` in annotation `@Two` based solely on a naming convention (i.e.,
   both attributes are named `A`).
2. **Explicit Overrides**: if attribute `A` is declared as an alias for
   attribute `B` in a meta-annotation via `@AliasFor`, then `A` is an _explicit
   override_ for `B`.
3. **Transitive Explicit Overrides**: if attribute `A` in annotation `@One` is
   an explicit override for attribute `B` in annotation `@Two` and `B` is an
   explicit override for attribute `C` in annotation `@Three`, then `A` is a
   _transitive explicit override_ for `C` following the
   [law of transitivity](https://en.wikipedia.org/wiki/Transitive_relation).


# Declaring attribute aliases with @AliasFor

Spring Framework 4.2 introduced first-class support for declaring and looking
up aliases for annotation attributes. The `@AliasFor` annotation can be used to
declare a pair of aliased attributes _within_ a single annotation or to declare
an alias from one attribute in a custom composed annotation to an attribute in
a meta-annotation.

For example, `@ContextConfiguration` from the `spring-test` module is now
declared as follows:

    public @interface ContextConfiguration {

        @AliasFor("locations")
        String[] value() default {};
        
        @AliasFor("value")
        String[] locations() default {};
        
        // ...
    }

Similarly, _composed annotations_ that override attributes from
meta-annotations can use `@AliasFor` for fine-grained control over exactly
which attributes are overridden within an annotation hierarchy. In fact, it is
even possible to declare an alias for the `value` attribute of a
meta-annotation.

For example, one can develop a composed annotation with a custom attribute
override as follows.

    @ContextConfiguration
    public @interface MyTestConfig {

        @AliasFor(annotation = ContextConfiguration.class, attribute = "value")
        String[] xmlFiles();
    
        // ...
    }


# Appendix

## Annotations using @AliasFor

As of Spring Framework 4.2, the following annotations from core Spring use
`@AliasFor` to declare aliases for their `value` attributes.

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

----

# Topics yet to be Covered

* Document the general search algorithm(s) for annotations and meta-annotations on classes, interfaces, methods, fields, parameters, and annotations.
  * What happens if an annotation is _present_ on an element both locally and as a meta-annotation?
  * How does the presence of `@Inherited` on an annotation (including custom composed annotations) affect the search algorithm?
* Document support for annotation attribute aliases configured via `@AliasFor`.
  * What happens if an attribute _and_ its alias are declared in an annotation instance (with the same value or with different values)?
    * Typically an `AnnotationConfigurationException` will be thrown.
* Document support for _composed annotations_.
* Document support for meta-annotation attribute overrides in composed annotations.
  * Document the algorithm used when looking up attributes, specifically explaining:
    * implicit mapping based on naming convention (i.e., composed annotation declares an attribute with the exact same name and type as declared in the _overridden_ meta-annotation)
    * explicit mapping using `@AliasFor`
  * What happens if an attribute _and_ one of its aliases are declared somewhere within the annotation _hierarchy_? Which one takes precedence?
  * In general, how are conflicts involving annotation attributes resolved?
* Document the special handling of the `value` attribute for `@Component` and `@Qualifier`.
