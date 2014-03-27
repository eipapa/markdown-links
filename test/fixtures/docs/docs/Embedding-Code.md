---
title: Embedding Code

area: docs
section: content
---

> Assemble has many solutions for embedding code snippets, depending on your needs.



## [Helpers for Embedding Code](https://github.com/assemble/handlebars-helpers#code-helpers)

You can use one of Assemble's built-in "code" helpers (from the [handlebars-helpers](https://github.com/assemble/handlebars-helpers) library), or create a [custom helper](http://assemble.io/docs/Custom-Helpers.html) that meets your needs.

Each "code helper" is useful for a different use case. Visit the documentation for each helper to learn more about them.

* `\{{embed}}`: https://github.com/assemble/handlebars-helpers#embed
* `\{{gist}}`: https://github.com/assemble/handlebars-helpers#gist
* `\{{jsfiddle}}`: https://github.com/assemble/handlebars-helpers#jsfiddle


[gfm]: http://github.github.com/github-flavored-markdown/ "GitHub Flavored Markdown"
[highlighting]: https://help.github.com/articles/github-flavored-markdown#syntax-highlighting



## Embedding Code in Markdown

If you're writing your code in markdown, the easiest way to embed snippets is to use ["fenced code blocks"][gfm], which also allows syntax highlighting. For examples in practice, see this assemble [boilerplate for markdown projects](https://github.com/assemble/boilerplate-markdown/), in particular take a look at the code in [these templates](https://github.com/assemble/boilerplate-markdown/tree/master/src/templates/pages).

Also see ["A Better Markdown Cheatsheet"](https://gist.github.com/jonschlinkert/5854601).

### Embedding options

#### Inline Code

Wrap inline snippets of code with a backtick before and after the snippet: <code>`code`</code>.


For example, `<section></section>` should be wrapped as "inline".

``` html
For example, `<section></section>` should be wrapped as "inline".
```


#### Block code "fences"

Use "fences"  `` ``` `` to block in multiple lines of code:

<pre>
  <code class="lang-javascript">
```
options: {
  helpers: 'src/helpers/helper-*.js'
}
```
  </code>
</pre>


Renders to this:

```js
options: {
  helpers: 'src/helpers/helper-*.js'
}
```


#### Indented code

For code blocks, as an alternative to backticks you may indent several lines of code by at least four spaces.

```
    // Indent your code like this
    line 1 of code
    line 2 of code
    line 3 of code
```

Renders to this:

    line 1 of code
    line 2 of code
    line 3 of code


### Syntax highlighting

Assemble uses [Marked.js][marked] for processing markdown. "A full-featured markdown parser and compiler, written in javascript. Built for speed". With Marked, you can use GitHub Flavored Markdown or "GFM" ["fenced" code blocks][highlighting] to achieve syntax highlighting with your snippets of code.

To activate it, simply add the file extension of the language you want to use directly after the first code "fence", ` ```js `, and syntax highlighting will automatically be applied in the rendered HTML.


For example, to apply syntax highlighting for JavaScript, you add either `js` or `javascript` after the first fence:

<pre>
  <code class="lang-javascript javascript">
```javascript
grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
};
```
  </code>
</pre>

Which renders to:

```javascript
grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
};
```

**Note** that whenever you embed handlebars templates _and you don't want them to be processed_, you do have to escape them with a backslash, like this: `\{{module-class}}`. Don't forget the close tags (I often do)... This is pretty cool because you can embed templates in your examples that **should be processed** as well. Makes it nice for maintaining documentation.


#### Embedding Code in HTML

Aside from using the  obviously add all of the `<pre>` tags manually as in your example, or you can use the `\{{#markdown}}...\{{/markdown}}` block helper (see [Markdown Helpers](https://github.com/assemble/handlebars-helpers#markdown-helpers) and the Assemble [docs for Markdown](http://assemble.io/docs/Markdown.html)) to wrap sections of markdown inside your HTML:

<pre>
  <code class="lang-javascript javascript">
\{{#markdown}}
``` js
options: {
  helpers: 'src/helpers/helper-*.js'
}
```
\{{/markdown}}
  </code>
</pre>


## Related info

* [Markdown](http://assemble.io/docs/Markdown.html)
* [Markdown Helpers](https://github.com/assemble/handlebars-helpers#markdown-helpers)
* [Helpers][helpers]
* [Custom helpers][custom-helpers]
