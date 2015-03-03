# CoffeeScript Style Guide

This is how you're supposed to write your code in CoffeeScript.

Inspired by: [CoffeeScript Style Guide](https://github.com/polarmobile/coffeescript-style-guide)

## Table of Contents
  * [Optional Commas](#optional-commas)
  * [Module Imports](#module-imports)
  * [Whitespace in Expressions and Statements](#whitespace)
  * [Functions](#functions)
  * [Strings](#strings)
  * [Conditionals](#conditionals)
  * [Looping and Comprehensions](#looping-and-comprehensions)
  * [Extending Native Objects](#extending-native-objects)
  * [Exceptions](#exceptions)
  * [Annotations](#annotations)
  * [Miscellaneous](#miscellaneous)

## Optional Commas

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

**[⬆ back to top](#table-of-contents)**

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

**[⬆ back to top](#table-of-contents)**

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
    - comparisons: `==`, `<`, `>`, `<=`, `>=`, `unless`, etc.
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

**[⬆ back to top](#table-of-contents)**

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

**[⬆ back to top](#table-of-contents)**

## Strings

Use string interpolation instead of string concatenation:

```coffeescript
"this is an #{adjective} string" # GOOD
"this is an " + adjective + " string" # BAD
```

Prefer single quoted strings (`''`) instead of double quoted (`""`) strings, unless features like string interpolation are being used for the given string.

**[⬆ back to top](#table-of-contents)**

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

**[⬆ back to top](#table-of-contents)**

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

**[⬆ back to top](#table-of-contents)**

## Extending Native Objects

Do not modify native objects.

For example, do not modify `Array.prototype` to introduce `Array#forEach`.

**[⬆ back to top](#table-of-contents)**

## Exceptions

Do not suppress exceptions.

**[⬆ back to top](#table-of-contents)**

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

**[⬆ back to top](#table-of-contents)**

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
