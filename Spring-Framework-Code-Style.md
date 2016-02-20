## Introduction

This document defines the coding standards for source files in the Spring Framework. It is primarily intended for the Spring Framework team but can be used as a reference by contributors.

The structure of this document is based on the [Google Java Style](http://google-styleguide.googlecode.com/svn/trunk/javaguide.html) reference and is _work in progress_.

## Source File Basics

### File encoding: -1 

Source files must be encoded using `-1`. (see [](https://jira.spring.io/browse/) for a suggestion to move to `UTF-8`)

### Indentation

* Indentation uses _tabs_ (not spaces)
* Unix (LF), not DOS (CRLF) line endings
* Eliminate all trailing whitespace
  * On Linux, Mac, etc.: `find . -type f -name "*.java" -exec perl -p -i -e "s/[ \t]$//g" {} \;`

## Source file structure

A source file consists of the following, in this exact order:

* License
* Package statement
* Import statements
* Exactly one top-level class

Exactly one blank line separates each of the above sections.

### License

Each source file must specify the following license at the very top of the file:

	/*
	 * Copyright 2002-2016 the original author or authors.
	 *
	 * Licensed under the Apache License, Version 2.0 (the "License");
	 * you may not use this file except in compliance with the License.
	 * You may obtain a copy of the License at
	 *
	 *      http://www.apache.org/licenses/LICENSE-2.0
	 *
	 * Unless required by applicable law or agreed to in writing, software
	 * distributed under the License is distributed on an "AS IS" BASIS,
	 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	 * See the License for the specific language governing permissions and
	 * limitations under the License.
	 */

Always check the date range in the license header. For example, if you've modified a file in 2016 whose header still reads:
```   
* Copyright 2002-2013 the original author or authors.
```
Then be sure to update it to 2016 accordingly:
```
* Copyright 2002-2016 the original author or authors.
```

### Import statements

The import statements are structured as follow:

* import `java.*`
* import `javax.*`
* blank line
* import all other imports
* blank line
* import `org.springframework.*`
* blank line
* import static all other imports

Also, static imports should not be used in production code. They should be used in test code, especially for things like `org.junit.Assert`.

### Java source file organization

The following governs how the elements of a source file are organized:

1. static fields
1. normal fields
1. constructors
1. (private) methods called from constructors
1. static factory methods
1. JavaBean properties (i.e., getters and setters)
1. method implementations coming from interfaces
1. private or protected templates that get called from method implementations coming from interfaces
1. other methods
1. `equals`, `hashCode`, and `toString`

Note that private or protected methods called from method implementations should be placed immediately below the methods where they're used. In other words if there 3 interface method implementations with 3 private methods (one used from each), then the order of methods should include 1 interface and 1 private method in sequence, not 3 interface and then 3 private methods at the bottom.

Above all, the organization of the code should feel _natural_.

## Formatting

### Braces

#### Block-like constructs: K&R style

Braces mostly follow the _Kernighan and Ritchie style_ (a.k.a., "Egyptian brackets") for nonempty blocks and block-like constructs:

* No line break before the opening brace but prefixed by a single space
* Line break after the opening brace
* Line break before the closing brace
* Line break after the closing brace if that brace terminates a statement or the body of a method, constructor, or named class with the exception of the `else`, `catch` and `finally` statements that also lead to a line break

Example:

```
return new MyClass() {
	@Override 
	public void method() {
		if (condition()) {
			something();
		}
		else {
			try {
				alternative();
			} 
			catch (ProblemException ex) {
				recover();
			}
		}
	}
};
```

### Line wrapping: around 90 characters

Aim to wrap code and Javadoc at 90 characters but favor readability over wrapping as there is no deterministic way to line-wrap in every situation. 

When wrapping a lengthy expression put the separator symbol at the end of the line, rather on the next line (think comma separated arguments as an exemple). For instance:

```
if (thisLengthyMethodCall(param1, param2) && anotherCheck() &&
        yetAnotherCheck()) {
....
}
```

### Blank Lines

Add two blank lines before the following elements:

* `static {}` block
* Fields
* Constructors
* Inner classes

Add one blank line after a method signature that is multiline, i.e.

```
@Override
protected Object invoke(FooBarOperationContext context, 
        AnotherSuperLongName name) {

    // code here
}
```