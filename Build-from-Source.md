_This document describes how to build and import the Spring Framework into an IDE.
You may also be interested to see [[Code Style]] and [[IntelliJ IDEA Editor Settings]]._

The Spring Framework uses a [Gradle](http://gradle.org) build. The instructions below
use [Gradle Wrapper](http://vimeo.com/34436402) from the root of the source tree.
The wrapper script serves as a cross-platform, self-contained bootstrap mechanism
for the build system.

### Before You Start

To build you will need [Git](http://help.github.com/set-up-git-redirect) and
[JDK 8 update 20 or later](http://www.oracle.com/technetwork/java/javase/downloads).
Be sure that your `JAVA_HOME` environment variable points to the `jdk1.8.0` folder
extracted from the JDK download.

### Get the Source Code

```
git clone git@github.com:spring-projects/spring-framework.git
cd spring-framework
```

### Build from the Command Line

To compile, test, build all jars, distribution zips, and docs use:
```
./gradlew build
```

The first time you run the build it may take a while to download Gradle and all build dependencies, as well as to run all tests. Once you've bootstrapped a Gradle distribution and downloaded dependencies, those are cached in your $HOME/.gradle directory.

Gradle has good incremental build support so run without `clean` to keep things snappy. You can also use the "-a" flag and the ":project" prefix to avoid evaluating and building other modules. For example, if iterating over changes in `spring-webmvc`, run with the following to evaluate and build only that module:
```
./gradlew -a :spring-webmvc:test
```

The Gradle daemon eliminates startup overhead. It's enabled by default but sometimes you may need to disable it. For example if building against [JDK 9](https://jdk9.java.net/download/), you may encounter an `Unrecognized VM option` error which halts the build. To avoid that error, add `org.gradle.jvmargs=-XX:MaxMetaspaceSize=1024m -Xmx1024m` to the `gradle.properties` file in your _gradle user home_ directory. See also [GRADLE-3256](https://issues.gradle.org/browse/GRADLE-3256) for details.

To install all Spring Framework jars into your local Maven cache (note that "-x" skips Javadoc generation):
```
./gradlew install -x javadoc
```

### Import Into Your IDE

Ensure JDK 8 is configured properly in the IDE.
Follow instructions for [Eclipse](https://github.com/spring-projects/spring-framework/blob/master/import-into-eclipse.md) and [IntelliJ IDEA](https://github.com/spring-projects/spring-framework/blob/master/import-into-idea.md).
