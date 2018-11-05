_This document describes new features, noteworthy changes, and provides guidance on upgrading from earlier versions. If you see anything missing or inaccurate, please submit a pull-request against individual pages, or create a [ticket in JIRA](https://jira.spring.io/browse/SPR)._

# Supported Versions

- 5.1.x is the latest and recommended line (to be superseded by 5.2.x in mid 2019)
- 5.0.x has been superseded by 5.1.x, but is supported for Boot 2.0's lifetime still (~ March 2019)
- 4.3.x is the last branch of the 4th generation, it's got an extended support life until 2020 so you can migrate your applications to the latest generation safely
- 3.2.x is EOL, no further maintenance releases are planned in that line

We strongly recommend upgrading to the latest Spring Framework 5.1.x or 4.3.x release from Maven Central.

# JDK Version Range

- Spring Framework 5.1: JDK 8-12
- Spring Framework 5.0: JDK 8-10
- Spring Framework 4.3: JDK 6-8

We fully test and support Spring on Long-Term Support (LTS) releases of the JDK, i.e. currently JDK 8 and 11 (both expected until 2023). Additionally, there is basic support for intermediate releases such as JDK 9/10 or the upcoming JDK 12 on a best-effort basis, meaning that we accept bug reports and will try to address them as far as technically possible but won't provide any service level guarantees.

_Please upgrade to Spring Framework 5.1 (and the corresponding Spring Boot 2.1) for JDK 11 support, as the common Long-Term Support migration path from JDK 8. No earlier Spring versions are officially supported on JDK 11, in particular not with JDK 11 bytecode level._

# What's New

- [[5th generation|What's New in Spring Framework 5.x]] and [[Spring Framework 5 FAQ]]
- [4th generation](https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/htmlsingle/#spring-whats-new) (4.3.x reference)
- [3rd generation](http://docs.spring.io/spring-framework/docs/3.2.x/spring-framework-reference/htmlsingle/#spring-whats-new) (3.2.x reference)

# Upgrading

- [[Spring Framework 5.x|Upgrading to Spring Framework 5.x]]
- [[Spring Framework 4.3|Upgrading to Spring-Framework 4.x]]
- [[Spring Framework 3.2|Upgrading to Spring-Framework 3.x]]