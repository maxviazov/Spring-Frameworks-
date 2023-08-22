_This document describes how to access Spring Framework artifacts. For snippets of POM configuration go to Maven Central or Spring Repositories. For more in-depth information about Spring repositories see the [[Spring Artifactory]] page._

The Spring Framework is modular and publishes 20+ different jars:

````
spring-aop      spring-context-indexer  spring-instrument  spring-orm    spring-web
spring-aspects  spring-context-support  spring-jcl         spring-oxm    spring-webflux
spring-beans    spring-core             spring-jdbc        spring-r2dbc  spring-webmvc
spring-context  spring-expression       spring-jms         spring-test   spring-websocket
                                        spring-messaging   spring-tx  
````

Some modules are interdependent. For example `spring-context` depends on `spring-beans` which in turn depends on `spring-core`. There are no required external dependencies although each module has optional dependencies and some of those may be required depending on what functionality the application needs.

There is no single "spring-all" jar that includes all modules.

## Maven Central

The Spring Framework publishes GA (general availability) versions to [Maven Central](https://central.sonatype.com/) which is automatically searched when using Maven or Gradle, so just add the dependencies to your project's build script:

### Maven

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.0.10</version>
</dependency>
```

### Gradle

```groovy
implementation 'org.springframework:spring-context:6.0.10'
```

## Spring Repositories

Snapshot, milestone, and release candidate versions are published to an [Artifactory](https://www.jfrog.com/artifactory/) instance hosted by [JFrog](https://www.jfrog.com). You can use the Web UI at https://repo.spring.io to browse the Spring Artifactory, or go directly to one of the repositories listed below.

### Snapshots

Add the following to resolve snapshot versions – for example, `6.1.0-SNAPSHOT`:

#### Maven

```xml
<repositories>
  <repository>
    <id>spring-snapshots</id>
    <name>Spring Snapshots</name>
    <url>https://repo.spring.io/snapshot</url>
    <releases>
      <enabled>false</enabled>
    </releases>
  </repository>
</repositories>
...

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.1.0-SNAPSHOT</version>
</dependency>
```

#### Gradle

```groovy
repositories {
    mavenCentral()
    maven {
        url "https://repo.spring.io/snapshot"
    }
}

...

dependencies {
    implementation 'org.springframework:spring-context:6.1.0-SNAPSHOT'
}
```

### Milestones and Release Candidates

Add the following to resolve milestone and RC versions – for example, `6.1.0-M2` or `6.1.0-RC1`:

#### Maven

```xml
<repositories>
  <repository>
    <id>spring-milestones</id>
    <name>Spring Milestones</name>
    <url>https://repo.spring.io/milestone</url>
    <snapshots>
      <enabled>false</enabled>
    </snapshots>
  </repository>
</repositories>
...

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.1.0-M2</version>
</dependency>
```

#### Gradle

```groovy
repositories {
    mavenCentral()
    maven {
        url "https://repo.spring.io/milestone"
    }
}

...

dependencies {
    implementation 'org.springframework:spring-context:6.1.0-M2'
}
```

