---
title: options.collections

area: docs
section: configuration
---
## Default Collections

The following built-in collections are available at the root of the context:

| **Collection** | **Collection item** | **Description**                |
| -------------- | ------------------- | ------------------------------ |
| `tags`         | `tag`               | Used to specify tags associated with the current page. Multiple tags may be associated with each page. Useful for adding semantic **tags** or tag clouds to your content. |
| `categories`   | `category`          | Used to specify categories associated with the current page. Multiple categories may be associated with each page. Similar to tags but more appropriate for categorizing pages by "broader" concepts. |
| `pages`        | `page`              | See [Pages collection differences](#pages-collection-differences) below |


### Pages collection differences

"[Pages][pages]" and "page" differ from other collections and collection items in the following ways:

* _Any files specified in the `src` of a given target_ will be the collection items associated with the "pages" object for that target.
* Although a "page" is a collection item, there is currently no concept of "pages with related pages". In other words _there is no object which contains a collection of pages associated with a given page_.


### Collection items

You may then add items to collections in the YAML front matter of any files that should include those collections:

```yaml
---
title: My Blog
widgets:
- one
- two
- three
---
```

### Collections Options

#### Implemented

* `name:`: the name of the collection, plural form
* `inflection`: the name of an individual collection item, in **singular** form
* `sortorder`: direction in which to sort the collection. Accepted values are (case insensitive): `asc`|`ascending`, `desc`|`descending`.
* `sortby`: you may sort the collection by any field available in the page's data context

#### Planned

* `index`: the template to use for generating an index page for the collection, such as: `src/templates/indices/archives.hbs`.

```js
options: {
  collections: [
    {
      // Collection options
      name: 'items',
      inflection: 'nav-item' // singular form
    },
    {
      name: 'archives',
      inflection: 'post' ,
      sortorder: 'ascending', // or any of the following ['asc', 'desc', 'descending'] upper or lower case
      sortby: 'datetime',
      index: 'src/templates/indices/archives.hbs'
    }
  ]
}
```

### List of associate pages

Additionally, any collection item from the `collections` object can list the [pages][pages] associated with that collection. For example, each "tag" would list the [pages][pages] associated with that tag.

```javascript
{
  tag: 'news',
  pages: ['one.html', 'two.html', 'three.html']
}
```

## Custom collections

### options.collections

type: `Array`
default: `null`

Custom `collections` may be defined using the `collections` option:


```javascript
assemble: {
  options: {
    collections: ['widgets', 'posts']
  }
}
```

And then in the YAML front matter of a page:

{{! TODO: Update these examples per this discussion https://github.com/assemble/assemble/issues/216 }}

```yaml
---
widgets:
- one
- two
- three
---
```

There are no restrictions on the number of collections created, you may specify as many custom collections as you require.


### Automatic inflection
Currently, for the sake of ease of use, the collection method uses the [inflection](https://github.com/dreamerslab/node.inflection) library to convert a collection's item key into the correct syntax:

* `tags` converts to: `{ tag: 'ficus', pages: [] }`
* `categories` converts to: `{ category: 'trees', pages: [] }`

If words you wish to use are either missing or don't work properly, please let us know by [creating an Issue](https://github.com/assemble/assemble/issues/) on Assemble's GitHub repository.


## Usage examples

Declaring tags and categories for a page within the page's [YAML front matter][yaml-front-matter]

``` yaml
---
tags:
- feature
- priority
categories:
- open
---
```

**List all tags**

```handlebars
<ul>
  \{{#tags}}
  <li><a href="/tag/\{{tag}}.html">\{{tag}}</a></li>
  \{{/tags}}
</ul>
```

**List all categories**

```handlebars
<ul>
  \{{#categories}}
  <li><a href="/category/\{{category}}.html">\{{category}}</a></li>
  \{{/categories}}
</ul>
```

**List tags on current page**

```handlebars
<ul>
  \{{#page.tags}}
  <li>\{{.}}</li>
  \{{/page.tags}}
</ul>
```

**List categories on current page**

```handlebars
<ul>
  \{{#page.categories}}
  <li>\{{.}}</li>
  \{{/page.categories}}
</ul>
```


{{#draft}}
Given we have a `tag` named `updates`:

```handlebars
\{{#tags.updates.pages}}
  \{{this.data.title}}
\{{/tags.updates.pages}}
```


### Collections options

The following collections options are under consideration and have not been implemented:

* `content`: returns the content of the given page in the collection.
* `excerpt`: returns an excerpt of the content of the given page in the collection.
* `include` / `exclude`
* `next`
* `previous`

### Excluding Pages

Pages can be excluded from a "collection" by adding `published: false` to the YAML front-matter of that page.
{{/draft}}