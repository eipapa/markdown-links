---
title: Idiomatic Templates

area: docs
section: templates

published: false
---

# Introduction

> Assemble is a Grunt.js plugin that makes it dead simple to render pages from templates, layouts, content, partials, and data.

For example:



Keywords and phrases:
* web components
* separation of concerns
* Modular
* Encapsulated
* Build re-usable components
* Better engineering practices
* Clear conventions, flexible terminology
* Object-oriented

Better engineering practices and

Clear and understandable conventions for building


> Assemble offers conventions for building modular, re-usable web components, and strategies for resolving the bottleneck between designers and developers.

Positioned with Web Components.


## Challenges

Lack of DOM encapsulation, leading to:
* Collision of DOM contents (ID collision)
* Broken styles
* Unexpected JavaScript behavior

Libraries work around these problems by following certain assumptions and conventions

## Modularize the Web

MV* frameworks help us to some extent

* Organize the complexity
* Separate contents from the presentation layer
* Define Templates / views
* Associate a model with the view
* Monitor the model for changes and update the view (Data binding)
* Does it solve all the problems? Lets see.



### The templates of today

**Method #1**: "offscreen" DOM using [hidden] or display:none

``` html
<div id="mytemplate" hidden>
  <img src="logo.png">
  <div class="comment"></div>
</div>
```
* We're working directly w/ DOM.
* Resources are still loaded (e.g. that `<img>`)
* Other side-effects like URLs not being fully composed yet.
* Style and theming is painful.
  - Embedding page must scope all its CSS to `#mytemplate`.
  - No guarantees on future naming collisions.

**Method #2**: manipulating markup as string. Overload `<script>` :

``` html
<script id="mytemplate" type="text/x-handlebars-template">
  <img src="logo.png">
  <div class="comment"></div>
</script>
```

* Encourages run-time string parsing (via .innerHTML)
  * may include user-supplied data → XSS attacks.

_Examples_: `handlebars.js`, John Resig's micro-template script


### Encapsulation

* Fundamental foundation of OOP
* Separates code you wrote from the code that will consume it
* We _don't have it on the web_!
* Well, sort of: `<iframe\>`. `<iframe\>` are heavy and restrictive. ★ [Seamless iframe](http://benvinegar.github.com/seamless-talk)


## Web Components

* `<\template>` : inert chunks of clonable DOM, which can be activated for later use.
* custom elements: create new HTML elements to expand HTML's existing vocabulary, and extend existing DOM objects with new imperative APIs
* shadow DOM: building blocks for encapsulation & boundaries inside of DOM

### Defining Web Components

_Supporting Cast_

* Style encapsulation
* Knowledge into app's state
* DOM changes: `MutationObserver`
* Model changes: `Object.observe()`
* CSS variables, `calc()`

_A collection of new capabilities in the browser_


### Web components - Templates

Templating of the near future
`<\template>`

Contains inert markup intended to be used later:
``` html
<template id="mytemplate">
  <img src="">
  <div class="comment"></div>
</template>
```
1. We're working directly w/ DOM again.
2. Parsed, not rendered

`<script>`s don't run, images aren't loaded, media doesn't play, etc.


### Web components - [Shadow DOM](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/shadow/index.html)

Shadow DOM is complex! Let's cover the basics:

* Concept of Shadow DOM
* Creating Shadow DOM
* Insertion Points
* Styling
* encapsulated styles & shadow boundaries
* styling hooks: using CSS variables
* @host at-rule


#### Turns out...

* DOM nodes can already "host" hidden DOM.
* It can't be accessed traversing the DOM.

_So...browser vendor's have been holding out on us!_

**Shadow DOM**: exposes the same internals browser vendors have been using to implement their native controls, to us.

[Attaching Shadow DOM to a host](http://slides.varunkumar.me/webcomponents/images/shadow/shadow-trees.svg)




---



