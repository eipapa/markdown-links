---
title: Custom Helpers

area: docs
section: templates
---

> Custom helpers and [Lo-Dash mixins](./External-Libraries.html) are so easy to use with Assemble, the possibilities are truly limitless. Contributors welcome! Please consider adding your helpers to this library!

To make it easier for Assemble users to consume custom helpers created by other users, we recommend the following conventions.

### Also see [Helpers](./Helpers.html) | [options.helpers](./options-helpers.html) →

## Adding Custom Helpers

Handlebars makes it really easy to add custom helpers. Just register your function into Handlebars with the `Handlebars.registerHelper` method and that helper will be available to any template you compile afterwards.

## Registering custom Handlebars helpers

Helpers can either be an object or a single `register` function. If `register` is on the object, then it calls the `register` function, passing in the engine. Otherwise each method is registered as a helper. For example, the following will result in two helpers being registered:

```js
module.exports.foo = function(str) { return str; };
module.exports.bar = function(str) { return str; };
```

And this will register the `foo` helper directly through Handlebars:

```js
module.exports.register = function(Handlebars, options) {
  Handlebars.registerHelper('foo', function(str) {
    return str;
  });
};
```

The `Handlebars.registerHelper` method takes the name of the helper and the helper function as arguments. Handlebars.js then takes whatever is returned from the helper function and writes it out to the template, _so be sure to always return a string from your custom helpers_.

## Loading Helpers

Minimatch patterns can be used in the `helpers` option, and they'll look inside your devDependencies for any node modules that it finds. If it finds modules, it will attempt to load those as helpers.

Requirements for use:

 - Install the module and save to devDependencies
   - `npm install my-custom-helper --save-dev`
 - Add a pattern (or the entire name) to use that module in the options
   - `options: { helpers: ['*-helper-module-name'] } }`
 - Enjoy


## Developing Custom Helpers

### Passing `assemble.options` into helpers

Any value from `assemble.options` may be passed to helpers when the helper defines the `register` method. For example:

Given our `Gruntfile.js` has the following `assemble` task configuration:

```js
assemble: {
  options: {
    version: '0.1.0', // or we could use '<%= pkg.version %>'
  },
  ...
}
```

And given we have defined a custom helper, `opt`, which gets properties from the `assemble.options` object and returns them:

```js
module.exports.register = function(Handlebars, options) {

  Handlebars.registerHelper('opt', function(key) {
    return options[key] || '';
  });

};
```

We can now user our helper in a Handlebars template like this:

``` html
<div>Version: v\{{opt 'version'}}</div>
```

And the output would be something like:

``` html
<div>Version: v0.1.0</div>
```


## Quickstart using [grunt-init](https://github.com/gruntjs/grunt-init)

### 1. Install grunt-init
If you haven't already done so, install [Grunt][grunt] and [grunt-init][]:

``` bash
npm i -g grunt-cli grunt-init
```
_**Windows users**, see [the documentation][grunt-init] for the correct destination directory path_.

<br>
Once grunt-init is installed, place the template in your `~/.grunt-init/` directory. It's recommended that you use `git clone` to install this template into that directory as follows:


### 2. Install [grunt-init-helper](https://github.com/assemble/grunt-init-helper)

``` bash
git clone https://github.com/assemble/grunt-init-helper.git ~/.grunt-init/helper
```

### 3. Install dependencies

Then, in the directory where your custom helpers will be stored, run `grunt-init helper` and follow the prompts to generate a new helper with placeholder code that should be customized.

**Note** that you may also force `grunt-init` to use custom default values, move the `defaults.json` file to your `~/.grunt-init/` directory, and customize the values in that file.


## Conventions and Recommendations
If you are creating a helper for distribution, then you might consider using [grunt-init-assemble](https://github.com/assemble/grunt-init-assemble) first to create a new Assemble project, then use [grunt-init-helper](https://github.com/assemble/grunt-init-helper) to generate the new helper.

We recommend that you save the helper to the root of the project to make it easy for others to consume via package managers, such as [Bower](https://github.com/bower/bower).

### Naming Conventions
* **project name**: It is recommended that you use the following pattern: "`assemble-helper-[custom helper name]`" (with `helper` being singular or plural).
* **helper name**: Name the helper itself something like "`helper-[helper-name].js`". All "official" helpers have been created following the pattern "helper-*.js" so that they can easily be consumed by `assemble.options.helpers` via simple minimatch patterns. This doesn't prevent them from being used elsewhere either.

### "Generalizing" code
Oftentimes, beyond being used as a Handlebars helper, the code for many helpers can easily be generalized so that they can also be used as Lo-Dash mixins, filters for other template engines etc. It's worth doing this whenever you can to make the helper more useful to others. Also:

* Make sure you add a `main` property to the project's **package.json** with a path to the helper.
* Register the helper with [Bower](https://github.com/bower/bower) and add a [bower.json](https://github.com/bower/bower#defining-a-package) for easy downloading and consumption of the helper.
* Add a test folder with any tests
* If you want to demonstrate the helper, add those to the test folder as well


## Related info

* [Learn about Templates][templates-overview]
* [Helpers][helpers]
* [options.helpers][options-helpers]
* [Options][options]


### External Links

* [handlebars-helpers Github repo][handlebars-helpers]
* [Handlebarsjs.com Block Helpers](http://handlebarsjs.com/block_helpers.html "Block Helpers")
* [Treehouse Blog, Handlebars.js Part 2: Partials and Helpers](http://blog.teamtreehouse.com/handlebars-js-part-2-partials-and-helpers)
* [NetTuts+: An Introduction to Handlebars](http://net.tutsplus.com/tutorials/javascript-ajax/introduction-to-handlebars/)

[handlebars-helpers]: http://github.com/assemble/handlebars-helpers "Extensive collection of Handlebars helpers"
[grunt-init]: http:/gruntjs.com