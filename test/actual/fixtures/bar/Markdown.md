---
title: Markdown

area: docs
section: content

categories:
- content
- markdown
tags:
- content
- converters
- markdown
- HTML
---

> With Assemble you can use markdown however you want, wherever you want

An advantage of writing content with markdown is that it is free from the angle brackets and tags used in HTML, so it feels and looks more like "content" than "code".

With Assemble you can:

* Write entire documents in markdown, and choose where and when to compile them to HTML
* Write document fragments in markdown, so they can be "included" or used as partials within other larger documents
* Write sections of markdown directly inside HTML documents (referred to as "inline markdown")


### "Include" extenal content
Use the markdown expression, `\{{md}}`, to enable importing of external markdown content.

**Example #1: using full path**

```handlebars
\{{md ../path/to/content.md}}
```

**Example #2: using variables**
Or use a variable instead of setting the path directly inside the template. For example you can add the content variable to the [YAML Front-Matter](https://github.com/assemble/assemble/wiki/YAML-Front-Matter):

```yaml
---
page:
  title: Home
content: ../path/to/content.md
---
```

then use it like this:

```handlebars
\{{md content}}
```

### Markdown "includes"

Using the `\{{md}}` markdown helper, you can import markdown formatted content from another file, and render it to HTML. For example:

Assuming we have a file named `index.hbs`, and we add the following:

```handlebars
\{{md '../path/to/content.md'}}
```

And give that `content.md` contains the following:

```markdown
# Getting Started
Lorem Ipsum...
```

When we run `grunt assemble`, a file named `index.html` will be rendered containing:

```html
<h1>Getting Started</h1>
Lorem Ipsum...
```

The same can be accomplished by specifying the path to the file in the YAML Front Matter:

```handlebars
---
content: ../path/to/content.md
---

\{{md content}}
```

### Markdown block expression

The `\{{#markdown}}...\{{/markdown}}` block expression is used to "wrap" markdown content that is written "inline" directly inside HTML documents:

```markdown
<h1> My Site </h1>

\{{#markdown}}
## Inline Markdown is awesome

> this is markdown content

* useful for simple content
* great for blog posts
* easier on the eyes than angle brackets
* even links look prettier

### Pretty links

[Visit Assemble](http://github.com/assemble/assemble)

### Even Prettier links

Embed handlebars templates to make them even prettier.

\{{#page.links}}
[\{{text}}](\{{href}})
\{{/page.links}}

\{{/markdown}}

```

In a layout, can also wrap the `\{{> body }}` tag with the `\{{#markdown}}...\{{/markdown}}` block helper to convert any HTML pages that use that layout to markdown:

```handlebars
\{{#markdown}}
  \{{> body }}
\{{/markdown}}
```

## Related Information

* [options.marked][options-markded]