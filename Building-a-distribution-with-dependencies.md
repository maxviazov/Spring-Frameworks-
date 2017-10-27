Sometimes due to corporate restrictions or when working with legacy builds, you can't use Maven or Gradle and have to download dependencies manually. If you're in this boat you can download a Spring Framework distribution zip from https://repo.spring.io including all source and binary jars. Or if you also want external, optional dependencies included, follow these steps:

1. Clone the Spring Framework source tree as described in the [Build from Source](https://github.com/spring-projects/spring-framework/wiki/Build-from-Source).

1. Check out the tag of the version you want, e.g. `git checkout v5.0.1.RELEASE`.

1. Run the `depsZip` gradle task with `./gradlew depsZip`.

1. When the task is complete, inspect the zip file at `build/distributions/spring-framework-${VERSION}-dist-with-deps.zip` that includes all optional and required runtime dependencies.

Keep in mind that _most of Spring Framework's dependencies are optional! Use only the dependencies your application actually needs.

