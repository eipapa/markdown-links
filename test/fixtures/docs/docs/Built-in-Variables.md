---
title: Built-in Variables

area: docs
section: configuration
---

## "[Page][pages]" Variables

The following variables are defined on the `page` object, which exposes data for the "current page" at build time:

* `\{{basename}}` : Equivalent to node [path.basename][path-basename], returns the basename for the current page from the root of the context. Example: `\{{basename 'index.html'}}`, returns "index", can also be used with the [page|Pages] variable: `\{{basename page}}`.
* `\{{dirname}}` : equivalent to node [path.dirname][path-dirname].
* `\{{ext}}` : equivalent to node [path.extname][path-extname].
* `\{{extname}}` : alias for `ext`
* `\{{filename}}` : equivalent to ([path.basename][path-basename] + [path.extname][path-extname]), `\{{filename 'index.html'}}`, returns `index.html`. Can also be used with `page` variable: `\{{filename page}}`.
* `\{{pagename}}` : alias for `basename`.
* `\{{pageName}}` : deprecated, use `pagename` or `filename`

[path-basename]: http://nodejs.org/api/path.html#path_path_basename_p_ext
[path-extname]: http://nodejs.org/api/path.html#path_path_extname_p
[path-dirname]: http://nodejs.org/api/path.html#path_path_dirname_p


## "[YFM][yaml-front-matter]" Variables

* `categories` : a category, or an array of categories that are associated with this page. These should be provided in the yaml header.
* `tags` : List of tag objects that are associated with this page. These should be provided in the yaml header.
{{#draft}}* `next` : The full/relative? URL to the "next" page. The next page will be the next page from the pages list. Can be overridden in the yaml header.{{/draft}}
{{#draft}}* `previous` : The full/relative? URL to the "previous" page. The previous page will the previous page from the pages list. Can be overridden in the yaml header.{{/draft}}
* `custom` : Any custom front matter that you specify will be available under `page`. For example, if you specify `something: true` in a page's front matter, that value will be available in templates as `page.something`"
* `layout` : the layout to be used for the current page. Overrides any layouts defined in the `assemble.options`, at the task and target level,
* `published` : Use `published: false` in the [YAML Front Matter][yaml-front-matter] of a page to exclude the page from being rendered.

``` yaml
---
title: Just testing some stuff on this page, it should not be published
published: false
---
```

### Collections
Collections can also be defined in YAML front matter:

* `pages` : list of pages in a target.
* `categories` : lists of all the category objects
* `tags` : lists of all tag objects
* `paginate` (planned)

> [Learn more][options-collections] about collections →



<a id="custom-variables"></a>
## Custom variables
You may add any custom variable you require to the `assemble` task or target options. Custom variables are added to the _root of the data context_ and be available in any templates.

For example, given that the custom variable `production` is set to `false` :

``` js
assemble: {
  options: {
    production: false
  },
  ...
}
```
This template:

``` html
\{{#if production}}
<script src="dist/assets/script.min.js"></script>
\{{else}}
<script src="dist/assets/script.js"></script>
\{{/if}}
```
Will render the HTML for the _non-minified_ &nbsp; script tag:

``` html
<script src="dist/assets/script.js"></script>
```

## Helpers

Variables can be modified using using special tags called [helpers][helpers]. Helpers may also accept parameters, each of which is a [Handlebars expression](http://handlebarsjs.com/expressions.html).

### See [Helpers][helpers] and [Custom Helpers][custom-helpers] →


{{#draft}}
### Contexts (? @doowb, how should this be described?)

* `this` : example: `this.title`
* `page` : example: `page.title`
* `root` : example: `title`

* `options.page` : exposes data for the "current" page at build time
* `options.pages` :
* `options.dest` :
* `options.src` :


### Example usage

``` js
assemble: {
  // Task options
  options: {
    data: ['src/one/*.json']
  },
  ghpages: {
    // Target options
    options: {
      data: ['src/two/*.{yml,json}']
    }
    files: { 'docs/': ['src/templates/*.hbs'] }
  }
}
```
{{/draft}}

## Related info

* [Options][options]
* [Helpers][helpers]
