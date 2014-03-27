---
title: options.marked

area: docs
section: configuration
---

## options.marked

Assemble uses [Marked.js][marked] for processing markdown. Any options from marked can be defined on the `marked` object in the assemble options. This is an example of using all options:

```js
assemble: {
  options: {
    marked: {
      breaks: false,
      gfm: true,
      highlight: function(code, lang, callback) {
        pygmentize(
          {
            lang: lang,
            format: 'html'
          },
          code,
          function(err, result) {
            callback(err, result.toString());
          }
        );
      },
      langPrefix: 'language-',
      pedantic: false,
      sanitize: false,
      silent: false,
      smartLists: false,
      smartypants: false,
      tables: true
    }
  },
  ...
}
```

_Please visit the [Marked.js][marked] project to learn more about available options._ (the following is from the [Marked.js][marked] readme).

### gfm
Type: `Boolean`
Default: `true`

Enable [GitHub flavored markdown](https://help.github.com/articles/github-flavored-markdown).

### highlight
Type: `Function`

A function to highlight code blocks. The function takes three arguments: `code`, `lang`, and `callback`. The above example uses async highlighting with [node-pygementize-bundled](https://github.com/rvagg/node-pygmentize-bundled), and here is a synchronous example using [highlight.js](https://github.com/isagalaev/highlight.js) which doesn't require the `callback` argument:

```js
options: {
  highlight: function (lang, code) {
    return hljs.highlightAuto(lang, code).value;
  }
}
```

#### highlight arguments
Type: `String`

* `code`: The section of code to pass to the highlighter.
* `lang`: The programming language specified in the code block.
* `callback`: The callback function to call when using an async highlighter.

### tables
Type: `Boolean`
Default: `true`

Enable GFM [tables](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#wiki-tables). This option requires the `gfm` option to be true.

### breaks
Type: `Boolean`
Default: `false`

Enable GFM [line breaks](https://help.github.com/articles/github-flavored-markdown#newlines). This option requires the `gfm` option to be true.

### pedantic
Type: `Boolean`
Default: `false`

Conform to obscure parts of `markdown.pl` as much as possible. Don't fix any of the original markdown bugs or poor behavior.

### sanitize
Type: `Boolean`
Default: `true`

Sanitize the output. Ignore any HTML that has been input.

### smartLists
Type: `Boolean`
Default: `true`

Use smarter list behavior than the original markdown. May eventually be default with the old behavior moved into `pedantic`.

### smartypants
Type: `Boolean`
Default: `false`

Use "smart" typograhic punctuation for things like quotes and dashes.

### langPrefix
Type: `String`
Default: `lang-`

Set the prefix for code block classes.


#### Marked License

Marked Copyright (c) 2011-2013, Christopher Jeffrey. (MIT License). See the Marked.js [LICENSE](https://github.com/chjj/marked/blob/master/LICENSE) and [repo][marked] for more info.

[marked]: https://github.com/chjj/marked "Marked Repo on GitHub"
