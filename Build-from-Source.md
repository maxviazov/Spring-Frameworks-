_This document describes how to build the Spring Framework from the command line
and how to import the Spring Framework projects into an IDE. You may also be
interested to see [[Code Style]] and [[IntelliJ IDEA Editor Settings]]._

The Spring Framework uses a [Gradle](https://gradle.org) build. The instructions below
use the [Gradle Wrapper](https://vimeo.com/34436402) from the root of the source tree.
The wrapper script serves as a cross-platform, self-contained bootstrap mechanism
for the build system.

### Before You Start

To build you will need [Git](https://help.github.com/set-up-git-redirect) and
[JDK 17](https://adoptium.net/). Be sure that your `JAVA_HOME`
environment variable points to the `jdk17` folder extracted from the JDK download.

For users of SDKMAN, Spring Framework provides `.sdkmanrc` files that set up your JDK correctly.
Simply use `sdk env` to do so.
This command is also available in the 5.3 branch, which uses JDK 8.


### Get the Source Code

```shell
git clone git@github.com:spring-projects/spring-framework.git
cd spring-framework
```

### Build from the Command Line

To compile, test, and build all jars, distribution zips, and docs use:

```shell
./gradlew build
```

The first time you run the build it may take a while to download Gradle and all build dependencies, as well as to run all tests. Once you've bootstrapped a Gradle distribution and downloaded dependencies, those are cached in your $HOME/.gradle directory.

Gradle has good incremental build support, so run without `clean` to keep things snappy. You can also use the `-a` flag and the `:project` prefix to avoid evaluating and building other modules. For example, if iterating over changes in `spring-webmvc`, run with the following to evaluate and build only that module:

```shell
./gradlew -a :spring-webmvc:test
```

### Install in local Maven repository

To install all Spring Framework jars in your local Maven repository, use the following.

Note that the `-x ...` arguments skip the generation of documentation.

```shell
./gradlew publishToMavenLocal -x api -x asciidoctor -x asciidoctorPdf
```

If you are building a previous version of the framework (for example, Spring Framework 5.1.x), use:

```shell
./gradlew install -x javadoc
```

### Import into your IDE

Ensure JDK 17 is configured properly in the IDE.
Follow instructions for [Eclipse](https://github.com/spring-projects/spring-framework/blob/master/import-into-eclipse.md) and [IntelliJ IDEA](https://github.com/spring-projects/spring-framework/blob/master/import-into-idea.md).
