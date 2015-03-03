# Jade Style Guide

We use jade over pure html to avoid markup closure errors and to improve templates readability. **HTML must be valid**. Always remember, that underneath all of the Jade's fancyness it's plain JavaScript, so same rules apply.

You can find language reference here: [http://jade-lang.com](http://jade-lang.com).

Please also read [HTML Style Guide](https://github.com/swiftgift/guidelines/blob/master/HTML.md) and [JavaScript Style Guide](https://github.com/swiftgift/guidelines/blob/master/JAVASCRIPT.md)

## Table of Contents
  * [General Rules](general-rules)
  * [Inline JavaScript](inline-javascript)
  * [Variables](variables)
  * [Interpolation](interpolation)
  * [JSON](json)
  * [Helpers](helpers)

## General Rules

  * Absolutely no traling spaces. Traling spaces break jade. If you need to put a space at the end of the line, use `&#32;`. You're welcome.
  * Ids must be placed first
  * Classes must use the dot syntax
  * Classes describing the element should be placed first
  * Responsive classes should be placed at the end

```jade
h1#id.l-h-title.col-md-6 //- GOOD

h1#id.col-md-6.l-h-title //- BAD

h1.l-h-title#id //- BAD

h1#id(class="l-h-title") //- BAD
```

**[⬆ back to top](#table-of-contents)**

## Inline JavaScript

Try to avoid inline JavaScript and always use Jade's indentation for blocks.

Prefer jade control structures.

**[⬆ back to top](#table-of-contents)**

## Variables

When outputting only a variable, use `tag= var` , not `tag #{var}`.

If you are declaring a new variable yourself, remember that Jade creates a local scope for each template. Use `var` statements and you'll be fine:

```jade
- var _class = null
```

**[⬆ back to top](#table-of-contents)**

## Interpolation

Interpolation is your friend. Always use interpolation in long blocks of text, or class names that require just a little bit extra:

```jade
a(href="/#{link}") Cap'n Awesome
```

**[⬆ back to top](#table-of-contents)**

## JSON

When you output JSON and raw JavaScript you need to always:

  1. Use unescaped version of output
  2. Stringify the object yourself
  3. Sanitize potentially unsafe strings to avoid possible XSS

```jade

script.
  var app = {
    config: !{JSON.stringify(config)},
    env: !{jade.helpers.sanitizeString(JSON.stringify(env))}
  };

```

**[⬆ back to top](#table-of-contents)**

## Helpers

We use one helpers file that should run on both client and server. Your templates, with rare exceptions, should be compatible with both server and client too. You should **NOT** use any environment related variables or tools in your template. You should **NOT** put business logic in the templates. Only minimal data manipulation is allowed. If it requires more, put it in the View.

**[⬆ back to top](#table-of-contents)**
