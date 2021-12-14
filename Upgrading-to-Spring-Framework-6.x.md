_This page provides guidance on upgrading to Spring Framework 6.0._


## Upgrading to Version 6.0


### Web Applications

Spring MVC and Spring WebFlux no longer detect controllers based solely on a type-level `@RequestMapping`
annotation. That means interfaced based AOP proxying for web controllers may no longer work. Please,
enable class based proxying for such controllers or otherwise the interface must also have `@Controller`.
See [22154](https://github.com/spring-projects/spring-framework/issues/22154).

