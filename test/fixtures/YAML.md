---
title: YAML data

area: docs
section: data

categories: ["data"]
tags: ["yfm", "yaml front matter"]
---

> YAML is a "human-readable data serialization format" that may be used with Assemble as an alternative to JSON

As a data format, YAML may be used as an alternative to JSON.

{{#draft}}
TODO:
* Add examples
* Explain how YAML is used in Assemble

## Data files

TODO...
{{/draft}}

## [YAML front matter][yaml-front-matter]

> YAML front matter was made popular by Jekyll, the "blog-aware, static site generator" that powers GitHub Pages.

YAML front-matter is optionally used at the beginning of a page to define metadata for the page's content. In order for YAML front-matter to be processed, it _must be the first thing at the top of the page_, and it must be "wrapped" properly using three dashes above (`---`) and three below (`---`).

### More information

* Go to the [YAML front matter][yaml-front-matter] page.
* See some great usage examples in assemble's [YAML test files](https://github.com/assemble/assemble/tree/master/test/actual/yfm)

> Visit [http://www.yaml.org/](http://www.yaml.org) to learn more →


{{#draft}}

## [js-yaml options][]
Assemble uses [js-yaml][] for parsing and stringifying YAML data.

<span class="warning">Heads up! These options are being reworked and may not be available at time of reading. if you have questions, please feel free to create an issue.</span>

The following options may be defined in `assemble.options` at the task or target level:

### filename
Type: `String`
Default: `null`

String to be used as a file path in error/warning messages.

### strict
Type: `Boolean`
Default: `false`

Forces the loader to throw errors instead of warnings.

### schema
Type: `String`
Default: `DEFAULT_SCHEMA`

Specifies a schema to use.

***

> Visit the [js-yaml][js-yaml] repo for more information →


## [js-yaml](https://github.com/nodeca/js-yaml)

[js-yaml](https://github.com/nodeca/js-yaml) is a JavaScript library used by Assemble for parsing YAML and YAML Front-Matter.
{{/draft}}


[js-yaml]: https://github.com/nodeca/js-yaml