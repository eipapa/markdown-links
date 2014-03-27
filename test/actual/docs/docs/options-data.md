---
title: options.data

area: docs
section: configuration
categories:
- options
tags:
- data
- yaml
- json
- yfm
---


### Also see [data types][data] →

{{#draft}}

## Usages Examples

* Pass configuration data to Grunt/Assemble
* Pass metadata to templates
* Pass content to files
{{/draft}}


## Supplying data to templates

You must first define the paths to any data files you wish to use via the `options.data` object in the `assemble` task or target, then Assemble will automatically supply data to your templates:

```js
assemble: {
  options: {
    data: 'src/data/*.json'
  },
  files: {
    'site/': ['src/pages/*.hbs']
  }
}
```

### Matching names

When using "external" data files (versus YAML front matter), _if name of the data file is the same as the associated template_ then Assemble will automatically associate the two files.

**"widget component" example**

Given a data file, such as `widget.json` or `widget.yml` :

```json
{
  "name": "This is a square widget",
  "modifier": "widget-square"
}
```

With the following Handlebars expressions in out template, `widget.hbs`:

```html
<div class="widget \{{ widget.modifier }}">\{{ widget.name }}</div>
```

The result after running `grunt assemble` will be:

```html
<div class="widget widget-square">This is a square widget</div>
```

**package.json example #1**

Add `package.json` to the `data` object:

```js
assemble: {
  myProject: {
    options: {
      data: 'package.json'
    },
    files: {
      'dest': ['src/templates/**/*.hbs']
    }
  }
}
```

And we will now be able to retrieve metadata from `package.json` by using variables such as:

* `\{{package.verson}}`
* `\{{package.name}}`
* `\{{package.description}}`
* `\{{package.author.url}}`
* `\{{package.author.name}}`



**package.json example #2**

Assuming we add the following code to our Gruntfile

```js
pkg: grunt.file.readJSON('package.json'),

assemble: {
  myProject: {
    options: {
      pkg: '<%= pkg %>',
      data: 'other/data/*.json'
    },
    files: {
      'dest': ['src/templates/**/*.hbs']
    }
  }
}
```

We can now use the following variables in our templates:

* `\{{pkg.verson}}`
* `\{{pkg.name}}`
* `\{{pkg.description}}`
* `\{{pkg.author.url}}`
* `\{{pkg.author.name}}`


> Also see: [YAML front matter][yaml-front-matter]


## Related Info

* [Complete list of Options][Options]
* [Data Types][data]
* [variables][built-in-variables]

