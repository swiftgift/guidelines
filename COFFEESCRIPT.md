# CoffeeScript Style Guide

Grab a nice cuppa and have a read. You can find the language reference here: [http://coffeescript.org](http://coffeescript.org). Remember to always keep your local CoffeeScript up to date: `npm install -g coffee-script`. For a quick js -> coffee conversion there is [http://js2.coffee](http://js2.coffee). Remember that you still have to edit the result.

Please also read [JavaScript Style Guide](https://github.com/swiftgift/guidelines/blob/master/JAVASCRIPT.md)

Inspired by: [CoffeeScript Style Guide](https://github.com/polarmobile/coffeescript-style-guide)

## Table of Contents
  * [Naming Conventions](naming-conventions)
  * [Optional Commas](#optional-commas)
  * [Module Imports](#module-imports)
  * [Whitespace in Expressions and Statements](#whitespace)
  * [Functions](#functions)
  * [Strings](#strings)
  * [Conditionals](#conditionals)
  * [Looping and Comprehensions](#looping-and-comprehensions)
  * [Extending Native Objects](#extending-native-objects)
  * [Exceptions](#exceptions)
  * [Miscellaneous](#miscellaneous)

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

For JSON-replies or JSON-like data please use underscore notation:
```coffeescript
largeJsonObj =
  awesome: true
  my_var: 'legit'
  another_var: 'sure thing bruv'
```

**[⬆ back to top](#table-of-contents)**

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
           test: (param = null) -> # GOOD
           test: (param=null) -> # BAD
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

When declaring a function that takes arguments, use one space after the closing parenthesis of the arguments list:

```coffeescript
foo = (arg1, arg2) -> # GOOD
foo = (arg1, arg2)-> # BAD
```

Do not use parentheses when declaring functions that take no arguments:

```coffeescript
bar = -> # GOOD
bar = ()-> # BAD
```

In cases where method calls are being chained and the code does not fit on a single line, each call should be placed on a separate line and indented by one level (i.e., two spaces), with a leading `.`.

```coffeescript
[1..3]
  .map((x) -> x * x)
  .concat([10..12])
  .filter((x) -> x < 11)
  .reduce((x, y) -> x + y)
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

(a, b, c, rest...) -> # GOOD
```

**[⬆ back to top](#table-of-contents)**
