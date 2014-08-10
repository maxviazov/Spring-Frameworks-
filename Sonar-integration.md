## Introduction

This document defines the quality profile the Spring Framework is using for Sonar. It is primarily intended as a revision history of the rules the team has decided to enable (or disable) and why

## Quality profile

The `Spring Framework` quality profile is based on the standard `Sonar Way` profile. Note that no findbugs-related rule can be enabled as Java8 support is not there yet.

The `Sonar Way` brings by 114 rules by default.

### Disabled rules

Theres are the rules that we have disabled:

* _Right curly brace and next "else", "catch" and "finally" keywords should be located on the same line_ as our [Spring Framework Code Style](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Code-Style) uses a different style
* _Useless parentheses around expressions should be removed to prevent any misunderstanding_ as we actually use such extra parantheses, especially with [ternary operatops](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Code-Style#ternary-operator)
* _Tabulation characters should not be used_ as we do ask our code to use tabs and not spaces
* _Throwable and Error classes should not be caught_ as framework code requires such arrangement in many places
* _Constant names should comply with a naming convention_ basically states that any `public static final` field is a constant. We address this specifically in [constant names](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Code-Style#constant-names)