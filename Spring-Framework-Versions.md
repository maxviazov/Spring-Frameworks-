_This document describes new features, noteworthy changes, and provides guidance on upgrading from earlier versions. If you see anything missing or inaccurate, please submit a pull-request against individual pages, or [create an issue](https://github.com/spring-projects/spring-framework/issues)._

# Supported Versions

- 5.3.x is the upcoming final feature branch of the 5th generation (general availability expected in October 2020), with long-term support to be provided until 2024.
- 5.2.x is the latest production line (GA as of September 2019), actively supported until the end of 2021.
- 5.1.x is the previous production line (September 2018), actively supported until October 2020.
- 5.0.x entered its EOL phase as of Q2 2019. As a courtesy to 5.0.x users, further maintenance is provided until October 2020.
- 4.3.x is the last feature branch of the 4th generation, with active maintenance until October 2020. _4.3.x will reach its official EOL (end-of-life) on December 31st, 2020._
- _3.2.x is EOL (end-of-life) as of December 31st, 2016. No further maintenance releases and security patches are planned in that line. Please migrate to 4.3 or 5.x at your earliest convenience!_

At this point, we recommend upgrading to the latest Spring Framework 5.2.x release from Maven Central.

# JDK Version Range

- Spring Framework 5.3.x: JDK 8-17 (expected)
- Spring Framework 5.2.x: JDK 8-15 (expected)
- Spring Framework 5.1.x: JDK 8-12
- Spring Framework 5.0.x: JDK 8-10
- Spring Framework 4.3.x: JDK 6-8

We fully test and support Spring on Long-Term Support (LTS) releases of the JDK, i.e. currently JDK 8 and 11 (both with a lifetime until 2023) and expecting JDK 17 (to be released in late 2021). Additionally, there is support for intermediate releases such as JDK 9/10/12/13/14 and the upcoming JDK 15/16 on a best-effort basis, meaning that we accept bug reports and will try to address them as far as technically possible but won't provide any service level guarantees.

_Please upgrade to Spring Framework 5.1+ (and the corresponding Spring Boot 2.1+) for JDK 11+ support, as the common Long-Term Support migration path from JDK 8. No earlier Spring versions are officially supported on JDK 11, in particular not with JDK 11 bytecode level. Note that third-party components might not fully support JDK 11 yet, so you are likely to be limited in your full-stack options._

# What's New

- [[5th generation|What's New in Spring Framework 5.x]] and [[Spring Framework 5 FAQ]]
- [4th generation](https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/htmlsingle/#spring-whats-new) (4.3.x reference)

# Upgrade Considerations

- [[Upgrading to Spring Framework 5.0, 5.1, 5.2 and 5.3|Upgrading to Spring Framework 5.x]]
- [[Upgrading to Spring Framework 4.3|Upgrading to Spring-Framework 4.x]]