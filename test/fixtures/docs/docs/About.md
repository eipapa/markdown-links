---
title: About

area: docs
section: getting started
---
> Assemble was created by [@jonschlinkert](https://github.com/jonschlinkert) and [@doowb](https://github.com/doowb) to get designers and developers on the same page.

## What you won't find in Assemble


### "Blog awareness"

Which really means "if you put your posts in a specific folder, and you name it exactly as required, then the parser will find your posts and render them into a blog". But Assemble isn't worried about what you put where, or where you go and how late you'll be out. You're a semi-responsible very bearded adult, you should be able to make your own decisions. Bottom line: Assemble is "beard aware". Wait... Assemble helps you make choices about your beard. Nevermind...

### Special required _folders

You won't find a requirement for directories like `_layouts`, `_posts` or `_anything-else`. Assemble is a Grunt.js plugin, so you have as much flexibility as you would with any other Grunt.js plugin. Your project structure is whatever you want it to be. You can put your [layouts][layouts], [pages][pages], posts, [partials][options-partials] or any other files wherever you want them to be. You can use an `includes` directory instead of `partials`. In fact, you could add hundreds of [targets](http://gruntjs.com/configuring-tasks) in the assemble task in your Gruntfile, and use a different convention for each one if you had a reason.

### _config.yml

A requirement to use `_config.yml`, or `config.json`, or `config` anything. Instead, Assemble provides [options.data][options-data] which enables you to use your own conventions for configuration. You can name your files however you want, or put them in whatever directory you want. It's up to you.


## Learn more

{{#draft}}* [Why Assemble?][why-assemble]{{/draft}}
* [Options][options]
* [variables][built-in-variables]
* [templates-overview][templates-overview]


