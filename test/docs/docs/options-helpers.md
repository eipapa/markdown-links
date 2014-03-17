---
title: options.helpers
shortname: helpers

area: docs
section: configuration

categories:
- options
- helpers
tags:
- options
- helpers
---
## options.helpers

> Helpers manipulate the output of variables

For the most part helper expressions follow this pattern: `\{{ helper_name variable_name }}`.

For example:

```handlebars
<title>\{{ uppercase title }}</title>
```
Renders to:

```html
<title>PAGE TITLE</title>
```

## Custom helpers
Custom helpers may be loaded with the current engine via `options: { helpers: []}` in the assemble task or target. But _any helpers registered at the target level will override task-level helpers_.

Globbing patterns may be used to specify paths to the helpers to be loaded:

```js
assemble: {
  options: {
    helpers: ['./lib/helpers/**/*.js']
  }
}
```
> For more info see [Custom Helpers][custom-helpers]. Or download [grunt-init-helper](https://github.com/assemble/grunt-init-helper) to generate helpers →


## Related Info

* [Helpers][helpers]
* [Custom Helpers][custom-helpers]
* [Options][options]

## External Links

* [handlebars-helpers](http://github.com/assemble/handlebars-helpers)
