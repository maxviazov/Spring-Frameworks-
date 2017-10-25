_This document describes how to build the Spring Framework sources locally._

The Spring Framework uses a [Gradle](http://gradle.org) build. The instructions below
use [Gradle Wrapper](http://vimeo.com/34436402) from the root of the source tree.
The wrapper script serves as a cross-platform, self-contained bootstrap mechanism
for the build system.

**Before You Start**

To build you will need [Git](http://help.github.com/set-up-git-redirect) and
[JDK 8 update 20 or later](http://www.oracle.com/technetwork/java/javase/downloads).
Be sure that your `JAVA_HOME` environment variable points to the `jdk1.8.0` folder
extracted from the JDK download.

**Get the Source Code**
```
git clone git@github.com:spring-projects/spring-framework.git
cd spring-framework
```

**Import Into Your IDE**

To import into an IDE, ensure JDK 8 is configured. Then run `./import-into-eclipse.sh`
or read [import-into-idea.md](import-into-idea.md). For IntelliJ please do read the
instructions as a straight-up import will not work.

**Run Gradle Tasks**

To compile, test, build all jars, distribution zips, and docs use:
```
./gradlew build
```

To install all spring-\* jars into your local Maven cache:
```
./gradlew install -x javadoc
```

Discover more commands:
```
./gradlew tasks
```
