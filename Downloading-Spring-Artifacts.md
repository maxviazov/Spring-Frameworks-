The Spring Framework is modular and publishes 20+ different jars:
````
spring-aop           spring-context-indexer  spring-instrument  spring-orm   spring-webflux  
spring-aspects       spring-context-support  spring-jcl         spring-oxm   spring-webmvc  
spring-beans         spring-core             spring-jdbc        spring-test  spring-websocket  
spring-beans-groovy  spring-expression       spring-jms         spring-tx  
spring-context       spring-framework-bom    spring-messaging   spring-web  
````
Some modules are interdependent. For example `spring-context` depends on `spring-beans` which in turn depends on `spring-core`. There are no required external dependencies although each module has optional dependencies and some of those may be required depending on what functionality is used.

There is no "spring-all" jar.

## Maven Central

The Spring Framework publishes GA (general availability) versions to [Maven Central](http://search.maven.org) which is automatically searched when using Maven, so just add the dependencies to your project's POM:
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>4.0.3.RELEASE</version>
</dependency>
```

## Spring Repository

Snapshot, milestone, and RC (release candidate) versions are published to the [Spring repository](http://repo.spring.io/), and so are GA releases as well.

### Snapshots

Add the following to resolve snapshot versions, e.g. `5.0.2.BUILD-SNAPSHOT`:
```xml
<repository>
    <id>repository.spring.snapshot</id>
    <name>Spring Snapshot Repository</name>
    <url>http://repo.spring.io/snapshot</url>
</repository>

...

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.0.2.BUILD-SNAPSHOT</version>
</dependency>
```

### Milestones and Release Candidates

Add the following to resolve milestone and RC versions, e.g. `5.1.0.M1` or `5.1.0.RC1`:
```xml
<repository>
    <id>repository.spring.milestone</id>
    <name>Spring Milestone Repository</name>
    <url>http://repo.spring.io/milestone</url>
</repository>

...

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.1.0.M1</version>
</dependency>
```

There is also `http://repo.spring.io/release` for GA releases.

## Downloading a Distribution

If for whatever reason you are not using a build system with dependency management capabilities, you can download Spring Framework _distribution zips_ from the Spring repository at <http://repo.spring.io>. These distributions contain all source and binary jar files, as well as Javadoc and reference documentation, but _do not_ contain external dependencies! 

To create a distribution with all dependencies locally you can build from source, see [[Build zip with dependencies]] for details.
