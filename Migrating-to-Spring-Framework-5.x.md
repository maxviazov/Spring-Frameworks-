Note that the 5.x generation is currently in the Milestone phase; please check out the [Roadmap page on JIRA](https://jira.spring.io/browse/SPR/?selectedTab=com.atlassian.jira.jira-projects-plugin:roadmap-panel) for more details on upcoming versions.

## Migrating to Spring Framework 5.0

For a general overview of new features, refer to [[What's New in the Spring Framework]].

### Baseline update

Spring Framework 5.0 requires Java SE 8 or above, since its entire codebase is now based on Java 8 source code level.
The project offers full compatibility with JDK 9 as of July 2016.

Java EE 7 API level is required in Spring's corresponding modules now:

* Servlet 3.1 (Servlet 2.5 runtime compatibility has been dropped)
* JMS 2.0
* JPA 2.1
* Bean Validation 1.1

### Servers

* Tomcat 8.5+
* Jetty 9.4+
* WildFly 10+
* with the addition of Netty 4.1 and Undertow 1.4 for the Web Reactive module

### Removed Packages, Classes and Methods

* Package `mock.staticmock` removed from `spring-aspects` module.
  * No support for `AnnotationDrivenStaticEntityMockingControl` anymore.
* Packages `web.view.tiles2` and `orm.hibernate3/hibernate4` dropped.
  * Minimum requirement: Tiles 3 and Hibernate 5 now.
* Many deprecated classes and methods removed across the codebase.
  * A few compromises made for commonly used methods in the ecosystem.

### Dropped support

The Spring Framework no longer supports: Portlet, Velocity, JasperReports, XMLBeans, JDO,
Guava (replaced by the Caffeine support).
If those are critical to your project, you should stay on Spring Framework 4.3.x (supported until 2019).

### Libraries

* Jackson 2.6+
* EhCache 2.10+ / 3.0 GA
* Hibernate 5.0+
* JDBC 4.0+
* XmlUnit 2.x+
* OkHttp 3.x+
* Netty 4.1+
