---
title: External Libraries
shortname: libs

area: docs
section: development
---
> "Thank you!" to the creators and contributors of these amazing libraries. Our projects are easier to maintain because of you!
> — Assemble Team


## [Grunt.js](http://gruntjs.com)

> The JavaScript Task Runner

Assemble wouldn't exist without Grunt.js.

The advantage of building Assemble on top of Grunt, is that the Grunt ecosystem is already well established, popular, and includes hundreds if not thousands of plugins to choose from. So if you use Assemble for generating sites, components, or other [templates-overview][], you can use any other Grunt.js plugin to automate virtually any other part of your build with very little effort.

Not to mention, if there isn't already a plugin that does what you need, it's really easy to create and publish your own!


## [Handlebars](http://handlebarsjs.com/)

> Handlebars provides the power necessary to let you build semantic templates effectively with no frustration.

Handlebars is the default template engine that ships with Assemble. In their own words:

_Handlebars.js is an extension to the Mustache templating language created by Chris Wanstrath. Handlebars.js and Mustache are both logicless templating languages that keep the view and the code separated like we all know they should be._


## [Handlebars Helpers][handlebars-helpers]
More than **110 Handlebars helpers** from [handlebars-helpers][] are included by default, so they are all available for use anywhere in your [templates-overview][]. Most of the helpers in [handlebars-helpers][] can be used with any Handlebars project, but some of them were created specifically for use with Assemble.

Here are just a few examples:

* **pagename**: Returns the full-name of a given file. Usage: `\{{filename "docs/toc.md"}}` would return: `toc.md`.
* **basename**: Returns the basename of a given file. Usage: `\{{basename "docs/toc.md"}}` would return: `toc`
* **relative**: Returns the derived relative path from file A to file B. Usage: `\{{relative "file/a" "file/b"}}`. This can also be used with the `page` and `pages` variables.
* **markdown**: Markdown block helper enables writing markdown inside HTML and then renders the markdown as HTML inline with the rest of the page. Usage: `\{{#markdown}}\{{/markdown}}`
* **md**: Markdown helper used to read in a file and inject the rendered markdown into the HTML. Usage: `\{{md 'file/to/include.md'}}`
* **embed**: Embeds code from an external file as preformatted text. The first parameter (required) takes a path to the file you want to embed. The second parameter (optional) allows forcing syntax highlighting for a specific language. Usage: `\{{embed 'path/to/file.js'}}` or `\{{embed 'path/to/file.hbs' 'html'}}`
* **gist**: Similar to `\{{embed}}` but for GitHub Gists.

> Go to [handlebars-helpers][] for a comprehensive list, or [Helpers][helpers] to learn about Assemble-specific helpers →


## [Lo-Dash Methods](http://lodash.com/)

> A low-level utility library delivering consistency, customization, performance, and extra features.

The [Lo-Dash](http://lodash.com/) library, exposed by Grunt.js, offers a number of powerful object, array, function, and collections utility methods (and more). Visit the [Grunt.js docs](http://gruntjs.com/) to learn more about using Lo-Dash templates with Grunt.js.


## [Underscore String][underscore-string]

> String manipulation extensions for Underscore.js javascript library.

Underscore.string offers dozens of really useful string utility methods. From the [Grunt.js docs][grunt-util]: "Note that Underscore.string is mixed into grunt.util._ but is also available as grunt.util._.str for methods that conflict with existing Lo-Dash methods." Please [visit the Grunt.js documentation][grunt-util] to learn more.

Here is a preview of the methods available from [Underscore.string][underscore-string]:

* `<%= _.capitalize(title) %>`
* `<%= _.humanize(title) %>`
* `<%= _.numberFormat(123456789.123, 5, '.', ',') %>` => "123,456,789.12300"
* `<%= _.clean(' foo    bar   ') %>` => "foo bar"
* `<%= _.unescapeHTML('&lt;div&gt;Blah blah blah&lt;/div&gt;') %>` => "`<div>Blah blah blah\</div>`"

> Visit [Underscore.string][underscore-string] to learn more →


## [marked]()

> A full-featured markdown parser and compiler, written in javascript. Built for speed.

Assemble uses [Marked.js][marked] for processing markdown.

Marked Copyright (c) 2011-2013, Christopher Jeffrey. (MIT License). See Marked [LICENSE](https://github.com/chjj/marked/blob/master/LICENSE) and [repo][marked] for more info.

[marked]: https://github.com/chjj/marked "Marked Repo on GitHub"


## [js-yaml]()

> JavaScript YAML parser and dumper. Very fast.



[grunt-util]: http://gruntjs.com/api/grunt.util#grunt.util._
[underscore-string]: https://github.com/epeli/underscore.string
[handlebars-helpers]: https://github.com/assemble/handlebars-helpers "A large collection of useful handlebars helpers."