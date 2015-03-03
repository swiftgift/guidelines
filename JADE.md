# Jade Style Guide

We use jade over pure html to avoid markup closure errors and to improve templates readability.

Except for directives where there can be custom HTML tags, **HTML must be valid**.

Please also read [HTML Style Guide](https://github.com/swiftgift/guidelines/blob/master/HTML.md)

## Table of Contents
  * [General Rules](general-rules)
  * [Inline JavaScript](inline-javascript)
  * [Variables](variables)
  * [Helpers](helpers)

## General Rules

  * Absolutely no traling spaces. Traling spaces break jade.
  * Ids must be placed first
  * Classes must use the dot syntax
  * Classes describing the element should be placed first
  * Responsive classes should be placed at the end

```jade
h1#id.l-h-title.col-md-6 // GOOD

h1#id.col-md-6.l-h-title // BAD

h1.l-h-title#id // BAD

h1#id(class="l-h-title") // BAD
```

**[⬆ back to top](#table-of-contents)**

## Inline JavaScript

Try to avoid inline JavaScript and always use Jade's indentation for blocks.

Prefer jade control structures.

**[⬆ back to top](#table-of-contents)**

## Variables

When outputting only a variable, use `tag= var` , not `tag #{var}`

**[⬆ back to top](#table-of-contents)**

## Helpers

We use one helpers file that should run on both client and server. Your templates, with minor exceptions, should be compatible with both server and client too. You should **NOT** use any environment-related variables or tools in your template. You should **NOT** put business logic in the templates. Only minimal data manipulation is allowed. If it requires more, put it in the View.

