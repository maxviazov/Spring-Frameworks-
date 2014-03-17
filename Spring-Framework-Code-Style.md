## Introduction

This document serves as the definition of the coding standards for source files in the Spring Framework. It is primarily intended for the Spring Framework team but can be used as a reference by contributors.

The structure of this document is based on the [Google Java Style](http://google-styleguide.googlecode.com/svn/trunk/javaguide.html) reference and is _work in progress_.

## Source File Basics

### File encoding: ISO-8859-1 

Source files must be encoded using `ISO-8859-1`. (see [SPR-11569](https://jira.spring.io/browse/SPR-11569) for an attempt to move to `UTF-8`)

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
			catch (ProblemException e) {
				recover();
			}
		}
	}
};
```

### Line wrapping: around 90 characters

Aim to wrap code and Javadoc at 90 characters but favor readability over wrapping as there is no deterministic way to line-wrap in every situation. 

### Spaces

Add two spaces around the following elements:

* `static {` block
* fields
* Constructors
* Inner class

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

### Elvis operator

Wrap the elvis operator with parenthesis, i.e. `return (foo != null ? foo : "default");`

### Null check

Use the `Assert.notNull` static method to check that a method argument is not `null`. Format the exception message so that the name of the parameter comes first with its first character capitalized, following by _must not be null_. For instance

```
public void handle(Event event) {
    Assert.notNull(event, "Event must not be null");
    //...
}
```

### Static imports

Static imports should not be used in production code. It should be used in test code, especially for things like `org.junit.Assert`

### Use of @Override

Always add `@Override` on methods overriding a method declared in a super type.

### Use of @since

* `@since` should be added to every new class with the version of the framework in which it was introduced
* `@since` should be added to any *new* **public** and **protected** methods of an existing class

### Utility classes

A class that has only a bunch of utility static methods should be named with a `Utils` suffix and should be abstract, e.g.

```
public abstract MyUtils {

  // static utility methods
}
```

Making the method abstract prevents anyone from instantiating it and replace the _private_ constructor.

## Javadoc

### Javadoc formatting

The following template summarizes a typical use for the javadoc of a method

```
/**
 * Parse the specified {@link Element} and register the resulting
 * {@link BeanDefinition BeanDefinition(s)}.
 * <p>Implementations must return the primary {@link BeanDefinition} that results
 * from the parse if they will ever be used in a nested fashion (for example as
 * an inner tag in a {@code <property/>} tag). Implementations may return
 * {@code null} if they will <strong>not</strong> be used in a nested fashion.
 * @param element the element that is to be parsed into one or more {@link BeanDefinition BeanDefinitions}
 * @param parserContext the object encapsulating the current state of the parsing process;
 * provides access to a {@link org.springframework.beans.factory.support.BeanDefinitionRegistry}
 * @return the primary {@link BeanDefinition}
 */
BeanDefinition parse(Element element, ParserContext parserContext);
```

In particular, please note:

* Use an imperative style (i.e. _Return_ and not _Returns_)
* No space between the description and the parameters description
* If the description is defined with multiple paragraphs, start each of them with `<p>`
* If a parameter description needs to be wrapped, do not align it (see `parserContext`)

The javadoc of a class has some extra rules that are illustrated by the sample below:

```
/*
 * Interface used by the {@link DefaultBeanDefinitionDocumentReader} to handle custom,
 * top-level (directly under {@code <beans/>}) tags.
 *
 * <p>Implementations are free to turn the metadata in the custom tag into as many
 * {@link BeanDefinition BeanDefinitions} as required.
 *
 * <p>The parser locates a {@link BeanDefinitionParser} from the associated
 * {@link NamespaceHandler} for the namespace in which the custom tag resides.
 *
 * @author Rob Harrop
 * @since 2.0
 * @see NamespaceHandler
 * @see AbstractBeanDefinitionParser
 */
```

* Each class should have a `@since` tag with the version in which the class was introduced
* The order of tags for a class javadoc is `@author`, `@since` and `@see`
* Contrary to methods javadoc, the paragraphs of a class description *are* separated by a space

The following are other general rules to also apply when writing javadoc:

* Use `{@code}` to wrap code statements or values such as `null`
* If a class is solely used by a `{@link}` element, use the fully qualified name to avoid a useless import

## Test

### Naming

Each test class should end with a `Tests` suffix.

### Mocking

Use the BDD Mockito support.