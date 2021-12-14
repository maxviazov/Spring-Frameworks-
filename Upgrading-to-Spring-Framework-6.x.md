_This page provides guidance on upgrading to Spring Framework 6.0._


## Upgrading to Version 6.0


### Web Applications

Spring MVC and Spring WebFlux no longer detect controllers based solely on a type-level `@RequestMapping`
annotation. That means interfaced based AOP proxying for web controllers may no longer work. Please,
enable class based proxying for such controllers or otherwise the interface must also have `@Controller`.
See [22154](https://github.com/spring-projects/spring-framework/issues/22154).

`HttpMethod` is a class and no longer an enum. Though the public API has been maintained, some 
migration might be necessary (i.e. change from `EnumSet<HttpMethod>` to `Set<HttpMethod>`, use `if 
else` instead of `switch`). For the rationale behind this decision, see 
[27697](https://github.com/spring-projects/spring-framework/issues/27697).
