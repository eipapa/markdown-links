---
title: Lo-Dash Cheatsheet

area: docs
section: templates

published: false
---
## Syntax

In this cheatsheet, to keep it simple models are represented as JSON.

* `<% %>`: to execute some code
* `<%= %>`: to print some value in template
* `<%- %>`: to print some values with HTML escaped

`_.template(templateString, [data], [settings])`

Compiles JavaScript templates into functions that can be evaluated for rendering. Useful for rendering complicated bits of HTML from JSON data sources. Template functions can both interpolate variables, using `<%= … %>`, as well as execute arbitrary JavaScript code, with `<% … %>`. If you wish to interpolate a value, and have it be HTML-escaped, use `<%- … %>`

When you evaluate a template function, pass in a **data** object that has properties corresponding to the template's free variables. If you're writing a one-off, you can pass the **data** object as the second parameter to **template** in order to render immediately instead of returning a template function. The **settings** argument should be a hash containing any `_.templateSettings` that should be overridden.

```js
var compiled = _.template("hello: ");
compiled({name : 'moe'});
=&gt; "hello: moe"

var list = "  ";
_.template(list, {people : ['moe', 'curly', 'larry']});
=&gt; "moecurlylarry"

var template = _.template("");
template({value : ''});
=&gt; "&lt;script&gt;"
```

You can also use `print` from within JavaScript code. This is sometimes more convenient than using ``.

```js
var compiled = _.template("");
compiled({epithet: "stooge"});
=&gt; "Hello stooge."
```

If ERB-style delimiters aren't your cup of tea, you can change Underscore's template settings to use different symbols to set off interpolated code. Define an **interpolate** regex to match expressions that should be interpolated verbatim, an **escape** regex to match expressions that should be inserted after being HTML escaped, and an **evaluate** regex to match expressions that should be evaluated without insertion into the resulting string. You may define or omit any combination of the three. For example, to perform [Mustache.js][13] style templating:

```js
_.templateSettings = {
  interpolate : /\{\{(.%2B?)\}\}/g
};

var template = _.template("Hello \{{ name }}!");
template({name : "Mustache"});
=&gt; "Hello Mustache!"
```

By default, **template** places the values from your data in the local scope via the `with` statement. However, you can specify a single variable name with the **variable** setting. This can significantly improve the speed at which a template is able to render.

```js
_.template("Using 'with': ", {answer: 'no'}, {variable: 'data'});
=&gt; "Using 'with': no"
```

Precompiling your templates can be a big help when debugging errors you can't reproduce. This is because precompiled templates can provide line numbers and a stack trace, something that is not possible when compiling templates on the client. The **source** property is available on the compiled template function for easy precompilation.


```js
JST.project = ;
```