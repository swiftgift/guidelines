# Coding Style Guide

This repository serves as a reference for our coding standarts, and an introduction to our products. You can read the common section, or jump to language specific pages.

* [CoffeeScript](https://github.com/swiftgift/guidelines/blob/master/COFFEESCRIPT.md)
* [Jade](https://github.com/swiftgift/guidelines/blob/master/JADE.md)
* [Stylus](https://github.com/swiftgift/guidelines/blob/master/STYLUS.md)
* [JavaScript](https://github.com/swiftgift/guidelines/blob/master/JAVASCRIPT.md)
* [HTML](https://github.com/swiftgift/guidelines/blob/master/HTML.md)

## Table of Contents
  * [Tabs or Spaces?](#tabs-or-spaces)
  * [Maximum Line Length](#maximum-line-length)
  * [Blank Lines](#blank-lines)
  * [Trailing Whitespace](#trailing-whitespace)
  * [Encoding](#encoding)
  * [Naming Conventions](#naming-conventions)

## Tabs or Spaces?

Use **spaces only**, with **2 spaces** per indentation level. Never mix tabs and spaces.

**[⬆ back to top](#table-of-contents)**

## Maximum Line Length

Limit all lines to a maximum of 90 characters. Going over the limit is tolerated, but frown upon. Please try to avoid it.

**[⬆ back to top](#table-of-contents)**

## Blank Lines

Separate top-level function and class definitions with a single blank line.

Separate method definitions inside of a class with a single blank line.

Use a single blank line within the bodies of methods or functions in cases where this improves readability (e.g., for the purpose of delineating logical sections).

**[⬆ back to top](#table-of-contents)**

## Trailing Whitespace

Do not include trailing whitespace on any lines. Use plugins to highlight that for you.

## Encoding

UTF-8 is the source file encoding.

**[⬆ back to top](#table-of-contents)**

## Naming Conventions

Use `camelCase` (with a leading lowercase character) to name all variables, methods, and object properties.

Use `CamelCase` (with a leading uppercase character) to name all classes.

For constants, use all uppercase with underscores:

```coffeescript
CONSTANT_LIKE_THIS
```

Methods and variables that are intended to be "private" should begin with a leading underscore:

```coffeescript
_privateMethod: ->
```

**[⬆ back to top](#table-of-contents)**
