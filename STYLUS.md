# Stylus Style Guide

A Stylus guide. No other way of writing stylus is valid. Please read [SMACSS](https://smacss.com). If you don't know if you can use a certain styling thingy, use [http://caniuse.com](http://caniuse.com) to check. Language reference can be found here: [http://learnboost.github.io/stylus/](http://learnboost.github.io/stylus/).

## Table of Contents
  * [Naming conventions](#naming-conventions)
  * [Units](#units)
  * [Specificity](#specificity)
  * [Formatting](#formatting)
  * [Vendor Prefixes](#vendor-prefixes)
  * [Variable Names](#variable-names)
  * [Property lookup](#property-lookup)
  * [Strings](#strings)
  * [Numbers](#numbers)
  * [Units](#units)
  * [Calculations](#calculations)
  * [Colors](#colors)
  * [Imports](#imports)
  * [Extend](#extend)
  * [Functions](#functions)

## Naming conventions

We are using a subset of [SMACSS](https://smacss.com) and use prefixes to separate elements on the page. Legend:

 * `.l-` layout
 * `.p-` page
 * `.m-` module
 * no prefix - state (example: `active`)

```stylus

.l-header
  background: #000

.p-index
  color: #333

.m-button
  font-size: 20px

  &.active
    color: #f00

```

As a rule of thumb, avoid unnecessary nesting in Stylus. At most, aim for three levels. If you cannot help it, step back and rethink your overall strategy (either the specificity needed, or the layout of the nesting).

Always put a class on everything. It is only OK to use a tagName if you're deeply nested, and styling a leef node.

**[⬆ back to top](#table-of-contents)**

## Units

Use px for font-size, because it offers absolute control over text. Additionally, unit-less line-height is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the font-size.

**[⬆ back to top](#table-of-contents)**

## Specificity

We never use IDs for styling. Leave dealing with IDs to JavaScript. Style with classes.

**[⬆ back to top](#table-of-contents)**

## Formatting

 - colons: **yes**
 - brackets: no
 - semicolons: hell no

```stylus
// BAD
p {
  color: hotpink;
}

// BAD
p
  color red

// GOOD
p
  color: red
```

**[⬆ back to top](#table-of-contents)**

## Vendor Prefixes
Use nib instead of writing your own

```stylus
// BAD
-webkit-border-radius: 4px
-moz-border-radius: 4px
border-radius: 4px

// GOOD
@import 'nib'
border-radius: 4px
```

**[⬆ back to top](#table-of-contents)**

## Variable Names
Start variable names with a `$`. Stylus is not a programming language. Let's not use any forms of camelCase. Avoid using dashes in variable names too: it looks like a minus sign later in the code.

```stylus
main_color = white // BAD
mainColour = white // BAD
main-color = white // BAD
$main_color = white // GOOD
```

**[⬆ back to top](#table-of-contents)**

## Property lookup

Use property lookup to avoid creating unnecessary variables.

```stylus
 #logo
   position: absolute
   top: 50%
   left: 50%
   width: 150px
   height: 80px
   margin-left: -(@width / 2)
   margin-top: -(@height / 2)

```

**[⬆ back to top](#table-of-contents)**

## Strings

URLs and font names should be quoted:

```stylus
// GOOD
$font-stack: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif

// BAD
$font-stack: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif

// BAD
$font-stack: Helvetica Neue Light, Helvetica, Arial, sans-serif

// GOOD
.foo
  background-image: url('/images/kittens.jpg')


// BAD
.foo
  background-image: url(/images/kittens.jpg)
```

**[⬆ back to top](#table-of-contents)**

## Numbers

Drop trailing and leading zeros before a decimal value when you can:

```stylus
// GOOD
.foo
  padding: 2em
  opacity: .5


// BAD
.foo
  padding: 2.0em
  opacity: 0.5

```

**[⬆ back to top](#table-of-contents)**

## Units

When dealing with lengths, a 0 value should never ever have a unit.

```stylus
// GOOD
$length: 0

// BAD
$length: 0em
```

**[⬆ back to top](#table-of-contents)**

## Calculations

Top-level numeric calculations should always be wrapped in parentheses.

```stylus
// GOOD
.foo
  width: (100% / 3)


// BAD
.foo
  width: 100% / 3

```

**[⬆ back to top](#table-of-contents)**

## Colors

In order to make colors as simple as they can be, my advice would be to respect the following order of preference for color formats:

1. Hexadecimal notation. Preferably lowercase and shortened when possible
2. RGB notation
3. HSL notation

When using HSL or RGB notation, always add a single space after a comma (,) and no space between parentheses ((, )) and content.

```stylus
// GOOD
.foo
  color: #f00

// BAD
.foo
  color: #ff0000

// BAD
.foo
  color: red

// GOOD
.foo
  color: rgba(0, 0, 0, 0.1)
  background: hsl(300, 100%, 100%)

// BAD
.foo
  color: rgba(0,0,0,0.1)
  background: hsl( 300, 100%, 100% )
```

**[⬆ back to top](#table-of-contents)**

## Imports

We place all imports in the main file. No nested imports should be made.

**[⬆ back to top](#table-of-contents)**

## Extend

Avoid using extend unless you have to. Please use mixins instead.

**[⬆ back to top](#table-of-contents)**

## Functions

We prefer using mixins over functions. If a function is absolutely necessary, document where it is used and why it wasn't possible to create a mixin instead.

**[⬆ back to top](#table-of-contents)**

