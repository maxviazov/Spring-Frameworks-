## Introduction

This document serves as the definition of the coding standards for source files in the Spring Framework. It is primarily intended for the Spring Framework team but can be used as a reference by contributors.

The structure of this document is based on the [Google Java Style](http://google-styleguide.googlecode.com/svn/trunk/javaguide.html) reference and is _work in progress_.

## Source File Basics

### File encoding: ISO-8859-1 

Source files must be encoded using `ISO-8859-1`.

### Indentation

* Indentation uses _tabs_ (not spaces)
* Unix (LF), not DOS (CRLF) line endings
* Eliminate all trailing whitespace

## Source file structure

A source file consists of, in order:

* License
* Package statement
* Import statements
* Exactly one top-level class

Exactly one blank line separates each section that is present.

### License

Each source file must specify the following license at the very top of the file:

	/*
	 * Copyright 2002-2014 the original author or authors.
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

Always check the date range in the license header. For example, if you've modified a file in 2014 whose header still reads:
```   
* Copyright 2002-2011 the original author or authors.
```
Then be sure to update it to 2014 accordingly:
```
* Copyright 2002-2014 the original author or authors.
```

### Java source file organization

The following governs how the elements of a source file are organized:

1. static fields
1. normal fields
1. constructors
1. (private) methods called from constructors
1. static factory methods
1. properties
1. method implementations coming from interfaces
1. private or protected templates that get called from method implementations coming from interfaces
1. other methods
1. `equals`, `hashCode`, and `toString`

Above all, the organization of the code should feel natural.

## Formatting

### Braces

#### Block-like constructs: K&R style

Braces mostly follow the _Kernighan and Ritchie style_ (a.k.a., "Egyptian brackets") for nonempty blocks and block-like constructs:

* No line break before the opening brace but prefixed by a single space
* Line break after the opening brace
* Line break before the closing brace
* Line break after the closing brace if that brace terminates a statement or the body of a method, constructor, or named class with the exception of the `else` statement that also leads to a line break

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
			} catch (ProblemException e) {
				recover();
			}
		}
	}
};
```

### Line wrapping: around 90 characters

Aim to wrap code and Javadoc at 90 characters but favor readability over wrapping as there is no deterministic way to line-wrap in every situation. 

## Naming

### Constant names

Constant names use `CONSTANT_CASE`: all uppercase letters, with words separated by underscores. 

Every constant is a `static final` field, but not all `static final` fields are constants. Constant case should therefore be chosen only if the field **is really** a constant.

Example:

```
// Constants
private static final Object NULL_HOLDER = new NullHolder();
public static final int DEFAULT_PORT = -1;

// Not constants
private static final ThreadLocal<Executor> executorHolder = new ThreadLocal<Executor>();
private static final Set<String> internalAnnotationAttributes = new HashSet<String>();
```

## Programming Practices

### File history

* A file should look like it was crafted by a single author, not like a history of changes
* Don't artificially spread things out that belong together

### Organization of setter methods

Choose wisely where to add a new setter method; it should not be simply added at the end of the list. Perhaps the setter is related to another setter or relates to a group. In that case it should be placed near related methods.

* Setter order should reflect order of importance, not historical order
* Ordering of _fields_ and _setters_ should be **consistent**
