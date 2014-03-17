---
title: Why Assemble?

area: docs
section: getting started

published: false
---

> As a _site generator_, Assemble was designed to do orders of magnitude more than just "render templates". However, if all you need is to generated templates, it can't get much easier than Assemble.



To demonstrate what assemble can do, take a look at some [examples][2].

A few reasons to try assemble:

* Inits/generators and boilerplates to use
* Documentation and actively supported
* Node.js/JavaScript alternative to Jekyll
* Full-featured site generated based on Grunt.js
* Easily deploy static sites to gh-pages (link to init and boilerplates)
* Grunt.js based, so you can use Assemble to build your site, and fill in any gaps in your build process with other grunt plugins.
* `npm install assemble` and be running in a couple of minutes.
* Assemble let's you use any combination of the following as data sources for your templates: [JSON][json] files, [YAML][yaml] files, [YAML front-matter][yaml-front-matter], and even custom properties in the `assemble` task or target options.
* Methods to the [assemble object][3] can be used for creating custom **[build "steps"][methods]**
* Built-in [variables][built-in-variables] and [helpers][helpers] for generating [sitemaps][sitemap], collections of pages, categories, tags, archives, or even custom collections and collection items.
* Assemble's [helper library](https://github.com/assemble/handlebars-helpers) is pretty awesome, which we externalized and generalized to a project called [handlebars-helpers][4], which now includes somewhere around 100-110 helpers. You will get a better sense of the "unique" helpers we provide by checking out the code in handlebars-helpers (either the coffeescript source files or generated javascript in the lib folder), or the [helper examples](https://github.com/assemble/handlebars-helpers-examples).
* You can build or omit specific pages using the various [src-dest configurations](http://gruntjs.com/configuring-tasks#files) offered from Grunt.js, and use as many targets as you need to build your site.
* [Layouts][layouts] can optionally be used to "wrap" pages with common code, such as a `<head>`, footer, scripts and stylesheets.
* [Partials][partials] can be used to include reusable code fragments. Useful for UI abstractions (e.g. "components" or "modules") or for snippets of code like the script for Google Analytics.
* The way assemble handles [templates-overview][templates-overview] and [data/metadata][data] is pretty powerful. You can, for instance, create a big library of partials, then create a bunch of `[name].json` or YAML data files that have the same names as the partials. Then just add the paths to the data files and partials in the assemble task and/or target options, and when you run `grunt assemble` any partials that are used anywhere in your pages will automatically be registered, and context will be appropriately applied.
* Let's say you're building a website/webapp that includes a bunch of UI components, like Bootstrap's LESS components. you could use assemble to not only build your pages, but also your documentation - and part of the live application - from the same source files. In a nutshell, in the assemble task you would set up one or more targets for building "static pages", then for your docs you could create another target where you could either build each partial (component) into a page of its own, or multiple partials per page, or both - or however you want to do it.
* Assemble wants to be the best task for generating pages from templates and data. Being based on Grunt.js means that Assemble is just another plugin. At the end of the day, pages are just a part of your project, so you can surround Assemble with any other plugins you need from the Grunt.js community, or custom plugins, to fill in whatever gaps still exist in your build process. In other words, we have no need or motivation to try to bundle in everything you can think of. So no need for this: "Assemble concats, minifies, shreds, dices, slices and does your taxes". You can use whatever plugin you think is best to accomplish each one of those tasks.
* Assemble is open source. We're just a couple of nerds that decided to do this on our own time, completely for fun, because we love doing it. Plus, we use Assemble on our own projects every day so we understand how it's being used and what could be done to improve it.


## Guiding philosophies

1. Leverage native [Grunt.js](http://gruntjs.com) functionality wherever possible, whenever practical
2. Try to focus on generalizing utliity functionality. This makes Assemble more flexible and keeps us from being hard-coded to a specific use case as we found with other site builders. However, we need to have conventions for things that can be generalized, such as the various means of accessing data, exposing options and methods and so on. We're just not big fans of "you can use as many includes (partials) as you want, as long as they're all in a special folder called 'includes', and with an underscore in front of it just to make absolutely sure that we know it's for includes, so call it '_includes'".Being built on top of Grunt gets us around these kinds of silly restrictions pretty easily. You can stick partials in as many directories as you want, just tell Assemble where they are in the task or targets. Same goes for data, pages, layouts, and even custom helpers - which are just like the "filters" used in Jekyll.
3. We use it, use it, use it... a lot. We try to break it as often as possible. And we use it constantly on projects that matter to us, so we're always motivated to fix it. This works.

{{#draft}}
## Use cases

* "I just want to generate templates, I don't need a _site generator_"
* "I need a personal blog"
* "I need to build the gh-pages for my GitHub project"
{{/draft}}

[sitemap]: https://github.com/assemble/assemble-boilerplate-sitemap
[1]: http://github.com/assemble/assemble
[2]: https://github.com/assemble/assemble-examples
[3]: https://github.com/assemble/assemble/blob/master/docs/docs-methods.md
[4]: https://github.com/assemble/handlebars-helpers