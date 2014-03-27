---
title: options.layout
shortname: layout

area: docs
section: configuration

categories:
- options
- templates
tags:
- options
- layout
- layouts
- templates
---

## options.layout

> Layouts are commonly used with client-side templates as a quick way to "wrap" a number of [pages][] with commonly used page "sections", such as the head, footer or navigation.

## Options
Type: `String`|`False`|`None` (optional)
Default: `undefined`

Path to the layout to be used for the current target. Layouts are optional and may be defined at the task and/or [target][tasks-and-targets] level. _Unlike Jekyll_, Assemble requires a file extension since you are not limited to using a single file type.

``` js
assemble: {
  options: {
    layout: 'path/to/layouts/default.hbs'
  }
}
```

## Defining Layouts
Oftentimes you will need more than one layout for your project, so layouts can be defined using the `options.layout` variable at the task or target-level, or they can be specified at the page-level by adding a `layout` property to the [YFM][yaml-front-matter].


## The `\{{> body }}` tag
Although layouts are optional, the `\{{> body }}` tag is required for content to be pulled into a layout.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>\{{title}}</title>
  </head>
  <body>
    <!-- the body tag is used to "pull in" content from pages -->
    \{{> body }}
  </body>
</html>
```

#### Also see [Layouts][layouts] and [layoutdir][options-layoutdir] →


## Related info:

* [Options][options]
* [Variables][built-in-variables]
{{#draft}}* [Markdown Options][Markdown]{{/draft}}
* [YAML Options][YAML]