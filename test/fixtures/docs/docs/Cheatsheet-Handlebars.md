---
title: Handlebars Cheatsheet

area: docs
section: templates

published: false
---

TODO:

* '.'
* '..'
* '{{> partial . }}'
* '{{> partial this }}'
* '{{#each .}}{{> partial this }}{{/each}}'



## Syntax

In this cheatsheet, to simplify, models are represented as JSON.

### Code comments

```html
\{{! code comments }}
```


### Properties

HTML is escaped by default.

```html
\{{person}}
```

### Un-escaped Properties

When you use a "triple-stache" the HTML is unescaped.

```html
\{{{person}}}
```

### Block Expressions

A block expression in Handlebars works like a block tag in HTML, with each block beginning with an "open tag" and ending with a "close tag".

```html
\{{#property}}
Content...
\{{/property}}
```

### Inverted Block Expressions

```html
\{{^foo}}
Homes for sale
\{{/foo}}
```

Inverted blocks begin with a circumflex (`^`) and behave in a similar way to the built-in [\{{unless}}](#\{{unless}}) helper. Thus, the following content will only render when `foo` **does not** satisfy one of the following conditions:

### Block Expression Conditionals

If the content is:

* `false/empty list`: content is not rendered
* `true scalar value`: content will be rendered
* `hash value`: context set to hash before rendering content
* `list value`: loops through list, sets context to each element before rendering content
* `function`: passes content to the function ([see docs](...........))


## Contexts

### Current context

`this` refers to current context

```html
\{{my_tag this}}
```

### Nested contexts

Use `.` paths to access nested contexts

```html
\{{person.name}}
```

### Absolute paths

Use absolute paths, too

```html
\{{one.two}}
```

### Ancestor contexts

Use `../` paths to access ancestor contexts

```html
\{{../company.name}}
```

### List elements

Use `[]` to access a list element

```html
\{{articles.[5]}}
```


## Built-In Helpers

### \{{if}}

```html
\{{#if}}
Yes
\{{else}}
No
\{{/if}}
```

### \{{unless}}

```html
\{{#unless}}
Content
\{{/unless}}
```

### \{{with}}

```html
\{{#with}}
Content
\{{/with}}
```

### \{{each}}

```html
\{{#each}}
Content
\{{/each}}
```

## Custom Helpers

Single-Tag:

```html
\{{myHelper [args]}} -> function ([args])
```

Block:

```html
\{{#myHelper [arg]}} blah
```

```html
\{{/myHelper}} -> function (arg|context, fn)
```

Allowed arguments:

* Strings
* context paths
* Hash args (`foo="bar"`)
* Options?
* `this`: always set to the current context within the helper

### Escaping HTML

and to escape something inside your helper

```js
Handlebars.Utils.escapeExpression(string)
```

### "Un"-escaping HTML

To prevent your helper's output from being HTML-escaped

```js
Handlebars.SafeString(string)
```


## Escaping the templates

Use `\` for escaping the Handlebars template itself.

``` md
\\{{ page.title }}
```

This will prevent the template from being compiled.



### Examples

#### "this"

Template:

```html
\{{#posts}} <li>\{{{link_to this}}}</li> \{{/posts}}
```

Helper:

```js
Handlebars.registerHelper('link_to', function (context) {
  return '<a href="' + context.url + '">' + context.body + '</a>';
});
```

Handlebars also allows for name conflict resolution between helpers and data fields via a `this` reference:

```html
<p>{{./name}} or {{this/name}} or {{this.name}}</p>
```

Any of the above would cause the `name` field on the current context to be used rather than a helper of the same name.

Partials:

```html
{{#each items}}
  {{! Passes the current item in items to your partial }}
  {{> item-template this}}
{{/each}}
```

#### hash args

Template:

```html
\{{#posts}} <li>\{{{headline title class="foo"}}}</li> \{{/posts}}
```

Helper:

```js
Handlebars.registerHelper('headline', function (title, options) {
  var attrs = [];
  for(var prop in options.hash) {
    attrs.push(prop + '="' + options.hash[prop] + '"');
  }
  return new Handlebars.SafeString(
    "<h2 " + attrs.join(" ") + ">" + title + "</h2>"
  );
});
```


Template:

```html
\{{#people}} <li>\{{{#link}}}\{{name}}\{{/link}}</li> \{{/people}}
```

Helper:

```js
Handlebars.registerHelper('link', function(context, fn) {
  return '<a href="/people/' + this.__get__("id") + '">' + fn(this) + '</a>';
});
```

## Partials


Inline another template's contents (inherits context)

```html
\{{> template-name }}
```

```html
\{{#people}} <li>\{{> link}}</li> \{{/people}}
```

```js
Handlebars.registerPartial('link', '<a href="/people/\{{id}}">\{{name}}</a>')
```

TODO:

* partials with variables



## Inlining Templates

```html
<script type="text/x-handlebars" [data-template-name="intro"]>
  My name is \{{name}}.
</script>
```


