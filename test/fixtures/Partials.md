---
title: Partials

area: docs
section: templates

categories:
- templates
tags:
- includes
- partials
---

> Like "includes", partials are reusable fragments of code that can be included in a page and rendered


## Syntax

Partials are useful when you have blocks of reusable code that are applicable in different contexts. The `Handlebars.registerPartial` method, which registers a partial, accepts the name of the partial as its first argument and either a _template source string_ or a _compiled template_ as its second argument.

Accepting a compiled template as the second argument enables you to, for example, use the partial in a loop that outputs a list but also append items to the list later using the partial's template function.

{{#draft}}
To use a partial from a template, simply include `\{{> partial-name }}`. For example:
{{/draft}}

#### Also see [options.partials][options-partials] →
