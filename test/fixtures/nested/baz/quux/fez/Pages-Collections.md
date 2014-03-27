---
title: Pages Collections

area: docs
section: templates
---


## Collections of Pages

### Rendering Collections of Pages

Let's say we create a project with the following structure:

```
src/
  layouts/default.hbs
  docs/
    index.hbs
    api.hbs
    cheatsheet.hbs
  posts/
    index.hbs
    articles.hbs
    projects.hbs
    about.hbs
    contact.hbs
```

Now in the Gruntfile, we configure the `assemble` task with two [targets][targets] and a [layout][layouts]:

```javascript
assemble: {
  options: {
    layout: 'layouts/default.hbs'
  },
  docs: {
    files: {
      'docs/': ['src/docs/pages/*.hbs'],
    }
  },
  blog: {
    files: {
      'blog/': ['src/blog/posts/*.hbs'],
    }
  }
}
```

Inside our [layout][layouts], `default.hbs`, we will add the `pages` variable to the `\{{#each}}` block expression, and inside the block we will add the [`\{{basename}}`][helpers] variable to give us the filename of each page, without the extension.

```handlebars
<ul>
  \{{#each pages}}
    <li><a href="#">\{{basename}}</a></li>
  \{{/each}}
</ul>
```

When we build the project, pages from the `docs` target will render with:

```html
<ul>
  <li><a href="#">index</a></li>
  <li><a href="#">api</a></li>
  <li><a href="#">cheatsheet</a></li>
</ul>
```

When we build the project, and pages from the `block` target will render with:

```html
<ul>
  <li><a href="#">index</a></li>
  <li><a href="#">articles</a></li>
  <li><a href="#">projects</a></li>
  <li><a href="#">about</a></li>
  <li><a href="#">contact</a></li>
</ul>
```

## \{{#each pages}} Usage Examples

Let's say our target has two pages with the following content:

Page #1: `src/templates/one.hbs`

```html
<ul>
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
</ul>
```

Page #2: `src/templates/two.hbs`

```html
---
title: Home
---

<h1>\{{title}}</h1>
```


#### \{{page}} variable

The following templates:

```handlebars
\{{#each pages}}
  \{{{page}}}
\{{/each}}
```

will return the concatenated "content" of each page in the target, with YFM stripped from each page, and templates returned _unrendered_:

```handlebars
<ul>
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
</ul>

<h1>\{{title}}</h1>
```


#### \{{src}} variable

The following templates:

```handlebars
\{{#each pages}}
  \{{{src}}}
\{{/each}}
```

will return the `src` path of each page in the target:

```html
src/templates/one.hbs
src/templates/two.hbs
```


#### Using YFM with the `page` variable

With a couple of simple modifications to the previous example, we can have the output reflect the `title` of each page instead of the file name. To do so, each page must actually have a "title". So let's add a `title` property to the YAML front matter of each page:

```yaml
---
title: Home
---
```

Next we will modify our template to use the `title` variable instead of the file name. Since we cannot use the context of each page as the first path ([see "Data, Context and Why it Works this Way"](#data-title-explanation)), to make sure we get the correct `title` we must add the `data` variable, giving us access to the root of the context:

```handlebars
<ul>
  \{{#each pages}}
    <li><a href="#">\{{data.title}}</a></li>
  \{{/each}}
</ul>
```
or this:

```html
<ul>
  \{{#each pages}}
    \{{#data}}
    <li><a href="#">\{{title}}</a></li>
    \{{/data}}
  \{{/each}}
</ul>
```

renders to:

```html
<ul>
  <li><a href="#">Home</a></li><!-- text is now "home" instead of "index" -->
  <li><a href="#">Blog</a></li>
  <li><a href="#">Projects</a></li>
  <li><a href="#">About Us</a></li>
  <li><a href="#">Contact Us</a></li>
</ul>
```

## Pages per Collection Item  <a id="pages-per-collection-item" name="pages-per-collection-item" class="anchor"><span class="glyphicon glyphicon-link"></span></a>

To get a list all of the pages in a given target with certain tag, such as `foo`, we would "wrap" the `\{{#each tags}}...\{{/each}}` block around the `\{{#each pages}}...\{{/each}}` block, like this:

```html
\{{#each tags}}
  \{{#is tag "foo"}}
  <h1>\{{tag}}</h1>
  <ul>
    \{{#each pages}}
      <li>\{{data.title}}</li>
    \{{/each}}
  </ul>
  \{{/is}}
\{{/each}}
```

Also see [collections][collections].


{{#draft}}

## Data, Context and Why it Works this Way

### Why `\{{data.title}}`?

> "we cannot use the context of each page as the first path..."

Remember this passage from the previous section?

This means that _we need to get the `title` of **each page** without having to write out the **context of each page**_. The reason the `\{{#each}}` expression exists to avoid having to do this kind of thing (and more). However, although this isn't supported (for good reason), if we were to explicitly use the context of each page it might look something like this:

```html
<ul>
  <li><a href="#">\{{index.title}}</a></li>
  <li><a href="#">\{{blog.title}}</a></li>
  <li><a href="#">\{{project.title}}</a></li>
  <li><a href="#">\{{about.title}}</a></li>
  <li><a href="#">\{{contact.title}}</a></li>
</ul>
```

### Why not just `\{{title}}` then?

```html
<ul>
  \{{#each pages}}
    <li><a href="#">\{{title}}</a></li>
  \{{/each}}
</ul>
```

The first reason is that their might be a `title` property on the very same page as the templates. We need to make sure that Assemble knows to get the title from all pages in the "current" collection (collections are limited to items included by the [current target]()).  `\{{title}}` The `\{{#each}}`




NOTE: If you're reading this unpublished content, know that these features haven't even been released. So it's probably best to _not_ try to use them ;-) Sorry.

# Pages

## Defining a Page

Each page consist of the following objects:

 * [Metadata](): aside from `<title>Page Title</title>`, in this project `metadata` means more than "meta tags", it also refers to information that might be recorded somewhere on a web page such as _time and date_, _creator_ or _author_ and so on.
 * [Content](): among other things, _content_ is the text, images, sounds, videos or animations that a page might contain, including even the [microcopy]() used inside buttons, tags and labels, or other similar elements.
 * [Layout]():

When a page is defined, all objects are optional except for the page `<title></title>`. In addition, when certain objects are excluded, any available defaults will be used in their place.

The simplest way to define a new page is to add a `page.json` file in the following directory `./src/templates/pages/custom/`, and add a single property to declare the

```json
{
  "home": {}
}
```

Sensible defaults are provide for common global properties, so that if you need to quickly scaffold a project you can do so without having to fill out an entire config file.

```json
{
  "home": {
    "title": "Home"
  }
}
```

then the page would compile with the file name `home.html`. So if we want the page's file name to be `index.html`, we woud add that to the `home` object:

```json
{
  "home": {
    "title": "Home",
    "filename": "index",
    "content": "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
  }
}
```

YAML front matter is also processed:

```html
---
title: Snow crabs are swarthy and devious criminals.
subtitle: A true and captivating tale of how a band of ingenious snow crabs successfully robbed the Bank of New York.
author: Jon Schlinkert
category: Breaking news
layout: featured-article
---
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
```
```json
{
  "home": {
    "title": "Home",
    "filename": "index",
    "layout": "path/to/layout.json",
    "masthead": "A beautiful, responsive theme. By <%= theme.author %>",
    "content": [
      "path/to/content1.md",
      "path/to/content1.md",
      "path/to/content2.md"
    ],
    "variables": {
      "hero": "This is an awesome theme!",
      "buy-now": "Buy Now!"
    }
  }
}
```
Or the same in YAML:

```yaml
home:
  title: "Home"
  filename: index
  layout: path/to/layout.json
  masthead: A beautiful, responsive theme. By <%= theme.author %>
  content:
  - path/to/content1.md
  - path/to/content1.md
  - path/to/content2.md
  variables:
    hero: This is an awesome theme!
    buy-now: Buy Now!
```

## Collections of pages

A collections of pages is defined like this:

```json
{
  "about": {
    // properties
  },
  "contact": {
    // properties
  },
  "blog": {
    // properties
  },
  "post": {
    // properties
  }
}
```

json

```json
{
  "pages": "path/to/pages.json",
}
```

YAML

```yaml
pages: path/to/pages.json
```
1. Create a `pages.json` file and add an object for each page to be built:


Add the `pages` object "short-format" to your configuration file, and create sub-objects for each page to be built.

```json
{
  "pages": {
    "home": "path/to/custom/home.json",
    "about": "path/to/custom/about.json",
    "blog": "path/to/custom/blog.json",
    "contact": false
  }
}
```

To exclude a page simple provide a falsy value. The same goes for excluding `layouts` or other default values.


Add the `pages` object "long-format" to your configuration file, and create sub-objects for each page to be built.

```json
{
  "pages": {
    "home": {
      "title": "Home",
      "masthead": "A beautiful, responsive theme. By <%= theme.author %>",
      "slug": "index",
      "layout-example1": "<%= defaults.layouts.home %>",
      "layout-example2": "path/to/home-page-layouts/carousel.hbs",
      "content-example": "path/to/home.md", // content can be a single path, array or globbing patterns
      "content": [
        "content1.md",
        "content1.md",
        "content2.md"
      ]
    },
    "about": {
      "title": "About Us",
      "slug": "about",
      "layout": "path/to/layouts-type1/full-width.hbs",
      "content": "path/to/about-us.md"
    },
    "contact": {
      "title": "Contact Us",
      "slug": "contact",
      "layout": "path/to/layouts-type1/full-width.hbs",
      "content": "path/to/contact-us.md"
    },
    "blog": {
      "title": "Blog",
      "subtitle": "Welcome to our Blog!",
      "slug": "blog",
      "layout": "path/to/layouts-type1/two-column.hbs",
      "content": "path/to/contact-us.md"
    },
    "post": {
      "title": "\{{ page.title }}",
      "slug": "<%= grunt.template.today(\"yyyy\")-<%= post-name %>",
      "layout": "path/to/layouts-type4/two-column.hbs",
      //"content": "<%= theme.content %>" // the 'content' object in the theme.json file, might reference content.md
      "content": "path/to/post.md"
    },
    "article": { // alternative to 'post'
      "title": "Example Blog Post",
      "subtitle": "The most important blog post you've ever read.",
      "slug": "example-blog-post",
      "layout": "<%= defaults.layouts.blog %>",
      "content": "path/to/post.md"
    },
    "catalog": {
      "title": "Products",
      "slug": "products",
      "layout": "path/to/layouts-type2/gallery.hbs",
      "content": "<%= products %>/products.yml"
    },
    "product": {
      "title": "\{{ page.title }}",
      "slug": "products",
      "layout": "path/to/layouts-products/product-example.hbs",
      "content": "<%= products %>/product-types1/product.yml"
    },
    "portfolio": {
      "title": "Our Work",
      "layout": "../../layouts/my-custom-layouts/portfolio.hbs"
    }
  }
}
```

{{/draft}}