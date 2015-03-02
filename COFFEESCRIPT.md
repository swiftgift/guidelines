# CoffeeScript Style Guide

CoffeeScript is a very liberal language, that allows you to write code in a variety of ways. That leads to the codebase becoming sloppy over time. Let's remedy that by establishing a few rules to code by.

Inspired by: [CoffeeScript Style Guide][https://github.com/polarmobile/coffeescript-style-guide]

## Table of Contents
  * [Code Layout](#code_layout)
      * [Tabs or Spaces?](#tabs_or_spaces)
      * [Maximum Line Length](#maximum_line_length)
      * [Blank Lines](#blank_lines)
      * [Trailing Whitespace](#trailing_whitespace)
      * [Optional Commas](#optional_commas)
      * [Encoding](#encoding)
  * [Module Imports](#module_imports)
  * [Whitespace in Expressions and Statements](#whitespace)
  * [Naming Conventions](#naming_conventions)
  * [Functions](#functions)
  * [Strings](#strings)
  * [Conditionals](#conditionals)
  * [Looping and Comprehensions](#looping_and_comprehensions)
  * [Extending Native Objects](#extending_native_objects)
  * [Exceptions](#exceptions)
  * [Annotations](#annotations)
  * [Miscellaneous](#miscellaneous)

<a name="code_layout"/>
## Code layout

<a name="tabs_or_spaces"/>
### Tabs or Spaces?

Use **spaces only**, with **2 spaces** per indentation level. Never mix tabs and spaces.

<a name="maximum_line_length"/>
### Maximum Line Length

Limit all lines to a maximum of 90 characters. Going over the limit is tolerated, but frown upon. Please try to avoid it.

<a name="blank_lines"/>
### Blank Lines

Separate top-level function and class definitions with a single blank line.

Separate method definitions inside of a class with a single blank line.

Use a single blank line within the bodies of methods or functions in cases where this improves readability (e.g., for the purpose of delineating logical sections).

<a name="trailing_whitespace"/>
### Trailing Whitespace

Do not include trailing whitespace on any lines. Use plugins to highlight that for you.

<a name="optional_commas"/>
### Optional Commas

Avoid the use of commas before newlines when properties or elements of an Object or Array are listed on separate lines.

```coffeescript
# GOOD
foo = [
  'some'
  'string'
  'values'
]
bar:
  label: 'test'
  value: 87

# BAD
foo = [
  'some',
  'string',
  'values'
]
bar:
  label: 'test',
  value: 87

# RETARDED
foo = [
    'some'
  , 'string'
  , 'values'
]
bar:
    label: 'test'
  , value: 87

```

<a name="encoding"/>
### Encoding

UTF-8 is the source file encoding.

<a name="module_imports"/>
## Module Imports

CommonJS Modules `require` statements should be placed on separate lines.

```coffeescript
require('lib/setup')
Backbone = require('backbone')
```
These statements should be grouped in the following order:

1. Standard library imports _(if a standard library exists)_
2. Third party library imports
3. Local imports _(imports specific to this application or library)_

<a name="whitespace"/>
## Whitespace in Expressions and Statements

Avoid extraneous whitespace in the following situations:

- Immediately inside parentheses, brackets or braces

    ```coffeescript
       ($('body')) # GOOD
       ( $ ('body') ) # BAD
    ```

- Immediately before a comma

    ```coffeescript
       console.log(x, y) # GOOD
       console.log(x , y) # BAD
    ```

Additional recommendations:

- Always surround these binary operators with a **single space** on either side

    - assignment: `=`

        - _Note that this also applies when indicating default parameter value(s) in a function declaration_

           ```coffeescript
           test: (param = null)-> # GOOD
           test: (param=null)-> # BAD
           ```

    - augmented assignment: `+=`, `-=`, etc.
    - comparisons: `<`, `>`, `<=`, `>=`, `unless`, etc.
    - arithmetic operators: `+`, `-`, `*`, `/`, etc.

    - _(Do not use more than one space around these operators)_

        ```coffeescript
           # GOOD
           x = 1
           y = 1
           fooBar = 3

           # BAD
           x      = 1
           y      = 1
           fooBar = 3
        ```

<a name="naming_conventions"/>
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

<a name="functions"/>
## Functions

_(These guidelines also apply to the methods of a class.)_

When declaring a function that takes arguments, don't use any spaces after the closing parenthesis of the arguments list:

```coffeescript
foo = (arg1, arg2)-> # GOOD
foo = (arg1, arg2) -> # BAD
```

Do not use parentheses when declaring functions that take no arguments:

```coffeescript
bar = -> # GOOD
bar = ()-> # BAD
```

In cases where method calls are being chained and the code does not fit on a single line, each call should be placed on a separate line and indented by one level (i.e., two spaces), with a leading `.`.

```coffeescript
[1..3]
  .map((x)-> x * x)
  .concat([10..12])
  .filter((x)-> x < 11)
  .reduce((x, y)-> x + y)
```

When calling functions, never omit parentheses:

```coffeescript
baz(12) # GOOD
baz 12 # BAD

time = new Date() # GOOD
time = new Date # BAD
```

It is very important to follow this rule. CoffeeScript allows to omit parenthesis when a function called with arguments being passed. Abusing this leads to hard to illegible code with hard to track bugs:

```coffeescript
(($ '#selektor').addClass 'klass').hide() # RETARDED
```

<a name="strings"/>
## Strings

Use string interpolation instead of string concatenation:

```coffeescript
"this is an #{adjective} string" # GOOD
"this is an " + adjective + " string" # BAD
```

Prefer single quoted strings (`''`) instead of double quoted (`""`) strings, unless features like string interpolation are being used for the given string.

<a name="conditionals"/>
## Conditionals

Favor `unless` over `if` for negative conditions.

Instead of using `unless...else`, use `if...else`:

```coffeescript
  # GOOD
  if true
    ...
  else
    ...

  # BAD
  unless false
    ...
  else
    ...
```

Multi-line if/else clauses should use indentation:

```coffeescript
  # GOOD
  if true
    ...
  else
    ...

  # BAD
  if true then ...
  else ...
```

<a name="looping_and_comprehensions"/>
## Looping and Comprehensions

Take advantage of comprehensions whenever possible:

```coffeescript
  # GOOD
  result = (item.name for item in array)

  # BAD
  results = []
  for item in array
    results.push item.name
```

To filter:

```coffeescript
result = (item for item in array when item.name is "test")
```

To iterate over the keys and values of objects:

```coffeescript
object = one: 1, two: 2
alert("#{key} = #{value}") for key, value of object
```

<a name="extending_native_objects"/>
## Extending Native Objects

Do not modify native objects.

For example, do not modify `Array.prototype` to introduce `Array#forEach`.

<a name="exceptions"/>
## Exceptions

Do not suppress exceptions.

<a name="annotations"/>
## Annotations

Use annotations when necessary to describe a specific action that must be taken against the indicated block of code.

Write the annotation on the line immediately above the code that the annotation is describing.

The annotation keyword should be followed by a colon and a space, and a descriptive note.

```coffeescript
  # FIXME: The client's current state should *not* affect payload processing.
  resetClientState()
  processPayload()
```

If multiple lines are required by the description, indent subsequent lines with two spaces:

```coffeescript
  # TODO: Ensure that the value returned by this call falls within a certain
  #   range, or throw an exception.
  analyze()
```

Annotation types:

- `TODO`: describe missing functionality that should be added at a later date
- `FIXME`: describe broken code that must be fixed
- `REVIEW`: describe code that should be reviewed to confirm implementation

If a custom annotation is required, the annotation should be documented in the project's README.

<a name="miscellaneous"/>
## Miscellaneous

`and` is preferred over `&&`.

`or` is preferred over `||`.

`is` is preferred over `==`.

`not` is preferred over `!`.

`or=` should be used when possible:

```coffeescript
temp or= {} # GOOD
temp = temp || {} # BAD
```

Prefer shorthand notation (`::`) for accessing an object's prototype:

```coffeescript
Array::slice # GOOD
Array.prototype.slice # BAD
```

Prefer `@property` over `this.property`.

```coffeescript
return @property # GOOD
return this.property # BAD
```

However, avoid the use of **standalone** `@`:

```coffeescript
return this # GOOD
return @ # BAD
```

Avoid `return` where not required, unless the explicit return increases clarity.

Use splats (`...`) when working with functions that accept variable numbers of arguments:

```coffeescript
console.log(args...) # GOOD

(a, b, c, rest...)-> # GOOD
```
