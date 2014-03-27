---
title: Data

area: docs
section: data
---

> Mix and match JSON, YAML, YAML front matter, and data stored in the Gruntfile however you want.


{{#draft}}
## TODO

Cover:
* how data is merged at task/target levels
* lo-dash templates
* yfm
* .yml/.json
* How large data files will slow down the build
{{/draft}}

## Data Formats

Any of the following data formats may be used:

* [JSON][json] files, such as `my-data.json`
* [YAML][yaml] files, such as `my-data.yml`
* [YAML Front-Matter][yfm], embedded directly inside the page/template itself

> Go to [options.data][options-data] to learn about supplying data to your templates →

## Usage examples

Let's start by creating a template, which can be any kind of markdown, text, xml or markup/HTML that we want to use. For this example our template is going to be HTML, and since I'm feeling creative let's call it `my-template.hbs`.

Now, focusing only on the `head` of our HTML document, let's add template variables for `title` and `author` so that we can later replace them with real data:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>\{{title}}</title>
    <meta name="author" content="\{{author}}">
  </head>
  <body>
  </body>
</html>
```

Handlebars.js is the default template engine in Assemble, so our variables are wrapped in "Handlebars expressions": `\{{` and `}}`.

### JSON example

Here is an example of what we might put inside of `my-template.json` to populate our template with data.

```json
{
  "title": "Assemble",
  "author": "Brian Woodward"
}
```
### YAML example

Here is the same in YAML format: `my-template.yml`

```yaml
title: Assemble
author: Brian Woodward
```

And this template:

`my-template.hbs`

```html
<h1>\{{ title }}</h1>
```

### YAML front-matter example

Or, in cases where we only require simple metadata we can use YAML Front-matter to eliminate the need for an external data file:

```html
---
title: Assemble
author: Brian Woodward
---

<h1>\{{ title }}</h1>
```

Outputs:

```html
<h1>Assemble</h1>
<p>Brian Woodward</p>
```

### Underscore and [YAML front-matter][yaml-front-matter]

Furthermore, we can optionally use underscore templates in the YAML front-matter to translate external variables into data inside the content:

```html
---
title: <%= some.title.variable %>
author: <%= some.author.variable %>
---

<h1>\{{ title }}</h1>
<p>\{{ author }}</p>
```

## The "data" Object


Using `data.json` or `data.yml` should work, but works a little bit differently than if you put data into a file called `myData.json`. When the data is in `data.json`, it's loaded directly into the root of the context...

`data.json`:

```json
{
  "title": "My Title"
}
```

`myTemplate.hbs`:

```html
\{{title}}
```

When used in `myData.json`, the data can be accessed through the name of the file...

`myData.json`:
```json
{
  "title": "My Title"
}
```

`myTemplate.hbs`:

```html
\{{myData.title}}
```


## Related information:

* [options.data][options-data]
* [Complete list of Options][Options]
* [Context][context]
* [templates-overview][templates-overview]
* [Variables][built-in-variables]
{{#draft}}* [Idiomatic Data][]{{/draft}}


