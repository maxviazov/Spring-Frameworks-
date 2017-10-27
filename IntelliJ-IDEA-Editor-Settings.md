This page describes the noticeable changes made to the default code formatting settings in Intellij IDEA. This is also a chance to review some of these changes to validate or tweak them if necessary:

## Issues

These are the reported issues that we still discuss (or simply things that the formatter does not support).  The first is what we use.

* Space in annotation parameter assignment: `@Foo(name="foo")` vs. `@Foo(name = "foo")`
* Space in annotation array parameter: `@Target({ ElementType.METHOD, ElementType.TYPE })` vs. `@Target({ElementType.METHOD, ElementType.TYPE})`

## General

* Default indent option to use tab character instead of space

## Java

### Tabs and indent

* Use tab character

### Spaces

* Add a space before the left brace of an array initializer

### Wrapping and braces

* Keep when reformating: _multiple expressions in one line_, _simple blocks in one line_, _simple classes in one line_
* `else`, `catch` and `finally` on new line
* Method declaration parameters: do not align when multiline

### Blank lines

* Keep one space before } (solely use to keep the space between the end of the last method and the end of the class)
* Minimum blank line after class header 0 (instead of 1)

### Javadoc

* Disabled

### Imports

* Class count to trigger static import to 50 (to prevent `import org.foo.*;` instead of listing the classes of `org.foo`)
* Changed the import sequence to import in the following order: `static imports`, `java.*`, `javax.*`, others, `org.springframework.*`. Each sequence is separated by a space
