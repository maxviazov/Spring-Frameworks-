_This document describes how to access Spring Framework artifacts. For snippets of POM configuration go to Maven Central or Spring Repositories. For more in-depth information about Spring repositories see the [[Spring Artifactory]] page._

The Spring Framework is modular and publishes 20+ different jars:

````
spring-aop           spring-context-indexer  spring-instrument  spring-orm   spring-webflux  
spring-aspects       spring-context-support  spring-jcl         spring-oxm   spring-webmvc  
spring-beans         spring-core             spring-jdbc        spring-test  spring-websocket  
                     spring-expression       spring-jms         spring-tx  
spring-context                               spring-messaging   spring-web  
````

Some modules are interdependent. For example `spring-context` depends on `spring-beans` which in turn depends on `spring-core`. There are no required external dependencies although each module has optional dependencies and some of those may be required depending on what functionality the application needs.

There is no one "spring-all" jar that includes all sources.

## Maven Central

The Spring Framework publishes GA (general availability) versions to [Maven Central](https://search.maven.org) which is automatically searched when using Maven, so just add the dependencies to your project's POM:

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.9</version>
</dependency>
```

## Spring Repositories

Snapshot, milestone, and release candidate versions are published to an [Artifactory](https://www.jfrog.com/artifactory/) instance hosted by [JFrog](https://www.jfrog.com). You can use the Web UI at https://repo.spring.io to browse the Spring Artifactory, or go directly to one of the repositories listed below.

### Snapshots

Add the following to resolve snapshot versions – for example, `5.3.10-SNAPSHOT`:

```xml
<repository>
    <id>repository.spring.snapshot</id>
    <name>Spring Snapshot Repository</name>
    <url>https://repo.spring.io/snapshot</url>
</repository>

...

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.10-SNAPSHOT</version>
</dependency>
```

### Milestones and Release Candidates

Add the following to resolve milestone and RC versions, e.g. `5.3.0-M1` or `5.3.0-RC1`:

```xml
<repository>
    <id>repository.spring.milestone</id>
    <name>Spring Milestone Repository</name>
    <url>https://repo.spring.io/milestone</url>
</repository>

...

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.0-M1</version>
</dependency>
```

### Releases

You can also resolve GA versions of Spring Framework artifacts against `https://repo.spring.io/release`.

For more in-depth information about Spring repositories, see the [[Spring Artifactory]] page.


## Downloading a Distribution

If for whatever reason you are not using a build system with dependency management capabilities, you can download Spring Framework _distribution zips_ from the Spring repository at <https://repo.spring.io>. These distributions contain all source and binary jar files, as well as Javadoc and reference documentation, but _do not_ contain external dependencies! 

To create a distribution with all dependencies locally you can build from source, see [[Build Zip with Dependencies]] for details.
